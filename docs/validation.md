# Input Validation (Runtime Schemas)

TypeScript types erase at runtime; validate all external data.

## Do
- Validate with Zod/Valibot/io-ts on boundaries (network, storage, URL params).
- Treat all external input as `unknown` then narrow via schema.
- Fail closed: reject invalid payloads and surface typed errors.

## Don't
- Trust server responses blindly or cast to `any`.
- Decode JSON and immediately use values without checks.

## Example: safe fetch wrapper (Zod)
```ts
import { z } from 'zod';

export const makeSafeFetch = <T>(schema: z.ZodType<T>) => {
  return async (input: RequestInfo, init?: RequestInit): Promise<T> => {
    const res = await fetch(input, init);
    if (!res.ok) throw new Error(`HTTP ${res.status}`);
    const json = await res.json();
    const parsed = schema.safeParse(json);
    if (!parsed.success) throw new Error('Invalid response');
    return parsed.data;
  };
};
```

## References
- Zod: https://zod.dev/
- TypeScript Handbook (Narrowing): https://www.typescriptlang.org/docs/handbook/2/narrowing.html
