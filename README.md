# Frontend Security Checklist (2025, TypeScript)

A concise, practical, and up-to-date security guideline for modern frontend apps. Every doc includes Do/Don'ts, examples, and references.

## Contents

- Threat model and common risks → [docs/threats.md](docs/threats.md)
- Input validation → [docs/validation.md](docs/validation.md)
- HTML sanitization, XSS, Trusted Types → [docs/html-sanitization.md](docs/html-sanitization.md)
- Cookies and sessions → [docs/cookies-sessions.md](docs/cookies-sessions.md)
- CSRF defenses → [docs/csrf.md](docs/csrf.md)
- HTTPS and security headers (CSP, HSTS, Permissions Policy) → [docs/https-headers.md](docs/https-headers.md)
- Secrets management (never in the client) → [docs/secrets-management.md](docs/secrets-management.md)
- Dependencies and supply chain → [docs/dependencies.md](docs/dependencies.md)
- TypeScript runtime validation patterns → [docs/typescript.md](docs/typescript.md)
- PR Security Checklist → [#pr-security-checklist](#pr-security-checklist)

## How to use this repo

- Start with the PR Security Checklist below during reviews.
- Use topic files for implementation details and copy-pasteable snippets.
- Keep this aligned with your stack (framework, hosting, proxies).

## PR Security Checklist

Use this checklist in every PR touching network, storage, auth, or rendering.

- [ ] No `innerHTML`/`dangerouslySetInnerHTML` unless sanitized.
- [ ] CSP present and non-inline; Trusted Types enforced on Chromium.
- [ ] Cookies are `HttpOnly; Secure; SameSite=(Lax|Strict)` unless justified.
- [ ] No secrets in client code or public env variables.
- [ ] Dependencies scanned (audit/Snyk); no risky new packages.
- [ ] State-changing requests are non-GET and CSRF-protected.
- [ ] Headers set: HSTS, X-Content-Type-Options, Referrer-Policy, frame-ancestors.
- [ ] Runtime validation present for external data (Zod/io-ts/Valibot).

---

Maintained for 2025 practices: CSP without `unsafe-inline`, Trusted Types on Chromium, HttpOnly cookies for auth, SameSite where possible, runtime validation, and provenance-aware dependencies.

