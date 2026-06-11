---
tags:
  - prompt
  - backend
  - bugzora
aliases:
  - Backend API Prompt
parent: "[[03_Yazilim_Mimarisi]]"
dg-publish: true
---

# PROMPT 01 - BugZora Backend Platform API

> **📎 Referans Dosyalar** — Bu promptu kullanmadan önce aşağıdaki dokümanları bağlam olarak ekle:
> - `@03_Yazilim_Mimarisi.md` — Microservice mimarisi, servis sorumlulukları, iletişim pattern'leri
> - `@05_Veritabani_Tasarimi.md` — Tüm tablo şemaları, index ve migration stratejisi
> - `@06_API_Tasarimi.md` — Endpoint listesi, request/response örnekleri, hata kodları
> - `@07_Guvenlik_Mimarisi.md` — Auth modeli, RBAC, rate limiting, OWASP gereksinimleri
> - `@08_SaaS_Modeli_Fiyatlandirma.md` — Plan limitleri, quota tanımları, tenant izolasyonu

You are a senior Go backend developer and platform engineer.
Build the BugZora Platform API Gateway plus core services for a multi-tenant SaaS security scanning platform.

## Product Context
- Existing scanners already exist in Go: BugZora-ImageScan, BugZora-FileScan, BugZora-RepoScan.
- Your task is to build the SaaS control plane around them.
- The platform must support tenants, users, auth, scan orchestration, policy evaluation, reports and audit logs.

## Required Stack
- Go 1.22+
- Gin or Echo
- PostgreSQL
- Redis
- JWT + refresh tokens
- gRPC for internal communication
- Docker Compose for local development
- Goose or Atlas for migrations

## Architecture Goals
- API-first design.
- Clear domain-driven package boundaries.
- Multi-tenant isolation.
- Production-grade observability.
- Clean error handling.
- High testability.

## Deliverables
- A runnable monorepo or multi-module backend project.
- REST API for external clients.
- gRPC stubs or interfaces for internal services.
- SQL migrations.
- Unit and integration tests.
- Docker Compose stack.

## Project Structure
```text
/cmd/api-gateway
/cmd/auth-service
/cmd/tenant-service
/cmd/scan-orchestrator
/cmd/report-service
/internal/app
/internal/domain
/internal/repository
/internal/service
/internal/http
/internal/grpc
/internal/middleware
/internal/platform
/migrations
/deployments/docker-compose
/test/integration
```

## Core Modules To Implement
- Auth service
- Tenant service
- User management
- API key management
- Scan jobs API
- Results query API
- Audit log writer
- Basic policy evaluation stub
- Report request API

## Public REST Endpoints
- POST /api/v1/auth/login
- POST /api/v1/auth/logout
- POST /api/v1/auth/refresh
- GET /api/v1/tenants/current
- PATCH /api/v1/tenants/current
- GET /api/v1/users
- POST /api/v1/users
- GET /api/v1/users/:id
- PATCH /api/v1/users/:id
- DELETE /api/v1/users/:id
- POST /api/v1/scans
- GET /api/v1/scans
- GET /api/v1/scans/:id
- POST /api/v1/scans/:id/cancel
- GET /api/v1/scans/:id/results

## Data Model Requirements
- tenants table
- users table
- api_keys table
- scan_jobs table
- scan_results table
- reports table
- audit_logs table
- subscriptions table placeholder

## Middleware Requirements
- Request ID
- Structured logging
- Panic recovery
- JWT auth
- API key auth
- Tenant isolation resolver
- Rate limiting
- Idempotency key support for POST scan jobs
- Audit log capture

## Error Handling Pattern
- Use a single error envelope with fields: code, message, details, request_id.
- Map domain errors to HTTP status codes cleanly.
- Avoid leaking internals.

## Testing Requirements
- Write unit tests for services and middleware.
- Write repository tests against PostgreSQL.
- Write integration tests for auth, tenants and scan job creation.
- Include table-driven tests where appropriate.

## Docker Compose Requirements
- Services: api, postgres, redis, mailhog, optional mock-scanner.
- Provide seed data and health checks.

## Implementation Constraints
- Use context.Context everywhere.
- Add graceful shutdown.
- Use dependency injection.
- Add OpenAPI generation scaffolding.
- Add config loading from env.
- Prefer interfaces around external dependencies.

