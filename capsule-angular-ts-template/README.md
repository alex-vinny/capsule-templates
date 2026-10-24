# Angular + TypeScript — Capsule app

A native mobile app built with **Angular + TypeScript** (Angular CLI), running inside a Capsule
native shell. Scaffolded with `capsule init my-app --template angular-ts`.

## Quick start

```bash
pnpm install

# Develop on a connected device/emulator (hot reload; sets up adb reverse for you):
capsule dev android

# Build + install a release-style build (embedded server, no dev server needed):
capsule build android --release
capsule run android --release
```

> Use **`capsule dev android`**, not `ng serve` — only the Capsule command runs `adb reverse`
> (and generates the proxy config), without which the device WebView can't reach your machine.
> (If Capsule is installed as a project dependency, prefix with `pnpm exec`.)

## What's inside

A **Home** tab and a **Server** tab demonstrating both halves of Capsule:

- `src/routes/hello.ts` — a **JSON-RPC route**, called from the UI via `bridge.call('hello', …)`.
- `src/server/routes/ping.ts` — an **HTTP route** served at `GET /api/ping`.

Both run on-device in the embedded QuickJS runtime (prod); in `capsule dev` they're proxied to
a local sidecar. The native APIs (device, haptics, clipboard, storage, …) come from `@capsule/core`.

## Structure

```
index.html            web entry
angular.json          Angular CLI config (Capsule wraps `ng serve` via --proxy-config)
src/
  main.ts             Angular bootstrap
  app.component.ts    the Home + Server tabs
  routes/hello.ts     JSON-RPC route  (bridge.call)
  server/routes/ping.ts  HTTP route   (GET /api/ping)
```

## Common commands

| Command                             | What                                       |
| ----------------------------------- | ------------------------------------------ |
| `capsule dev android`               | dev server + hot reload on device/emulator |
| `capsule build android [--release]` | build the APK                              |
| `capsule run android [--release]`   | install + launch                           |
| `capsule doctor`                    | check your environment                     |

Edit `src/app.component.ts` to build your UI; add routes by dropping files in `src/routes/`
(JSON-RPC) or `src/server/routes/` (HTTP). See the Capsule documentation for the full
`@capsule/core` API.
