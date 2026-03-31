<p align="center">
  <img src="https://raw.githubusercontent.com/miguelmatg/requestflow-feedback/main/assets/logo.png" alt="RequestFlow Logo" width="128" />
</p>

<p align="center">
  <a href="https://marketplace.visualstudio.com/items?itemName=requestflow.requestflow"><img src="https://img.shields.io/visual-studio-marketplace/v/requestflow.requestflow?label=Marketplace" alt="Marketplace Version" /></a>
  <a href="https://marketplace.visualstudio.com/items?itemName=requestflow.requestflow"><img src="https://img.shields.io/visual-studio-marketplace/i/requestflow.requestflow?label=Installs" alt="Marketplace Installs" /></a>
  <a href="https://marketplace.visualstudio.com/items?itemName=requestflow.requestflow"><img src="https://img.shields.io/visual-studio-marketplace/r/requestflow.requestflow?label=Rating" alt="Marketplace Rating" /></a>
</p>
# RequestFlow

**Your API client that lives inside your project and works with your AI agent.**

<p align="center">
  <img src="https://raw.githubusercontent.com/miguelmatg/requestflow-feedback/main/assets/preview.jpg" alt="RequestFlow Preview" width="800" />
</p>

RequestFlow keeps your HTTP requests as native `.http` files in your repository, plus protocol-specific files for MQTT/WS. Your coding agent can read that structure and generate, update, or complete requests automatically — no copy-paste, no external tools.

## Public README (all languages)

- English: <https://github.com/miguelmatg/requestflow-feedback/blob/main/README.app.md>
- Espanol: <https://github.com/miguelmatg/requestflow-feedback/blob/main/README.app.es.md>

## Why RequestFlow?

- **Project-native** — your HTTP requests are plain `.http` files and workspace config lives in `.requestsflow/`. Version it, share it, review it in PRs.
- **LLM-ready** — generate structured docs that your AI agent reads to understand your APIs, then let it create or update requests by controller.
- **Zero context switching** — send and inspect HTTP requests without leaving your editor.
- **Team-ready** — share collections and environments via source control. Keep secrets out of the repo with gitignored private environments.
- **Per-API environments** — assign a different active environment to each API. Team-shared variables with personal secrets that stay local.
- **MQTT built-in** — connect to brokers, subscribe, publish, and monitor messages alongside your HTTP workflow.
- **WebSocket built-in** — create WS connections, connect/disconnect, send payloads, and inspect inbound/outbound messages.
- **Works where you code** — VS Code, Cursor, Windsurf, and other VS Code-based IDEs.

## Key features

### HTTP

- Manage multiple APIs inside `.requestsflow/`.
- Organize endpoints by folders and collections.
- Send requests with `GET`, `POST`, `PUT`, `PATCH`, `DELETE`.
- Configure headers, params, body, and auth (`Bearer`, `Basic`, `API Key`).
- View response: status, headers, body (with collapsible JSON tree view), time, size, and cURL export.
- Always-visible response pane — no context switch when sending requests.

### HTTP compatibility mode (.http/.rest)

- Open and execute requests directly from `.http` and `.rest` files with inline CodeLens.
- Parse multi-request files with `###` blocks and execute by block.
- Use standalone mode for files outside the managed root directory.
- Keep an in-session response history (last 20 executions per request block).
- Optional migration helpers: import REST Client environments and centralize standalone files.

### Environments

- Global, per-API, and personal environments with reusable variables.
- Variable interpolation with `{{variable}}` syntax.
- Per-API environment selection — assign a different active environment to each API with global fallback.
- Private environments (gitignored) for secrets and local overrides — each team member maintains their own.
- File watcher auto-refreshes variables across open tabs when environment files change.
- Switch active environment from the status bar or inline from the request editor.

### MQTT

- Create brokers inline from the MQTT home panel — no multi-step wizard needed.
- Subscribe to topics with wildcard support (`+`, `#`).
- Publish messages with JSON, XML, YAML, or raw payloads.
- Real-time message log with high-contrast bubbles and topic tree visualization.

### WebSocket

- Dedicated WebSocket home panel with connection overview and inline creation.
- Configure URL, headers, and initial message per connection.
- Connect, disconnect, send payloads, and inspect inbound/outbound/system messages.
- Filter and clear messages from the integrated WS session panel.

### LLM Integration

- One-click generation of structured docs in `.requestsflow/llm/`.
- Your AI agent reads these docs to understand your API structure, naming conventions, and environments.
- Suggested prompt included: point it at a controller and let it generate all related requests.
- Docs are auto-generated and auto-maintained — no manual updates needed.

## Requirements

- VS Code `^1.95.0` (or a compatible VS Code-based IDE).
- Node.js 20+ and npm for local development.

## Quick start

1. Open a workspace folder in your IDE.
2. Open **RequestFlow** in the sidebar.
3. Click **Initialize RequestFlow** to create `.requestsflow/`.
4. Add APIs, create requests, and select an environment.
5. Click **Generate LLM docs** to let your AI agent understand your project.

Tip: you can change the managed root with the `requestflow.rootDirectory` setting.

## Multi-root operations guide

- Keep managed HTTP roots explicit with `requestflow.http.managedRoots` so teams and IDEs share the same boundaries.
- Use standalone mode only for discovery and ad-hoc runs; standalone files do not load RequestFlow environments.
- If a standalone request contains `{{variable}}` placeholders, RequestFlow blocks execution until the file is migrated to a managed root.
- Use **RequestFlow: Centralize Standalone Requests** to migrate with `copy` or `move` and review the preview before applying.
- Use **RequestFlow: Undo Last Standalone Centralization** if the latest migration needs rollback.

### Safety and rollback behavior

- RequestFlow stores the latest centralization manifest at `.requestsflow/_migration/last-centralization.json`.
- Undo is conflict-aware and can be partial:
  - `move`: restores files only when target content is unchanged and source does not exist.
  - `copy`: removes generated targets only when content still matches the migration hash.
- When conflicts exist, undo keeps the manifest so users can inspect and resolve remaining files manually.

### Performance best practices

- Keep managed roots under a shared base path when possible to let optimized watcher mode reduce file-system load.
- Prefer fewer high-signal roots over many fragmented roots.
- Keep generated or vendor folders outside managed roots to avoid unnecessary watcher churn.

## Project structure

```plaintext
<requestflow-root>/                   # default: .requestsflow (configurable)
├── environments/
│   └── local.env.json
├── personal-environments/          # private (gitignored)
├── _mqtt/
│   └── my-broker.mqtt.json
├── llm/                            # generated for AI agents
│   ├── llm.md
│   ├── http.llm.md
│   ├── mqtt.llm.md
│   ├── ws.llm.md
│   └── environments.llm.md
├── _websocket/
│   └── echo-test.ws
├── <api>/
│   ├── _environments/
│   └── <folders>/<request>.http
├── .gitignore
└── settings.json
```

## UI patterns (internal)

- Real-time message bubble pattern (MQTT/WS/Kafka/AMQP future): [docs/ui-message-pattern.md](./docs/ui-message-pattern.md)

This guideline is the reference for keeping direction, colors, and bubble composition consistent across all messaging modules.

## Feedback and Issues

Use GitHub Issues to report bugs and propose improvements.

External code contributions and pull requests are currently not accepted.
See [CONTRIBUTING.md](./CONTRIBUTING.md) for the issue reporting policy.

## License

Proprietary — All rights reserved. Public source visibility does not grant permission to reuse, modify, or redistribute. See [LICENSE](./LICENSE).
