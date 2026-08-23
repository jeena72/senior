# Engineering Practices

[← Back to README](README.md)

Applied engineering topics every Senior/Lead Python developer is expected to know: the modern toolchain, reproducible environments, the web stack, configuration, observability, Docker, and security.

## Table of Contents
- [Modern Python Tooling (2025-2026)](#modern-python-tooling-2025-2026)
- [Dependency Management and Reproducible Environments](#dependency-management-and-reproducible-environments)
- [WSGI vs ASGI and the modern web stack](#wsgi-vs-asgi-and-the-modern-web-stack)
- [Configuration and secrets (12-factor in practice)](#configuration-and-secrets-12-factor-in-practice)
- [Structured logging and observability](#structured-logging-and-observability)
- [Docker best practices for Python](#docker-best-practices-for-python)
- [Security essentials for Python developers](#security-essentials-for-python-developers)

## Modern Python Tooling (2025-2026)

The Python toolchain consolidated hard over the last three years. A senior developer is expected
to know not just the tool names, but *why* the ecosystem moved.

| Job | Legacy stack | Modern stack (2025-2026) | Why it replaced the old one |
|---|---|---|---|
| Env + install | `virtualenv` + `pip` + `pip-tools` | **uv** | 10-100x faster, resolver + lockfile + Python installs in one binary |
| Format | `black` + `isort` | **ruff format** | One tool, ~black-compatible output, no config drift |
| Lint | `flake8` + plugins + `pylint` | **ruff check** | Reimplements 800+ rules from ~50 plugins in Rust; instant on large repos |
| Types | (none) | **mypy** or **pyright** | Catches whole bug classes before tests run |
| Gate | Manual discipline | **pre-commit** + CI | Enforcement must be mechanical, not social |

### uv: one tool instead of five

```bash
uv init myproject && cd myproject   # creates pyproject.toml + .python-version
uv python install 3.14              # manages interpreters too - no pyenv needed
uv add fastapi "httpx>=0.28"        # resolves, writes uv.lock, updates .venv
uv add --dev pytest ruff mypy       # PEP 735 dependency group, not a prod dep
uv run pytest                       # auto-syncs the env, then runs - no "activate"
uv sync --frozen                    # CI/prod: install exactly the lock, fail on drift
uvx ruff check .                    # run a tool without installing it into the project
```

**Why uv over `python -m venv` + `pip install -r requirements.txt`:**
- `pip install -r` is **not reproducible**: transitive dependencies float unless every one is pinned.
  `uv.lock` pins the entire graph with hashes, cross-platform, in one file.
- `uv run` removes the "did I activate the right venv?" class of bugs — the environment is
  derived from the project, not from shell state.
- One binary replaces `pyenv` + `virtualenv` + `pip` + `pip-tools` + `pipx`, so CI images shrink
  and local setup becomes `uv sync`.

**Why uv over Poetry:** Poetry pioneered lockfiles but predates the standards; historically it
used a non-standard `[tool.poetry]` table and its own resolver. uv is built on PEP 621 metadata
(`[project]`), so your `pyproject.toml` stays portable to any other tool. Poetry is still a fine,
mature choice — the anti-pattern is unpinned `pip` + `requirements.txt` in 2026.

### Ruff: lint and format

```toml
# pyproject.toml
[tool.ruff]
line-length = 100
target-version = "py313"

[tool.ruff.lint]
select = ["E", "F", "I", "UP", "B", "SIM", "RUF", "ASYNC", "S"]
# E/F pycodestyle+pyflakes, I isort, UP pyupgrade, B bugbear,
# SIM simplify, ASYNC async-specific bugs, S bandit security rules
ignore = ["E501"]              # the formatter owns line length

[tool.ruff.lint.per-file-ignores]
"tests/*" = ["S101"]           # asserts are the point in tests
```

```bash
ruff check --fix .    # autofix ~60% of findings
ruff format .
```

**Why Ruff over black + flake8 + isort + pyupgrade:** those were four tools with four configs,
four CI steps, and mutually contradictory opinions (the classic `black` vs `flake8 E203` fight).
Ruff is one process, one config table, and fast enough to run on every keystroke — which is what
actually makes teams keep the linter green.

### Type checking

```bash
mypy src/          # gradual, plugin ecosystem (SQLAlchemy, Django via django-stubs)
pyright src/       # faster, stricter inference, powers the VS Code experience
```

Start with `mypy --strict` **on new modules only**; retrofitting a whole legacy codebase at once
produces thousands of errors and the check gets disabled. Ratchet instead:

```toml
[tool.mypy]
strict = true
[[tool.mypy.overrides]]
module = ["legacy.*"]
ignore_errors = true      # shrink this list over time; never grow it
```

Note the emerging Rust-based checkers (**ty** from Astral, **pyrefly** from Meta, both preview as
of 2026) — worth watching, but mypy/pyright remain the production answer today.

### pre-commit: make it mechanical

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.14.0
    hooks:
      - id: ruff-check
        args: [--fix]
      - id: ruff-format
  - repo: https://github.com/astral-sh/uv-pre-commit
    rev: 0.9.0
    hooks:
      - id: uv-lock          # fails if pyproject.toml and uv.lock disagree
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v6.0.0
    hooks:
      - id: check-merge-conflict
      - id: detect-private-key
```

```bash
pre-commit install                 # local git hook
pre-commit run --all-files         # also run this in CI - hooks must not be bypassable
```

**Why pre-commit and *also* CI:** the local hook gives fast feedback, but `git commit --no-verify`
exists. The CI job is the actual gate. Running the same config in both places means "works on my
machine" and "passes the pipeline" are the same statement.

## Dependency Management and Reproducible Environments

"It worked yesterday" is almost always a dependency problem. A senior developer should be able to
explain the difference between *declaring*, *resolving*, and *installing* dependencies.

### Three files, three jobs

| File | Contains | Written by | Committed? |
|---|---|---|---|
| `pyproject.toml` | Abstract ranges: `httpx>=0.28,<1.0` | Humans | Yes |
| `uv.lock` / `poetry.lock` / `pylock.toml` | Exact versions + hashes for the whole graph | The resolver | Yes |
| `.venv/` | Installed artifacts | The installer | **No** (`.gitignore`) |

The classic mistake is using `requirements.txt` for both jobs at once. Either it holds loose ranges
(then installs are not reproducible) or it holds `pip freeze` output (then you have lost the
information about *which* packages you actually asked for, and upgrades become guesswork).

### Declaring dependencies (PEP 621 + PEP 735)

```toml
[project]
name = "myservice"
requires-python = ">=3.12"
dependencies = [
    "fastapi>=0.120",
    "sqlalchemy[asyncio]>=2.0",
]

[dependency-groups]              # PEP 735 - dev deps that are NOT extras
dev = ["pytest>=8", "pytest-asyncio", "ruff", "mypy"]
docs = ["sphinx>=8"]
```

**Why `[dependency-groups]` and not `[project.optional-dependencies]`:** extras are *published* —
`pip install myservice[dev]` would give your users your test tooling. Dependency groups are
local-only development metadata and never ship in the wheel.

**Applications vs libraries — the key distinction:**
- **Libraries** declare *wide* ranges and must **not** ship a lockfile as a constraint. Pinning
  `requests==2.32.3` in a library makes it uninstallable next to any app that needs another version.
- **Applications** declare ranges *and* commit a lockfile. The app is the one place where the
  entire dependency graph gets decided, so decide it once and deploy that exact set everywhere.

### Locking

```bash
uv lock                    # resolve pyproject.toml -> uv.lock (all platforms, with hashes)
uv sync --frozen           # install exactly uv.lock; error if it is out of date
uv lock --upgrade-package httpx    # deliberate, reviewable single-package bump
uv export --format pylock.toml -o pylock.toml   # PEP 751 standard interchange format
```

**PEP 751 (`pylock.toml`)** standardised the lockfile format in 2025 so lockfiles stop being
tool-private; pip 25.1+ can install from one directly. Use it when you need to hand a locked
environment to a tool that does not speak `uv.lock`.

### Environment hygiene

- **Never `sudo pip install`.** Since PEP 668, system Pythons on Debian/Ubuntu/Fedora refuse it
  (`externally-managed-environment`) precisely because it can break OS tooling.
- **One venv per project**, created from the project's `requires-python`, never shared.
- **Install CLI tools in isolation** (`uv tool install ruff` / `pipx`), not into the project venv —
  otherwise your linter's transitive deps join your application's resolution and cause conflicts.
- **Pin `requires-python` narrowly.** `>=3.12` resolves differently from `>=3.9`; the resolver must
  pick versions compatible with the *oldest* allowed interpreter, silently holding you on old code.

### Keeping dependencies fresh

Automate upgrades with **Renovate** or **Dependabot** so the diff is one PR per package with a
changelog, reviewed by CI. The alternative — a yearly "upgrade everything" sprint — is where
projects get stuck on an EOL framework. Pair it with `uv lock --upgrade` on a schedule and let the
test suite be the acceptance gate.

## WSGI vs ASGI and the modern web stack

### The two interfaces

**WSGI** (PEP 3333, 2003) is a synchronous callable: one request in, one response out, one thread
blocked for the duration. It cannot represent WebSockets, server-sent events, background tasks
after the response, or long-lived connections, because the protocol has no vocabulary for them.

**ASGI** is the async successor: an `async` callable receiving a `scope` plus `receive`/`send`
channels, so a single connection can exchange many messages. That is what makes WebSockets,
SSE, HTTP/2 and lifespan (startup/shutdown) events expressible.

```python
async def app(scope, receive, send):          # the entire ASGI contract
    assert scope["type"] == "http"
    await send({"type": "http.response.start", "status": 200,
                "headers": [(b"content-type", b"text/plain")]})
    await send({"type": "http.response.body", "body": b"ok"})
```

| | WSGI | ASGI |
|---|---|---|
| Frameworks | Flask, Django (sync), Pyramid | FastAPI/Starlette, Litestar, Django (async), Quart |
| Servers | gunicorn, uWSGI, waitress | uvicorn, hypercorn, granian |
| WebSockets / SSE | No | Yes |
| Concurrency per worker | One request per thread | Thousands of connections per event loop |
| Best at | CPU-ish handlers, mature sync ORMs | High-fan-out I/O, streaming, long-lived connections |

**ASGI is not automatically faster.** For a handler that spends its time in a synchronous ORM and
CPU work, WSGI with threads is equally good and far simpler. ASGI wins when a request spends most
of its time *waiting* on other services — which is exactly what a microservice does.

### FastAPI: what to actually know

```python
from fastapi import Depends, FastAPI
from pydantic import BaseModel, Field

app = FastAPI()

class OrderIn(BaseModel):
    sku: str
    qty: int = Field(gt=0, le=100)     # validation lives in the type, not in if-statements

async def get_repo() -> OrderRepo:     # dependency injection, overridable in tests
    async with session_factory() as s:
        yield OrderRepo(s)

@app.post("/orders", status_code=201)
async def create(order: OrderIn, repo: OrderRepo = Depends(get_repo)) -> OrderOut:
    return await repo.create(order)
```

**Why type-driven validation over manual parsing:** the same annotation produces request parsing,
validation, the error response, the response serialisation *and* the OpenAPI schema. Hand-written
validation drifts from the documentation within weeks; here they cannot drift, because they are
generated from one declaration.

**Why `Depends` over module-level globals:** `app.dependency_overrides[get_repo] = fake_repo` makes
integration tests trivial without monkeypatching imports.

### The sync/async trap in FastAPI

- `async def` endpoint → runs **on the event loop**. Any blocking call inside it stalls the worker.
- `def` (sync) endpoint → FastAPI runs it in a **threadpool** automatically, which is safe but
  bounded (~40 threads by default).

So a blocking DB driver in an `async def` endpoint is far worse than the same driver in a plain
`def` endpoint. Pick one honestly: either go async end-to-end (asyncpg/psycopg3-async, httpx,
redis-py asyncio) or stay sync and let the threadpool do its job. Half-async is the worst option.

### Running it in production

```bash
# CPU-bound-ish or mixed: multiple processes, one loop each
uvicorn app:app --workers 4 --host 0.0.0.0 --port 8000
```

- **Workers ≈ CPU cores** for a container. Async workers need *fewer* than WSGI workers, because
  one worker already handles thousands of concurrent connections.
- Put a real reverse proxy / ingress in front for TLS, timeouts, slow-client buffering and
  gzip — application servers are not hardened edge servers.
- Set `--timeout-graceful-shutdown` and handle `SIGTERM` so rolling deploys drain in-flight
  requests instead of dropping them.
- Expose `/health` (liveness) and `/ready` (readiness — checks DB/broker) as *separate* endpoints;
  conflating them makes orchestrators kill pods that are merely waiting on a dependency.

## Configuration and secrets (12-factor in practice)

The 12-factor rule is *"store config in the environment"*, and the reason is deployability: the
same immutable artifact must run in dev, staging and prod with nothing changed but the environment.
The moment configuration lives inside the image, you need a different build per environment and
"promoting a tested build to prod" stops being true.

### The anti-pattern

```python
# settings.py - three problems in six lines
import os
DEBUG = os.environ.get("DEBUG", False)          # "false" is a truthy string!
PORT = os.environ["PORT"]                       # a str, not an int
DB = os.environ.get("DATABASE_URL")             # None until it explodes at 3am
SECRET = "hunter2"                              # committed forever, in git history
```

Environment variables are strings with no schema, so every consumer re-parses them differently and
a typo (`DATABSE_URL`) surfaces as a `NoneType` error deep inside a request handler.

### Typed settings with pydantic-settings

```python
from functools import lru_cache
from pydantic import Field, PostgresDsn, SecretStr
from pydantic_settings import BaseSettings, SettingsConfigDict

class Settings(BaseSettings):
    model_config = SettingsConfigDict(
        env_file=".env",              # local dev only; absent in prod
        env_prefix="APP_",            # APP_DATABASE_URL -> database_url
        env_nested_delimiter="__",    # APP_REDIS__HOST -> redis.host
        frozen=True,                  # config is immutable after startup
        extra="forbid",               # a typo'd env var fails loudly
    )

    environment: str = "local"
    debug: bool = False                          # parses "0"/"false"/"no" correctly
    database_url: PostgresDsn                    # no default -> required
    secret_key: SecretStr                        # never printed by repr() or logs
    request_timeout_s: float = Field(default=5.0, gt=0)

@lru_cache
def get_settings() -> Settings:
    return Settings()                # validated once, at import/startup
```

**Why this beats `os.environ.get` everywhere:**
- **Fail fast at startup**, not on the first request that touches the missing value. A pod that
  cannot start is a clear signal; a pod that 500s intermittently is a debugging session.
- **Types, not strings** — `bool`, `int`, URLs and enums are parsed and validated once.
- **`SecretStr` prevents the classic leak**: an exception repr or a debug log dumping the settings
  object would otherwise print your DB password into your log aggregator.
- **`extra="forbid"`** catches `APP_DATABSE_URL` at boot instead of silently using the default.

### Secrets: env vars are the floor, not the ceiling

Environment variables are fine for low-sensitivity config, but they are readable via `/proc`,
leak into crash dumps and child processes, and cannot be rotated without a restart. For real
secrets use a manager (AWS Secrets Manager, GCP Secret Manager, Vault, or Kubernetes Secrets backed
by an external store) and fetch at startup — pydantic-settings supports custom sources for this.

Rules that survive audits:
- **Never commit secrets.** Add `detect-private-key` / `gitleaks` to pre-commit; a secret in git
  history is compromised even after you delete the file.
- `.env` is for **local development only** and is gitignored. Commit a `.env.example` with keys
  and dummy values so onboarding is one copy command.
- **Rotate on exposure, always.** "It was only in a private repo" is not a mitigation.
- Keep **feature flags** out of config files. Flags change at runtime; config changes at deploy.
  Mixing them means every experiment needs a redeploy.

## Structured logging and observability

### stdlib `logging` pitfalls a senior must know

```python
import logging
logger = logging.getLogger(__name__)      # module-level, named - never the root logger

# WRONG - the f-string is evaluated even when DEBUG is disabled,
# and every message is a unique string, so it cannot be aggregated
logger.debug(f"processed order {order.id} for {user.email} in {elapsed}s")

# RIGHT - lazy interpolation, and the message stays a constant template
logger.debug("processed order %s for %s in %ss", order.id, user.email, elapsed)

# WRONG - loses the traceback
except ValueError as e:
    logger.error(f"failed: {e}")

# RIGHT - inside an except block, logger.exception() attaches the traceback
except ValueError:
    logger.exception("order processing failed", extra={"order_id": order.id})
```

Other traps:
- **Never call `basicConfig()` in a library.** Configuring handlers is the *application's* job; a
  library that does it hijacks the host app's logging. Libraries attach `logging.NullHandler()`.
- **Configure once, declaratively**, with `logging.config.dictConfig()` at startup — not with
  scattered `addHandler` calls that double-log after a reload.
- **Logging is synchronous I/O.** A slow log sink blocks your request thread or event loop. In
  high-throughput services use `QueueHandler` + `QueueListener` so handlers run on their own thread.
- `print()` is not logging: no level, no timestamp, no context, no way to turn it off, and it
  bypasses every handler and filter you configured.

### Why structured (JSON) logs

Grep-friendly prose stops working the moment logs are centralised. `"order 123 failed"` cannot be
queried as "all failures for customer X in the last hour, grouped by endpoint". Structured events
can.

```python
import structlog

structlog.configure(
    processors=[
        structlog.contextvars.merge_contextvars,   # request-scoped context, async-safe
        structlog.processors.add_log_level,
        structlog.processors.TimeStamper(fmt="iso", utc=True),
        structlog.processors.format_exc_info,
        structlog.processors.JSONRenderer(),       # ConsoleRenderer() in dev
    ],
    wrapper_class=structlog.make_filtering_bound_logger(logging.INFO),
)

log = structlog.get_logger()

# in middleware, once per request:
structlog.contextvars.bind_contextvars(request_id=rid, user_id=uid, path=path)

# anywhere deeper in the call stack - context comes along for free:
log.info("order_created", order_id=order.id, amount_cents=4200, currency="EUR")
# -> {"event":"order_created","order_id":17,"amount_cents":4200,"currency":"EUR",
#     "request_id":"a1b2","user_id":9,"level":"info","timestamp":"2026-08-23T10:00:00Z"}
```

**Why structlog over hand-rolled JSON formatters:** `contextvars` binding means request ID, user
and tenant are attached automatically to every log line in that request — including from deep
library code — without threading a context object through every function signature. It works
correctly under asyncio, where thread-locals do not.

**Why `event` names are constants:** `log.info("order_created", order_id=...)` gives one
aggregatable event type. Interpolating the ID into the message would create unbounded cardinality,
which is what makes log platforms expensive and dashboards impossible.

### The three signals, and OpenTelemetry

**Logs** say what happened, **metrics** say how much/how often, **traces** say where the time went
across services. You need all three; a Lead should know which question each one answers.

```bash
pip install opentelemetry-distro opentelemetry-exporter-otlp
opentelemetry-bootstrap -a install       # auto-detects and installs instrumentation
OTEL_SERVICE_NAME=orders \
OTEL_EXPORTER_OTLP_ENDPOINT=http://collector:4317 \
  opentelemetry-instrument uvicorn app:app
```

That single wrapper instruments FastAPI, httpx, SQLAlchemy, Redis and more without touching your
code — spans for every request and every outbound call, propagated via W3C `traceparent` headers.

**Why OpenTelemetry over a vendor SDK:** OTel is a CNCF standard, so instrumentation is written
once and the *exporter* decides whether data goes to Jaeger, Grafana Tempo, Datadog or Honeycomb.
Vendor SDKs make instrumentation a migration project.

Finally, **put `trace_id` in your logs** (a structlog processor can pull it from the active span).
That link — click an error log, land on the exact distributed trace — is what actually shortens
incident resolution, and it is the difference between "we have logs" and "we have observability".

## Docker best practices for Python

### A production Dockerfile

```dockerfile
# syntax=docker/dockerfile:1

# ---- build stage: has the toolchain, never ships ----
FROM python:3.14-slim AS builder
COPY --from=ghcr.io/astral-sh/uv:latest /uv /usr/local/bin/uv

ENV UV_COMPILE_BYTECODE=1 \
    UV_LINK_MODE=copy \
    UV_PYTHON_DOWNLOADS=never

WORKDIR /app
# dependencies first: this layer is cached until the lockfile changes
COPY pyproject.toml uv.lock ./
RUN --mount=type=cache,target=/root/.cache/uv \
    uv sync --frozen --no-install-project --no-dev

COPY src/ ./src/
RUN --mount=type=cache,target=/root/.cache/uv \
    uv sync --frozen --no-dev

# ---- runtime stage: only the venv and the code ----
FROM python:3.14-slim AS runtime
RUN groupadd -r app && useradd -r -g app app

ENV PATH="/app/.venv/bin:$PATH" \
    PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONFAULTHANDLER=1

WORKDIR /app
COPY --from=builder --chown=app:app /app /app
USER app

EXPOSE 8000
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### Why each choice

- **Multi-stage.** Compilers, headers and build caches are needed to *build* wheels, never to run
  them. Shipping them doubles image size and adds CVEs you will have to answer for in a scan.
- **Copy the lockfile before the source.** Docker caches layers by content: source changes on every
  commit, dependencies change weekly. Copying `pyproject.toml`/`uv.lock` first means a code change
  rebuilds in seconds instead of reinstalling the whole dependency tree.
- **`--mount=type=cache`.** Keeps the package cache across builds without baking it into a layer.
- **`--frozen --no-dev`.** `--frozen` fails the build if the lock is stale (so a drifted dependency
  is caught in CI, not in prod); `--no-dev` keeps pytest and ruff out of the runtime image.
- **`slim`, not `alpine`.** Alpine uses musl, so PyPI's `manylinux` wheels do not apply: pip falls
  back to **compiling from source**, turning a 30-second build into 15 minutes, producing a *larger*
  image, and occasionally hitting musl-specific runtime bugs. `slim` is the right default;
  `-alpine` is a trap that looks like an optimisation.
- **Non-root `USER`.** A container escape from root is far more damaging, and most Kubernetes
  admission policies (`runAsNonRoot`) reject root images outright.
- **`PYTHONUNBUFFERED=1`.** Without it, stdout is block-buffered when not a TTY and your logs
  appear minutes late — or vanish entirely when the container is killed.
- **`UV_COMPILE_BYTECODE=1`.** Pre-compiles `.pyc` at build time so the first request does not pay
  compilation cost (matters for autoscaling and serverless cold starts).
- **Exec-form `CMD`.** Shell form (`CMD uvicorn ...`) makes `/bin/sh` PID 1, which does not forward
  `SIGTERM` — so your app never drains gracefully and Kubernetes SIGKILLs it after the grace period.

### Operational rules

- **Pin the base image by digest** (`python:3.14-slim@sha256:...`) for reproducibility, and rebuild
  weekly so OS CVE fixes actually reach production. A tag is a moving target.
- **`.dockerignore` is not optional** — exclude `.git`, `.venv`, `__pycache__`, `tests`, `.env`.
  Otherwise the build context is huge and a local `.env` can end up inside the image.
- **One process per container.** Scaling, restarts and logging all assume it.
- **Never bake secrets in.** `ENV DB_PASSWORD=...` is visible in `docker history` to anyone with
  the image. Use runtime env injection or `--mount=type=secret` at build time.
- **Scan images** (`trivy`, `grype`) in CI and fail on new HIGH/CRITICAL findings.
- Consider **distroless** or `-slim` with a stripped runtime once the above is in place; do not
  start there, because debugging a distroless container without a shell is painful.

## Security essentials for Python developers

### Deserialisation: `pickle` is code execution

```python
import pickle
pickle.loads(untrusted_bytes)      # arbitrary code execution, by design
```

`pickle` invokes `__reduce__` on unpickling, which can return any callable — a malicious payload
runs `os.system` before your first line of code. The docs say it plainly: pickle is not secure.

- Never unpickle data crossing a trust boundary — cookies, cache entries, queue messages, uploads.
- Use **JSON** for interchange, **msgpack**/**protobuf** for compact binary, **pydantic** to
  validate the result into typed objects.
- The same applies to `yaml.load` (use **`yaml.safe_load`**), `marshal`, and `dill`.
- Redis/Memcached used as a pickle cache is a real-world RCE path: anyone who can write to the
  cache owns your app servers.

### Injection

```python
# SQL - WRONG: string building
cur.execute(f"SELECT * FROM users WHERE email = '{email}'")
# RIGHT: parameters are sent separately from the query text, so they can never become SQL
cur.execute("SELECT * FROM users WHERE email = %s", (email,))

# Shell - WRONG
subprocess.run(f"convert {filename} out.png", shell=True)
# RIGHT: argument list, no shell, no metacharacter interpretation
subprocess.run(["convert", filename, "out.png"], check=True, timeout=30)
```

ORMs protect you only where you use them: `session.execute(text(f"... {x}"))` is just as injectable.
Also validate paths from users (`Path(base, name).resolve().is_relative_to(base)`) — `../` traversal
is still one of the most common findings in Python code reviews.

### Cryptography and randomness

```python
import secrets, hmac
token = secrets.token_urlsafe(32)          # NOT random.random() - Mersenne Twister is
                                           # predictable from ~624 observed outputs
if hmac.compare_digest(provided, expected):  # constant-time; `==` leaks length/prefix via timing
    ...
```

Hash passwords with **argon2-cffi** or **bcrypt**, never SHA-256 — fast hashes are exactly what an
offline cracker wants. Use the **cryptography** library rather than assembling primitives yourself.

### Other Python-specific traps

- **`assert` is stripped by `python -O`.** Never use it for authorisation or input validation.
- **`eval`/`exec` on user input** — there is no safe sandbox in CPython. Don't.
- **XML** — use **defusedxml**; stdlib parsers are vulnerable to billion-laughs and XXE.
- **Archive extraction** — `tarfile.extractall()` can write outside the target directory. Python
  3.12 added `filter="data"` and 3.14 makes it the default (PEP 706); pass it explicitly if you
  support older versions.
- **Debug mode in production** — Flask's debugger and Django's `DEBUG=True` expose a console and
  full settings. Assert `settings.debug is False` at startup in prod.
- **SSRF** — user-supplied URLs fetched server-side reach your cloud metadata endpoint. Allowlist
  hosts, resolve and reject private ranges, disable redirects.

### Supply chain

The Python ecosystem has seen repeated typosquatting and account-takeover attacks; treat
dependencies as untrusted code you execute.

```bash
uv run pip-audit             # known CVEs in your resolved dependency tree
uv run bandit -r src/        # static analysis for the patterns above
ruff check --select S src/   # the same bandit rules, inline in your linter
```

Practices that matter:
- **Commit a lockfile with hashes.** Hash-pinned installs make a compromised re-upload fail loudly
  rather than silently changing what you ship.
- **Beware dependency confusion.** If you use a private index, ensure your installer cannot
  silently prefer a public package of the same name (`uv`'s default index strategy is safe; plain
  `pip` with multiple `--extra-index-url`s is **not** — it picks the highest version anywhere).
- **Vet before adding.** Check maintenance activity, maintainer count and whether the package
  actually needs to exist. Every dependency is a permanent trust relationship.
- **Enable Dependabot/Renovate + `pip-audit` in CI**, and fail the build on known-exploited CVEs.
- **Publish with Trusted Publishing (OIDC)** rather than long-lived API tokens, and enable PyPI
  attestations (PEP 740) so consumers can verify an artifact came from your repository.
