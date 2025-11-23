# Frontend – Cannon Ops Console

This package hosts the Next.js application that DevOps teams use to explore Cannon packages, manage staged Safe transactions, and follow the docs/guides. It combines Contentlayer-generated guides, Wagmi/RainbowKit wallet integration, and Cypress-driven quality gates.

## Tech stack

- Next.js 14 (App Router), React 18, TailwindCSS.
- Contentlayer for MDX guides stored under `guides/`.
- Wagmi, RainbowKit, and Safe SDKs for wallet interactions.
- Cypress (E2E + component) and Vitest for automated testing.

## Local development

```sh
npm install
npm run dev
```

The app runs at <http://localhost:3000>. Contentlayer rebuilds automatically on MDX changes.

## Environment variables

Create `.env.local` with the following common options:

| Variable | Description |
| --- | --- |
| `NEXT_PUBLIC_SAFE_BACKEND_URL` | Base URL for the backend service created in `backend/`. |
| `NEXT_PUBLIC_E2E_TESTING_MODE` | Enables mocks for Cypress runs. |
| `NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID` | WalletConnect Project ID for RainbowKit. |
| `SENTRY_DSN` / `SENTRY_AUTH_TOKEN` | Observability (optional). |
| `NEXT_PUBLIC_IPFS_GATEWAY_URL` | Override default IPFS gateway. |

Check `sentry.*.config.ts`, `helpers/*.ts`, and Cypress configs for additional optional vars.

## Useful scripts

| Script | Purpose |
| --- | --- |
| `npm run dev` | Next dev server. |
| `npm run build` | Runs `contentlayer build` + `next build`. |
| `npm run start` | Runs the production server (after `build`). |
| `npm run lint` | ESLint with Next.js config. |
| `npm run test` | Vitest unit suite. |
| `npm run e2e` | Builds, serves, and launches Cypress in interactive mode. |
| `npm run e2e:headless` | CI-friendly headless Cypress run. |

## Testing

- **Unit** – `npm run test`.
- **E2E** – `npm run e2e` (requires backend URL, can use mocks with `NEXT_PUBLIC_E2E_TESTING_MODE=true`).
- **Component** – `npm run component` to debug UI components in isolation.

CI pipelines should run `npm run lint && npm run test && npm run e2e:headless` for full coverage.

## Deployment

- **Vercel** – Recommended; ensure `contentlayer build` runs before `next build`.
- **Static export** – Use `npm run build && npm run start` on any Node 18+ runtime.
- **Observability** – Sentry configs (`sentry.*.config.ts`) are pre-wired; set `SENTRY_DSN`.

During deployment, set `NEXT_PUBLIC_SAFE_BACKEND_URL` to a routable backend endpoint so UI actions (staged txns, search) function.

## Troubleshooting

- MDX not updating – delete `.contentlayer` and restart `npm run dev`.
- Wallet connection failures – confirm `NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID` and RPC provider availability.
- Cypress flakes – run `npm run e2e:local` to skip the build step during investigation.
