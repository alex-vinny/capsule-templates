# Vanilla JavaScript — Capsule app

A native mobile app built with **vanilla JavaScript** (no framework, Vite), running inside a
Capsule native shell. Scaffolded with `capsule init my-app --template vanilla-js`.

## Quick start

```bash
pnpm install

# Develop on a connected device/emulator (hot reload; sets up adb reverse for you):
capsule dev android

# Build + install a release-style build (embedded server, no dev server needed):
capsule build android --release
capsule run android --release
```

> Use **`capsule dev android`**, not `pnpm dev` — only the Capsule command runs `adb reverse`,
> without which the device WebView can't reach your machine (`ERR_CONNECTION_REFUSED`).
> (If Capsule is installed as a project dependency, prefix with `pnpm exec`.)

## What's inside

A **Home** tab and a **Server** tab demonstrating both halves of Capsule:

- `src/routes/hello.ts` — a **JSON-RPC route**, called from the UI via `bridge.call('hello', …)`.
- `src/server/routes/ping.ts` — an **HTTP route** served at `GET /api/ping`.

Both run on-device in the embedded QuickJS runtime (prod); in `capsule dev` they're proxied to
a local sidecar. The native APIs (device, haptics, clipboard, storage, …) come from `@capsule/core`.
(Route files are `.ts` even here — they're compiled for the on-device runtime, independent of
your app bundle.)

## Structure

```
index.html            web entry
src/
  main.js             app entry — builds the Home + Server tabs
  routes/hello.ts     JSON-RPC route  (bridge.call)
  server/routes/ping.ts  HTTP route   (GET /api/ping)
vite.config.js        bundler config
```

## Common commands

| Command                             | What                                       |
| ----------------------------------- | ------------------------------------------ |
| `capsule dev android`               | dev server + hot reload on device/emulator |
| `capsule build android [--release]` | build the APK                              |
| `capsule run android [--release]`   | install + launch                           |
| `capsule doctor`                    | check your environment                     |

Edit `src/main.js` to build your UI; add routes by dropping files in `src/routes/` (JSON-RPC)
or `src/server/routes/` (HTTP). See the Capsule documentation for the full `@capsule/core` API.
