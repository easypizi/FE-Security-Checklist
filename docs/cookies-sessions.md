# Cookies and Sessions

Use cookies for auth; prefer HttpOnly, Secure, SameSite where viable.

## Do
- Set `HttpOnly; Secure; SameSite=Lax|Strict` for session cookies.
- Bind cookies to domain/path; set short expiries; rotate session IDs.
- Store auth server-side; keep client state minimal.

## Don't
- Store tokens in `localStorage` or expose refresh tokens to JS.
- Use `SameSite=None` without `Secure` and a concrete cross-site need.

## Example: Set cookie (Node/Edge)
```ts
const setAuthCookie = (res: Response, value: string) => {
  res.headers.append('Set-Cookie', [
    `sid=${value}`,
    'Path=/',
    'HttpOnly',
    'Secure',
    'SameSite=Lax',
  ].join('; '));
};
```

## References
- RFC 6265bis (draft): https://datatracker.ietf.org/doc/html/draft-ietf-httpbis-rfc6265bis
- OWASP Session Management: https://owasp.org/www-project-cheat-sheets/cheatsheets/Session_Management_Cheat_Sheet.html