## Coding Instructions
- Create clean packages, no circular dependencies.
- Keep handlers thin and services rich.
- Put validation close to transport boundaries.
- Add pagination and filtering for list endpoints.
- Add tenant_id to all protected resources.

## Authentication Rules
- Access tokens short-lived.
- Refresh tokens stored hashed or revocable.
- Passwords hashed with bcrypt or argon2id.
- Support role claims in JWT.

## Acceptance Criteria
- `docker compose up` starts the full stack.
- `make test` or equivalent runs cleanly.
- Migrations run automatically or via a documented command.
- A developer can create a tenant, log in, create a scan job and query results.

## Output Format
- Return the full implementation.
- Include file tree.
- Include commands to run locally.
- Include sample curl commands.

## Extra Nice To Have
- Background worker interface for future Kafka/Redis queue integration.
- OpenTelemetry hooks.
- Feature flags for licensed features.

## Start Now
- Scaffold the project first.
- Then implement migrations.
- Then implement auth and tenant flows.
- Then implement scan jobs and results queries.
- Then add tests and compose.
- Instruction 001: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 002: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 003: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 004: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 005: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 006: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 007: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 008: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 009: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 010: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 011: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 012: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 013: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 014: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 015: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 016: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 017: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 018: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 019: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 020: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 021: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 022: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 023: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 024: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 025: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 026: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 027: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 028: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 029: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 030: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 031: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 032: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 033: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 034: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 035: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 036: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 037: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 038: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 039: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 040: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 041: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 042: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 043: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 044: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 045: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 046: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 047: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 048: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 049: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 050: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 051: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 052: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 053: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 054: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 055: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 056: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 057: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 058: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 059: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 060: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 061: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 062: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 063: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 064: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 065: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 066: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 067: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 068: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 069: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 070: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 071: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 072: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 073: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 074: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 075: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 076: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 077: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 078: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 079: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 080: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 081: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 082: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 083: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 084: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 085: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 086: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 087: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 088: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 089: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 090: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 091: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 092: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 093: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 094: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 095: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 096: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 097: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 098: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 099: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 100: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 101: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 102: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 103: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 104: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 105: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 106: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 107: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 108: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 109: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 110: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 111: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 112: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 113: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 114: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 115: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 116: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 117: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 118: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 119: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 120: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 121: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 122: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 123: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 124: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 125: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 126: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 127: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 128: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 129: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 130: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 131: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 132: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 133: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 134: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 135: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 136: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 137: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 138: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 139: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 140: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 141: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 142: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 143: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 144: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 145: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 146: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 147: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 148: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 149: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 150: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 151: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 152: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 153: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 154: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 155: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 156: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 157: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 158: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 159: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 160: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 161: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 162: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 163: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 164: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 165: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 166: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 167: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 168: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 169: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 170: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 171: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 172: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 173: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 174: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 175: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 176: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 177: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 178: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 179: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 180: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 181: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 182: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 183: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 184: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 185: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 186: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 187: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 188: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 189: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 190: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 191: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 192: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 193: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 194: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 195: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 196: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 197: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 198: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 199: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 200: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 201: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 202: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 203: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 204: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 205: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 206: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 207: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 208: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 209: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 210: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 211: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 212: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 213: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 214: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 215: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 216: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 217: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 218: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 219: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 220: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 221: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 222: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 223: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 224: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 225: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 226: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 227: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 228: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 229: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 230: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 231: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 232: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 233: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 234: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 235: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 236: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 237: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 238: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 239: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 240: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 241: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 242: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 243: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 244: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 245: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 246: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 247: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 248: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 249: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 250: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 251: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 252: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 253: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 254: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 255: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 256: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 257: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 258: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 259: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 260: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 261: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 262: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 263: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 264: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 265: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 266: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 267: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 268: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 269: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 270: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 271: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 272: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 273: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 274: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 275: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 276: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 277: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 278: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 279: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.
- Instruction 280: make implementation decisions explicit, produce production-grade code, and document assumptions inline when they affect multi-tenant security or reliability.


---

## 🔗 İlgili Notlar

- [[03_Yazilim_Mimarisi]]
- [[05_Veritabani_Tasarimi]]
- [[06_API_Tasarimi]]
