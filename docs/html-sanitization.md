# HTML Sanitization, XSS, and Trusted Types

Modern XSS prevention combines framework-safe rendering, sanitization, CSP, and Trusted Types.

## Do
- Prefer framework-escaped rendering (React/Next.js) and avoid raw HTML.
- Sanitize any HTML you must render (DOMPurify with restrictive config).
- Enforce CSP without `unsafe-inline`; use nonces or hashes for allowed inline.
- Enable Trusted Types (Chromium) and use a sanitizer policy for `innerHTML`.

## Don't
- Use `dangerouslySetInnerHTML` or `element.innerHTML = ...` without sanitize.
- Allow `script-src 'unsafe-inline'` or `style-src 'unsafe-inline'` in CSP.
- Bypass sanitizer with custom allowlists unless strictly required.

## Example: Safe component (React + DOMPurify)
```tsx
import DOMPurify from 'dompurify';

type Props = { html: string };

export const SafeHtml: React.FC<Props> = ({ html }) => {
  const sanitized = DOMPurify.sanitize(html, { USE_PROFILES: { html: true } });
  return <div dangerouslySetInnerHTML={{ __html: sanitized }} />;
};
```

## Example: Trusted Types header (Next.js middleware)
```ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(req: NextRequest) {
  const res = NextResponse.next();
  res.headers.set('Content-Security-Policy', [
    "default-src 'self'",
    "script-src 'self' 'nonce-__CSP_NONCE__'",
    "object-src 'none'",
    "base-uri 'self'",
    "frame-ancestors 'none'",
    "require-trusted-types-for 'script'",
  ].join('; '));
  res.headers.set('Permissions-Policy', 'camera=(), microphone=()');
  return res;
}
```

## References
- DOMPurify: https://github.com/cure53/DOMPurify
- Trusted Types (Chrome): https://developer.chrome.com/docs/web-platform/trusted-types/
- MDN: CSP: https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP
