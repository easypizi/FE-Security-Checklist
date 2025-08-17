# Frontend Security Checklist (2025, TypeScript)

A concise, practical, and up-to-date security guideline for modern frontend apps. Every doc includes Do/Don'ts, examples, and references.

## Contents

- Threat model and common risks → `docs/threats.md`
- Input validation → `docs/validation.md`
- HTML sanitization, XSS, Trusted Types → `docs/html-sanitization.md`
- Cookies and sessions → `docs/cookies-sessions.md`
- CSRF defenses → `docs/csrf.md`
- HTTPS and security headers (CSP, HSTS, Permissions Policy) → `docs/https-headers.md`
- Secrets management (never in the client) → `docs/secrets-management.md`
- Dependencies and supply chain → `docs/dependencies.md`
- TypeScript runtime validation patterns → `docs/typescript.md`
- PR checklist → `docs/pr-checklist.md`
- Summary → `docs/summary.md`

## How to use this repo

- Start with `docs/pr-checklist.md` during reviews.
- Use topic files for implementation details and copy-pasteable snippets.
- Keep this aligned with your stack (framework, hosting, proxies).

---

Maintained for 2025 practices: CSP without `unsafe-inline`, Trusted Types on Chromium, HttpOnly cookies for auth, SameSite where possible, runtime validation, and provenance-aware dependencies.

