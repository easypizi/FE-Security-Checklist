# PR Security Checklist

Use this checklist in every PR touching network, storage, auth, or rendering.

- [ ] No `innerHTML`/`dangerouslySetInnerHTML` unless sanitized.
- [ ] CSP present and non-inline; Trusted Types enforced on Chromium.
- [ ] Cookies are `HttpOnly; Secure; SameSite=(Lax|Strict)` unless justified.
- [ ] No secrets in client code or public env variables.
- [ ] Dependencies scanned (audit/Snyk); no risky new packages.
- [ ] State-changing requests are non-GET and CSRF-protected.
- [ ] Headers set: HSTS, X-Content-Type-Options, Referrer-Policy, frame-ancestors.
- [ ] Runtime validation present for external data (Zod/io-ts/Valibot).

Link to: `../README.md`
