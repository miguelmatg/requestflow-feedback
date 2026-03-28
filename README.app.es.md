<p align="center">
  <img src="https://raw.githubusercontent.com/miguelmatg/requestflow-feedback/main/assets/logo.png" alt="RequestFlow Logo" width="128" />
</p>

# RequestFlow

**Tu cliente API que vive dentro de tu proyecto y trabaja con tu agente IA.**

<p align="center">
  <a href="https://marketplace.visualstudio.com/items?itemName=requestflow.requestflow"><img src="https://img.shields.io/visual-studio-marketplace/v/requestflow.requestflow?label=Marketplace" alt="Marketplace Version" /></a>
  <a href="https://marketplace.visualstudio.com/items?itemName=requestflow.requestflow"><img src="https://img.shields.io/visual-studio-marketplace/i/requestflow.requestflow?label=Instalaciones" alt="Marketplace Installs" /></a>
  <a href="https://marketplace.visualstudio.com/items?itemName=requestflow.requestflow"><img src="https://img.shields.io/visual-studio-marketplace/r/requestflow.requestflow?label=Valoraci%C3%B3n" alt="Marketplace Rating" /></a>
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/miguelmatg/requestflow-feedback/main/assets/preview.jpg" alt="RequestFlow Preview" width="800" />
</p>

RequestFlow guarda tus requests HTTP como archivos `.http` nativos en tu repositorio, junto con archivos específicos por protocolo para MQTT/WS. Tu agente de código puede leer esa estructura y generar, actualizar o completar requests automáticamente — sin copiar y pegar, sin herramientas externas.

## README publico (todos los idiomas)

- English: <https://github.com/miguelmatg/requestflow-feedback/blob/main/README.app.md>
- Espanol: <https://github.com/miguelmatg/requestflow-feedback/blob/main/README.app.es.md>

## ¿Por qué RequestFlow?

- **Nativo del proyecto** — tus requests HTTP viven como `.http` y la configuración del workspace en `.requestsflow/`. Versionalo, compártelo, revísalo en PRs.
- **Preparado para LLM** — genera docs estructuradas que tu agente IA lee para entender tus APIs, y después crea o actualiza requests por controlador.
- **Cero cambio de contexto** — envía e inspecciona requests HTTP sin salir de tu editor.
- **Listo para equipos** — comparte colecciones y entornos por control de versiones. Mantén secretos fuera del repo con entornos privados gitignoreados.
- **MQTT integrado** — conéctate a brokers, suscríbete, publica y monitoriza mensajes junto a tu flujo HTTP.
- **WebSocket integrado** — crea conexiones WS, conecta/desconecta, envía payloads y revisa mensajes entrantes/salientes.
- **Funciona donde programas** — VS Code, Cursor, Windsurf y otros IDEs basados en VS Code.

## Funcionalidades

### HTTP

- Gestiona múltiples APIs dentro de `.requestsflow/`.
- Organiza endpoints por carpetas y colecciones.
- Envía requests con `GET`, `POST`, `PUT`, `PATCH`, `DELETE`.
- Configura headers, params, body y auth (`Bearer`, `Basic`, `API Key`).
- Visualiza respuesta: status, headers, body, tiempo, tamaño y exportación cURL.

### Entornos

- Entornos globales y por API con variables reutilizables.
- Interpolación de variables con sintaxis `{{variable}}`.
- Entornos privados (gitignoreados) para secretos y overrides locales.
- Cambia el entorno activo desde la barra de estado.

### MQTT

- Crea y gestiona conexiones a brokers.
- Suscríbete a topics con soporte de wildcards (`+`, `#`).
- Publica mensajes con payloads JSON, XML, YAML o raw.
- Log de mensajes en tiempo real y visualización en árbol de topics.

### WebSocket

- Crea y gestiona conexiones `.ws` en `.requestsflow/_websocket/`.
- Configura URL, headers y mensaje inicial por conexión.
- Conecta, desconecta, envía payloads y visualiza mensajes inbound/outbound/system.
- Filtra y limpia mensajes desde la sesión integrada de WS.

### Integración LLM

- Generación con un clic de docs estructuradas en `.requestsflow/llm/`.
- Tu agente IA lee estas docs para entender la estructura de tu API, convenciones de naming y entornos.
- Prompt sugerido incluido: apúntalo a un controlador y deja que genere todas las requests relacionadas.
- Mantén las docs actualizadas conforme evoluciona tu API — el agente se mantiene sincronizado.

## Requisitos

- VS Code `^1.110.0` (o un IDE compatible basado en VS Code).
- Node.js 20+ y npm para desarrollo local.

## Inicio rápido

1. Abre una carpeta de workspace en tu IDE.
2. Abre **RequestFlow** en la barra lateral.
3. Haz clic en **Inicializar RequestFlow** para crear `.requestsflow/`.
4. Agrega APIs, crea requests y selecciona un entorno.
5. Haz clic en **Generar docs LLM** para que tu agente IA entienda tu proyecto.

## Estructura del proyecto

```plaintext
.requestsflow/
├── environments/
│   └── local.env.json
├── personal-environments/          # privado (gitignoreado)
├── _mqtt/
│   └── mi-broker.mqtt.json
├── llm/                            # generado para agentes IA
│   ├── llm.md
│   ├── http.llm.md
│   ├── mqtt.llm.md
│   ├── ws.llm.md
│   └── environments.llm.md
├── _websocket/
│   └── echo-test.ws
├── <api>/
│   ├── _environments/
│   └── <carpetas>/<request>.http
├── .gitignore
└── settings.json
```

## Licencia

Propietaria — Todos los derechos reservados. La visibilidad pública del código no concede permiso de reutilización, modificación o redistribución. Consulta [LICENSE](./LICENSE).
