# CSRF Defenses

Prevent cross-site request forgery on state-changing operations.

## Do
- Use SameSite cookies (Lax/Strict) where compatible with your flows.
- For cross-site needs (SSO, embedded flows), use CSRF tokens (double submit or synchronizer pattern).
- Restrict state changes to POST/PUT/PATCH/DELETE and validate origin/referrer.

## Don't
- Perform state changes on GET.
- Rely only on custom headers without verifying cookies.

## Example: Double-submit token (simplified)
```ts
// Server sets csrf cookie and echoes token in body/meta
// Client sends token in header; server verifies cookie === header
```

## References
- OWASP CSRF Prevention: https://owasp.org/www-community/attacks/csrf
- MDN SameSite cookies: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite
