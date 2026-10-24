# Capsule templates

Starter apps for [Capsule](https://github.com/alex-vinny/capsule_framework): a web bundle inside a
generated native Android/iOS shell. `capsule init` downloads one of these folders:

```bash
capsule init my-app --template react-ts
```

| Template           | Stack                           |
| ------------------ | ------------------------------- |
| `vanilla-js`       | Vanilla JavaScript (Vite)       |
| `vanilla-ts`       | Vanilla TypeScript (Vite)       |
| `react-ts`         | React + TypeScript (Vite)       |
| `vue-ts`           | Vue + TypeScript (Vite)         |
| `svelte-ts`        | Svelte + TypeScript (Vite)      |
| `angular-ts`       | Angular + TypeScript (zoneless) |
| `jquery-bootstrap` | jQuery + Bootstrap (Vite)       |

`manifest.json` is the registry the CLI reads; each folder's `README.md` covers that template.
Every template shows both halves of Capsule: a JSON-RPC route (`src/routes/hello.ts`) and an HTTP
route (`src/server/routes/ping.ts`), both running on-device in the embedded QuickJS runtime.

## Adding a template

1. A folder `capsule-<name>-template/` with `package.json` (`"license": "Apache-2.0"`), the app,
   `src/routes/` and `src/server/routes/`, and a `README.md`.
2. An entry in `manifest.json` (`value`, `title`, `dir`), and the same in the CLI's bundled
   fallback list (`packages/cli/src/commands/init.ts` in the framework repo).
3. Check it builds: `pnpm install && pnpm build` in the folder.

Templates change faster than the framework, which is why they live in their own repo. Issues and
security reports go to the [framework repo](https://github.com/alex-vinny/capsule_framework).

## License

[Apache-2.0](LICENSE).
