# TypeScript Practices for Security

Use types to model intent and runtime validation to enforce it.

## Do
- Treat external input as `unknown` and narrow via schemas.
- Model auth/session types explicitly (e.g., `role: 'user' | 'admin'`).
- Prefer discriminated unions over booleans for permission states.

## Don't
- Use `any` or non-null assertions on untrusted data.
- Encode security-critical logic in types only; enforce at runtime too.

## Example: typed session
```ts
export type UserRole = 'user' | 'admin';
export type Session = { userId: string; role: UserRole };

export const requireAdmin = (session: Session) => {
  if (session.role !== 'admin') throw new Error('Forbidden');
};
```

## References
- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/intro.html
- Zod + TypeScript: https://zod.dev/?id=typescript-inference
