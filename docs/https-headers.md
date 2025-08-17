# HTTPS and Security Headers

Deploy HTTPS everywhere and enforce with headers.

## Do
- Enable HSTS: `Strict-Transport-Security: max-age=31536000; includeSubDomains; preload`.
- Configure a strict CSP with nonces or hashes; avoid `unsafe-inline`.
- Set `X-Content-Type-Options: nosniff`, `Referrer-Policy: no-referrer` or strict variant.
- Use `Permissions-Policy` to disable unused capabilities (camera=(), geolocation=()).
- Use `frame-ancestors 'none'` (or `X-Frame-Options: DENY`) to prevent clickjacking.

## Don't
- Allow wildcards for script sources.
- Forget `preload` submission for HSTS if you control apex + subdomains.

## Example: Next.js middleware headers
```ts
import { NextResponse } from 'next/server';

export function middleware() {
  const res = NextResponse.next();
  res.headers.set('Strict-Transport-Security', 'max-age=31536000; includeSubDomains; preload');
  res.headers.set('X-Content-Type-Options', 'nosniff');
  res.headers.set('Referrer-Policy', 'no-referrer');
  res.headers.set('Permissions-Policy', 'camera=(), microphone=(), geolocation=()');
  res.headers.set('X-Frame-Options', 'DENY');
  return res;
}
```

## References
- MDN: HSTS: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security
- MDN: CSP: https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP
- MDN: Permissions-Policy: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Permissions-Policy
- MDN: Referrer-Policy: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy
