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
- **MQTT built-in** — connect to brokers, subscribe, publish, and monitor messages alongside your HTTP workflow.
- **WebSocket built-in** — create WS connections, connect/disconnect, send payloads, and inspect inbound/outbound messages.
- **Works where you code** — VS Code, Cursor, Windsurf, and other VS Code-based IDEs.

## Key features

### HTTP

- Manage multiple APIs inside `.requestsflow/`.
- Organize endpoints by folders and collections.
- Send requests with `GET`, `POST`, `PUT`, `PATCH`, `DELETE`.
- Configure headers, params, body, and auth (`Bearer`, `Basic`, `API Key`).
- View response: status, headers, body, time, size, and cURL export.

### Environments

- Global and per-API environments with reusable variables.
- Variable interpolation with `{{variable}}` syntax.
- Private environments (gitignored) for secrets and local overrides.
- Switch active environment from the status bar.

### MQTT

- Create and manage broker connections.
- Subscribe to topics with wildcard support (`+`, `#`).
- Publish messages with JSON, XML, YAML, or raw payloads.
- Real-time message log and topic tree visualization.

### WebSocket

- Create and manage `.ws` connections under `.requestsflow/_websocket/`.
- Configure URL, headers, and initial message per connection.
- Connect, disconnect, send payloads, and inspect inbound/outbound/system messages.
- Filter and clear messages from the integrated WS session panel.

### LLM Integration

- One-click generation of structured docs in `.requestsflow/llm/`.
- Your AI agent reads these docs to understand your API structure, naming conventions, and environments.
- Suggested prompt included: point it at a controller and let it generate all related requests.
- Keep docs updated as your API evolves — the agent stays in sync.

## Requirements

- VS Code `^1.110.0` (or a compatible VS Code-based IDE).
- Node.js 20+ and npm for local development.

## Quick start

1. Open a workspace folder in your IDE.
2. Open **RequestFlow** in the sidebar.
3. Click **Initialize RequestFlow** to create `.requestsflow/`.
4. Add APIs, create requests, and select an environment.
5. Click **Generate LLM docs** to let your AI agent understand your project.

## Project structure

```plaintext
.requestsflow/
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
