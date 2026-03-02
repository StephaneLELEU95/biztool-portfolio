# BizTool - Portfolio Case Study

This public repository presents BizTool as a technical case study.
The full production source code is intentionally kept private.

## 1) Product Context and Goal

BizTool targets billing workflows for freelancers and small businesses:
- clients and products management
- quote-to-invoice lifecycle
- payments and status tracking

Goal: deliver a robust, readable, and testable business API, designed to evolve toward SaaS usage.

## 2) Architecture (Engineering View)

Layered architecture:
- `api/`: HTTP routes and contracts
- `services/`: business rules (quotes/invoices/payments)
- `repositories/`: SQLAlchemy data access layer
- `models/` + `schemas/`: DB modeling + Pydantic validation
- `core/`: configuration, DB, JWT security

Typical business flow:
1. Admin JWT authentication
2. Client/product creation
3. Quote creation and amount calculations
4. Quote send/validation
5. Quote conversion to invoice
6. Partial/full payments and state transitions

## 3) Implemented Security

- JWT auth required on business routes
- `/health` kept public for monitoring
- Swagger/OpenAPI aligned with Bearer scheme
- Secret hygiene (`.env` excluded, safe `.env.example`)
- Local DB files (`*.db`) excluded from version control

## 4) Engineering Decisions and Trade-offs

- SQLAlchemy 2 + repository layer for testability and DB evolution
- Alembic for deterministic migrations and clean deployments
- Pydantic v2 validation for strict API contracts
- Clear separation of responsibilities to reduce coupling

## 5) Software Quality

- Pytest coverage on critical workflows (quotes, invoices, payments, auth)
- Explicit auth enforcement checks (401 without token)
- Structured Git history (initial import, security hardening, docs)
- Solid base for standard CI/CD extension

## 6) Covered Scenarios

- Draft quote creation, send, and post-send locking
- Quote duplication and invoice conversion
- Successive payments and `partial` to `paid` transition
- Access denial without bearer token on business routes

## 7) Work Delivered (Responsibilities)

- API design and implementation for billing domain
- Business modeling for clients/products/quotes/invoices/payments
- Global JWT auth enforcement across business routes
- Test implementation/adaptation for security requirements
- Repository hygiene and recruiter-focused documentation

## 8) Technical Roadmap

- SMTP (quote/invoice sending + reminders)
- Structured JSON logging + tracing
- Production hardening (rate limiting, stricter env profiles)
- Multi-tenant extension

## Stack

FastAPI, SQLAlchemy 2, Alembic, Pydantic v2, JWT (python-jose), Pytest.

## Full Source Access

The full codebase is kept private.
Access can be granted for recruiter/school evaluation upon request via my GitHub profile.
