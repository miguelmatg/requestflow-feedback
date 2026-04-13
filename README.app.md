<p align="center">
  <img src="https://raw.githubusercontent.com/miguelmatg/requestflow-feedback/main/assets/logo.png" alt="RequestFlow Logo" width="128" />
</p>

<p align="center">
  <a href="https://marketplace.visualstudio.com/items?itemName=requestflow.requestflow"><img src="https://img.shields.io/visual-studio-marketplace/v/requestflow.requestflow?label=Marketplace" alt="Marketplace Version" /></a>
  <a href="https://marketplace.visualstudio.com/items?itemName=requestflow.requestflow"><img src="https://img.shields.io/visual-studio-marketplace/i/requestflow.requestflow?label=Installs" alt="Marketplace Installs" /></a>
  <a href="https://marketplace.visualstudio.com/items?itemName=requestflow.requestflow"><img src="https://img.shields.io/visual-studio-marketplace/r/requestflow.requestflow?label=Rating" alt="Marketplace Rating" /></a>
</p>
# RequestFlow

**Your project-native API client for VS Code.**

<p align="center">
  <img src="https://raw.githubusercontent.com/miguelmatg/requestflow-feedback/main/assets/preview.jpg" alt="RequestFlow Preview" width="800" />
</p>

RequestFlow keeps your HTTP requests as native `.http` files in your repository. Organize, send, and inspect your requests without leaving your editor — no external tools needed.

## Release status

- v2.2.0 — Environments module re-enabled with a fixed 3-layer variable model (Global, Per-API, Personal).
- MQTT and WebSocket UI are intentionally hidden and return in later phases.

## Public README (all languages)

- English: <https://github.com/miguelmatg/requestflow-feedback/blob/main/README.app.md>
- Espanol: <https://github.com/miguelmatg/requestflow-feedback/blob/main/README.app.es.md>

## Why RequestFlow?

- **Project-native** — each API root stores plain `.http` files inside your repo. Version it, share it, review it in PRs.
- **Zero context switching** — send and inspect HTTP requests without leaving your editor.
- **Team-ready** — share collections via source control and review requests in PRs.
- **Focused UX** — HTTP-only scope for maximum stability and low onboarding friction.
- **Works where you code** — VS Code, Cursor, Windsurf, and other VS Code-based IDEs.

## Key features

### HTTP

- Treat each API as a managed root directory.
- Organize HTTP requests inside `http/` with folders by controller or feature.
- Drag & drop requests and folders to reorganize your collection.
- Multi-select items in the sidebar and delete them in a single action.
- Send requests with `GET`, `POST`, `PUT`, `PATCH`, `DELETE`.
- Configure headers, params, body, and auth (`Bearer`, `Basic`, `API Key`).
- Response viewer with collapsible JSON tree (syntax-colored), formatted XML/HTML with line numbers, and raw view.
- Image preview tab for binary responses (`image/*`) with automatic detection.
- Content-type selector (JSON/XML/HTML/Text/Auto) to control Pretty formatting.
- Status code, response time, size, cookies, and headers displayed in a tabbed layout.
- Collapsible response panel — always visible, no context switch when sending requests.
- cURL export from the Debug tab.

### Environments

- **3-layer variable model**: Global → Per-API → Personal, with automatic resolution based on request location.
- Global and per-API variables stored in `requestflow.config.json`. Personal variables stored in VS Code workspace state (never committed).
- Environment tree view in the sidebar showing all scopes with item counts.
- Table-based environment editor with enable/disable toggles and override hints.
- Rich hover tooltips in `.http` files and the webview URL bar: source badge, resolved value, override info, and Ctrl+Click navigation.
- Click a variable or the API badge to jump directly to the environment editor.
- Status bar button for quick access to environment management.
- Resolver cache auto-invalidates when `requestflow.config.json` changes.

### HTTP compatibility mode (.http/.rest)

- Open and execute requests directly from `.http` and `.rest` files with inline CodeLens.
- Parse multi-request files with `###` blocks and execute by block.
- Use standalone mode for files outside the managed root directory.

### Module roadmap note

- WebSocket returns in v2.3.0.
- MQTT returns in v2.4.0.

## What's next

**v2.3.0 — SSE (Server-Sent Events)**: Stream real-time events over HTTP with connect/disconnect, auto-reconnect, and message log. First extension of the unified multi-protocol tree.

## Requirements

- VS Code `^1.95.0` (or a compatible VS Code-based IDE: Cursor, Windsurf, VSCodium, etc.).

## Quick start

1. Open a workspace folder in your IDE.
2. Open **RequestFlow** in the sidebar.
3. Click **Initialize RequestFlow** to create your first API root.
4. Use the sidebar title actions: **+ API** to add roots, **+ Request** to create requests in the selected API or folder.
5. Open a request from the sidebar tree to edit and send it.
6. Use the **?** icon in the sidebar title to revisit the quick guide.

Tip: each root can be any folder in your workspace — the default is `.requestsflow/`, but you can choose `http`, `src/api`, or any other name.

## Project structure

A root is any folder you choose. You can place `.http` files directly inside it or use subfolders to organize.

Simple repo:

```plaintext
my-project/
├── requestflow.config.json        # API roots + environment variables
└── http/                          # root named "http" (you pick the name)
    ├── users/
    │   ├── list-all.http
    │   └── create.http
    └── orders/
        └── get-by-id.http
```

Monorepo with multiple roots:

```plaintext
my-monorepo/
├── requestflow.config.json        # declares multiple roots + environments
├── src/api/                       # root: "Backend API"
│   └── users/
│       └── list.http
└── apps/payments/http/            # root: "Payments"
    └── orders/
        └── create.http
```

Environment variables in `requestflow.config.json`:

```json
{
  "roots": [...],
  "environments": {
    "global": [
      { "key": "BASE_URL", "value": "https://api.example.com", "enabled": true }
    ],
    "apis": {
      "http": [
        { "key": "API_KEY", "value": "dev-key-123", "enabled": true }
      ]
    }
  }
}
```

Personal variables (secrets, local config) are stored in VS Code workspace state and never appear in version control.

Subfolders inside a root are only for organization. They are not separate APIs.

## Feedback and Issues

Use GitHub Issues to report bugs and propose improvements.

External code contributions and pull requests are currently not accepted.
See [CONTRIBUTING.md](./CONTRIBUTING.md) for the issue reporting policy.

## License

Proprietary — All rights reserved. Public source visibility does not grant permission to reuse, modify, or redistribute. See [LICENSE](./LICENSE).
