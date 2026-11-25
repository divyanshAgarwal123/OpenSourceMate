# Production API documentation policy — #440

This change reuses the existing FastAPI OpenAPI generator and serializers. `API_DOCS_ENABLED` defaults to false in production/prod and true elsewhere, with an explicit override. HTTP Swagger UI, its OAuth redirect, ReDoc and the schema disappear together. Discovery returns `enabled: false` and null links when disabled. Functional APIs remain available. The schema now documents the existing unified API error envelope.

Validation used a fresh installation of the declared Python 3.12 requirements, including FastAPI 0.162.7. `pip check`, all 32 focused tests (15 new), and Mypy on 38 application files pass. The offline schema check covers 27 paths, operation/response structure and generated local references. Invalid documents fail the check. Its documented scope excludes complete OpenAPI semantic validation.

Real Uvicorn and Chrome acceptance covered development, production defaults, production with documentation enabled, and development with documentation disabled. Swagger’s live Execute returned HTTP 200 and a healthy response at 1,280 and 390 pixels in both enabled configurations. Browser errors and horizontal overflow were absent. Disabled configurations returned 404 for all four documentation URLs and advertised no documentation links.

The complete backend suite has 426 passes, 17 failures and one setup error. The exact parent, `f6d84ec`, has 411 passes and the same 17 failures and setup error. Coverage is 89.63%, above the required 80%. There are no added failing test IDs or Ruff diagnostics after mapping unchanged lines; full Ruff reports 109 errors versus 118 on the parent. Scoped formatting and lint pass.

The unchanged frontend has 700 passing and 24 failing tests, with existing lint, type and build failures involving TypeScript 7 support, JSX in `.ts` tests and mock data/route configuration. Node 22 installation, codegen consistency, the production npm audit and source secret scans pass. Local pip-audit was unavailable; hosted audits remain pending. Repository-wide gates therefore remain blocked.

The manifest binds the source commit, its actual parent, 10 source blobs and every public artifact digest. Captured plaintext logs have trailing whitespace normalized. Full raw test reports remain local; their hashes are recorded alongside the public outcome summary.
