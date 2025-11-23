## Security Policy – Frontend

Report UI or client-side vulnerabilities (XSS, CSRF, wallet spoofing, etc.) with reproduction steps and affected routes. Mention “frontend” in the subject to route triage.

### Scope

- `frontend/src/**`, `guides/**`, Cypress tests, and deployment configs
- Production builds served via Vercel, custom hosting, or static exports

### Hardening tips

- Set a strict Content Security Policy and leverage Next.js’ headers configuration.
- Keep dependencies up to date (`npm audit`, `npm outdated`).
- Configure Sentry DSNs carefully to avoid leaking secrets.

Disclosure timeline: acknowledgement within 3 business days, status update within 10 business days, coordinated release afterward.

