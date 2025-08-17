# Threat Model and Common Risks (2025)

Modern FE apps face both classic web risks and supply-chain issues.

## Do
- Enumerate assets: auth cookies, tokens, PII, internal feature flags.
- Identify entry points: SSR/ISR, API responses, WebSocket, postMessage.
- Prefer defense-in-depth: CSP + Trusted Types + sanitize + runtime validation.
- Use Content-Security-Policy reporting endpoints to observe violations.

## Don't
- Assume your own API is safe; treat it as untrusted input.
- Trust third-party scripts without Subresource Integrity (SRI) and pinning.
- Ignore dependency provenance and maintainer risk.

## Examples
- Add a security section to ADRs describing threats and mitigations.
- Enable CSP report-only in staging first; move to enforce after 1-2 sprints.

## References
- OWASP ASVS: https://owasp.org/ASVS/
- OWASP Top 10: https://owasp.org/www-project-top-ten/
- MDN: CSP: https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP
