# Manus Service Dependencies and Alternatives

## Overview
This project uses Manus for OAuth-based user authentication and development-time runtime integrations. Manus is primarily used for:

- OAuth login flow via `/api/oauth/callback`
- session management through a `manus-session` cookie
- local browser session fallback via `sessionStorage` for blocked third-party cookies
- Vite runtime plugin support in development

## Manus dependencies in this repo

### NPM packages
- `vite-plugin-manus-runtime` (dev dependency)
  - Injects Manus runtime behavior during Vite development
  - Used in `vite.config.ts`

### Core browser/client integration
- `client/src/const.ts`
  - `startLogin()` builds the Manus OAuth redirect URL using `VITE_OAUTH_PORTAL_URL` and `VITE_APP_ID`
- `client/src/main.tsx`
  - `sessionStorage.getItem("manus-cookie")` fallback for cookies
  - `httpBatchLink` uses `credentials: "include"`
- `client/src/components/ManusDialog.tsx`
  - User-facing login dialog for Manus

### Server integration
- `server/_core/oauth.ts`
  - Registers `/api/oauth/callback`
  - Exchanges OAuth `code` and `state` with Manus via `sdk`
  - Saves a JWT-based session cookie with name `manus-session`
- `server/_core/sdk.ts`
  - Communicates with Manus OAuth services
  - Uses `ENV.oAuthServerUrl` and `ENV.appId`
  - Signs/verifies session tokens via `jose`
- `server/_core/trpc.ts` and `server/_core/context.ts`
  - Uses authenticated user context provided by Manus session verification

## Required configuration
The app expects these environment variables for Manus OAuth and session management:

- `VITE_OAUTH_PORTAL_URL`
  - Browser-side Manus auth portal URL used by `startLogin()` in `client/src/const.ts`
- `VITE_APP_ID`
  - Manus application identifier used in OAuth requests
- `OAUTH_SERVER_URL`
  - Server-side Manus API base URL used in `server/_core/sdk.ts`
- `COOKIE_SECRET`
  - Secret used to sign session JWTs in `server/_core/sdk.ts`

## How the flow works
1. User clicks login UI and `startLogin()` is called.
2. `startLogin()` writes an one-time `__Host-oauth-state` nonce cookie and redirects to Manus `app-auth` URL.
3. Manus redirects back to `/api/oauth/callback` with `code` and `state`.
4. Server validates `state` against cookie, exchanges the code for a token, and retrieves user info from Manus.
5. Server stores/updates the user and issues the `manus-session` JWT cookie.
6. Subsequent TRPC requests use `credentials: include` and can also fallback to `sessionStorage` when cookies are blocked.

## Existing Manus runtime alternatives
If Manus is unavailable or you want a simpler auth integration, these are viable alternatives:

### 1. Local JWT auth / custom OAuth
- Replace `startLogin()` and `/api/oauth/callback` with a local auth form or alternative OAuth provider
- Keep the same cookie/session patterns in `server/_core/sdk.ts`
- Useful if you already have Google, Microsoft, or internal SSO

### 2. Auth0 / Clerk / Firebase Auth
- Use a hosted provider for authentication and session management
- Map provider user IDs to `openId` or local user records in `server/db.ts`
- Benefits: built-in MFA, identity management, and reusable user sessions

### 3. Email/password auth with JWTs
- Implement a `/login` endpoint and session cookie handling directly
- Keep `protectedProcedure`/`protectedStoreProcedure` middleware but replace Manus session verification
- May be preferable for small internal apps with no external OAuth dependency

### 4. Browser-only session storage / local dev auth stub
- For local development, stub `useAuth()` to return a mocked user instead of Manus
- Useful to decouple frontend work from backend OAuth until the integration is ready

## Recommended migration path
1. Create a replacement auth provider module for `server/_core/sdk.ts`.
2. Keep `server/_core/oauth.ts` only if you still need OAuth callback logic.
3. Replace `client/src/const.ts` `startLogin()` with a login URL or redirect for the new provider.
4. Remove `vite-plugin-manus-runtime` from `vite.config.ts` if not using Manus dev runtime.
5. Keep `sessionStorage` fallback only when needed for third-party cookie scenarios.

## Notes
- This repo currently relies on Manus as the default auth provider.
- Manus-specific UI is isolated to `ManusDialog` and `client/src/const.ts`.
- Server session code is centralized in `server/_core/sdk.ts`.

If you want, I can also add a small `AUTH_ALTERNATIVES.md` file listing a concrete replacement plan for this app.