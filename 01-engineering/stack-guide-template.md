# Stack Guide: [Bahasa / framework / versi]

Gunakan template ini di repo proyek atau handbook stack khusus. Tuliskan hanya aturan yang berbeda atau lebih rinci dari baseline bersama. Pin versi runtime/framework, beri tanggal review, dan tautkan dokumentasi resmi yang menjadi sumber.

## Metadata dan dukungan

- Stack/runtime/framework dan versi yang didukung:
- Owner:
- Last reviewed / next review:
- Official documentation / version policy:
- End-of-life and upgrade policy:

## Perintah standar

| Tujuan | Perintah | Kapan dijalankan |
| --- | --- | --- |
| Install dependencies | [command] | [condition] |
| Format | [command] | [before PR/CI] |
| Lint/static analysis | [command] | [before PR/CI] |
| Test | [command] | [scope] |
| Build/run | [command] | [scope] |

## Repository layout

- Lokasi entry points, domain/business logic, adapters, config, tests, migrations, dan generated files:
- Konvensi nama dan import:
- Aturan module/package boundaries:

## Coding patterns

- Error handling dan validation:
- Dependency injection/lifecycle/resource cleanup:
- Async/concurrency/thread-safety:
- Logging, metrics, tracing, correlation IDs:
- API and serialization:

## Security and data

- Supported authentication/authorization integrations:
- Secure configuration and secret handling:
- Query/output/file-handling guidance:
- Data migration and compatibility:
- Unsafe APIs/patterns yang dilarang dan alternatifnya:

## Tests and quality gates

- Unit/integration/e2e conventions:
- Fixtures and test-data constraints:
- Coverage expectations for critical paths:
- CI checks and merge blockers:

## Upgrade and exceptions

- Version update cadence and compatibility window:
- Migration guide and rollback approach:
- Stack-specific exceptions to handbook baseline:
- Owner and review date:
