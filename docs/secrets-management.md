# Secrets Management (Client vs Server)

Never ship secrets in client bundles. Route sensitive calls through a server/edge.

## Do
- Keep API keys and tokens server-side (Edge Functions, Workers, server routes).
- Use environment variables only on the server; avoid exposing via public env.
- Proxy third-party calls through your backend if they require credentials.

## Don't
- Embed secrets in JS, `NEXT_PUBLIC_*`, or store in localStorage.
- Rely on obfuscation or source maps removal as a protection.

## Example: Edge proxy (Vercel/Workers-like)
```ts
export const runtime = 'edge';
export async function GET() {
  const apiKey = process.env.SECRET_API_KEY!;
  const r = await fetch('https://api.example.com/data', {
    headers: { Authorization: `Bearer ${apiKey}` },
  });
  return new Response(r.body, { status: r.status });
}
```

## References
- Twelve-Factor App: Config
- Vercel/Cloudflare Workers secrets docs
