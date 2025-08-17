# Dependencies and Supply Chain Security

Minimize risk from third-party packages and build tools.

## Do
- Run `npm audit` and/or Snyk in CI; track allowlists with expiry.
- Prefer well-maintained deps; pin versions; enable provenance (npm provenance/Sigstore).
- Lock down `postinstall` scripts; use `--ignore-scripts` where possible.
- Use Subresource Integrity (SRI) for CDN scripts and pin exact versions.

## Don't
- Install packages with unknown maintainers for trivial tasks.
- Keep stale lockfiles or floating ranges for critical deps.

## Example: CI step (GitHub Actions)
```yaml
- run: npm ci --ignore-scripts
- run: npm audit --audit-level=high || true
```

## References
- OpenSSF Scorecard: https://securityscorecards.dev/
- npm package provenance: https://docs.npmjs.com/generating-provenance-statements
- Snyk advisories: https://security.snyk.io/
