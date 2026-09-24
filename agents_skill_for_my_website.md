# AGENTS.md

## Commands
- `npm run dev` — builds first, then `wrangler dev` (API `:8788`) + `vite` (`:5173`) concurrently. Open frontend at `:5173`; Vite proxies `/api` → `:8788`.
- `npm run build` — `vite build` → `./dist`. Rebuild if changes don't appear at `:8788` (wrangler serves static from `dist`).
- `npm run deploy` — active target: Worker (`worker/index.js`) on `2nul.dpdns.org`. `pages:dev` / `pages:deploy` are legacy Pages-Functions flow only.
- No tests, linter, or typecheck configured.

## Env
Please never read environment or secret files such as .env, .dev.vars, or *.vars.

## Architecture
- Vanilla JS + Tailwind 4 via Vite, no framework. Vite inputs: `index.html`, `software.html`, `win-ltsc.html`, `profile.html`.
- Two backends: active **Worker** (`worker/index.js`, `main` in `wrangler.toml`) and legacy **Pages Functions** (`functions/api/`, `functions/profile/`). Both import shared `functions/_lib/{github,session,supabase}.js` — edits there affect both targets.
- Worker flow in `worker/index.js`: `/api/*` → `handleApi()` router; everything else → `assetPathFor()` pretty-URL rewrite (`/software` → `/software.html`, `/profile/:uuid` → `/profile.html`, `/win-ltsc` → `/win-ltsc.html`) served from `dist` via `ASSETS` binding with 404 fallback. `profileRoute` in `vite.config.js` mirrors `/profile/*` → `/profile.html` for `vite` dev only.
- All API responses get `nosniff` / `DENY` / `no-referrer` headers (Worker: `withSecurityHeaders`; Pages: `functions/api/_middleware.js`).

## Backend quirks
- GitHub OAuth in `worker/index.js` + `functions/_lib/github.js`: `gh_state` (CSRF) + `gh_next` cookies; `callback` validates state, exchanges code, upserts to Supabase, signs session.
- Sessions (`functions/_lib/session.js`): stateless HMAC-SHA256 `base64(payload).base64(sig)` in HttpOnly `session` cookie (30d, no expiry in token). Signed with `SESSION_SECRET`.
- Supabase (`functions/_lib/supabase.js`): raw REST on `profiles` table via service-role key, no SDK. Helpers no-op when env missing; `/api/auth/me` reports `meta: ok | supabase-env-missing | profile-row-missing | supabase-error` instead of failing.
- Downloads: `/api/download/:app` requires session, 302s to `APPS` map at top of `worker/index.js` — add apps there. `software.html` gates guest/user views via `/api/auth/me`.

## Frontend quirks
- Each page loads `/src/main.js` (CSS + banner + downloads) and `/src/js/libnav.js` (theme/copy wiring, login `?next=` rewrite, avatar dropdown from `/api/auth/me`). `profile.js` parses uuid from pathname → `/api/profile/:uuid`.
- `public/` copies as-is; banner images live in `/assets/img/` and must also be added to the array in `src/js/banner.js`.
- Styling: Tailwind 4 tokens in `@theme` in `src/css/main.css`; dark mode is class-based (`@custom-variant dark`, `.dark` on `<html>`, dark by default, persisted in `src/js/theme.js`).
- `old_ui/`, `dist/`, `.wrangler/`, `worker.vars` are gitignored — don't edit or depend on them.

### Note
Adhere to the design rules specified in .agents/design.md.
Fast. lol

## Commit message
Write commit messages with a clear type and a comprehensive yet concise description, focusing on the core of the update.
