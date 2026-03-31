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
- **Entornos por API** — asigna un entorno activo diferente a cada API. Variables compartidas de equipo con secretos personales que quedan locales.
- **MQTT integrado** — conéctate a brokers, suscríbete, publica y monitoriza mensajes junto a tu flujo HTTP.
- **WebSocket integrado** — crea conexiones WS, conecta/desconecta, envía payloads y revisa mensajes entrantes/salientes.
- **Funciona donde programas** — VS Code, Cursor, Windsurf y otros IDEs basados en VS Code.

## Funcionalidades

### HTTP

- Gestiona múltiples APIs dentro de `.requestsflow/`.
- Organiza endpoints por carpetas y colecciones.
- Envía requests con `GET`, `POST`, `PUT`, `PATCH`, `DELETE`.
- Configura headers, params, body y auth (`Bearer`, `Basic`, `API Key`).
- Visualiza respuesta: status, headers, body (con vista de árbol JSON colapsable), tiempo, tamaño y exportación cURL.
- Panel de respuesta siempre visible — sin cambio de contexto al enviar requests.

### Modo de compatibilidad HTTP (.http/.rest)

- Abre y ejecuta requests directamente desde archivos `.http` y `.rest` con CodeLens inline.
- Parsea archivos multi-request con bloques `###` y ejecuta por bloque.
- Usa modo standalone para archivos fuera del directorio raíz gestionado.
- Conserva historial de respuestas en sesión (últimas 20 ejecuciones por bloque).
- Incluye ayudas de migración: importar entornos de REST Client y centralizar archivos standalone.

### Entornos

- Entornos globales, por API y personales con variables reutilizables.
- Interpolación de variables con sintaxis `{{variable}}`.
- Selección de entorno por API — asigna un entorno activo diferente a cada API con fallback global.
- Entornos privados (gitignoreados) para secretos y overrides locales — cada miembro del equipo mantiene el suyo.
- File watcher auto-refresca variables en pestañas abiertas cuando cambian los archivos de entorno.
- Cambia el entorno activo desde la barra de estado o inline desde el editor de requests.

### MQTT

- Crea brokers inline desde el panel MQTT — sin wizard multi-paso.
- Suscríbete a topics con soporte de wildcards (`+`, `#`).
- Publica mensajes con payloads JSON, XML, YAML o raw.
- Log de mensajes en tiempo real con burbujas de alto contraste y visualización en árbol de topics.

### WebSocket

- Panel WebSocket dedicado con vista general de conexiones y creación inline.
- Configura URL, headers y mensaje inicial por conexión.
- Conecta, desconecta, envía payloads y visualiza mensajes inbound/outbound/system.
- Filtra y limpia mensajes desde la sesión integrada de WS.

### Integración LLM

- Generación con un clic de docs estructuradas en `.requestsflow/llm/`.
- Tu agente IA lee estas docs para entender la estructura de tu API, convenciones de naming y entornos.
- Prompt sugerido incluido: apúntalo a un controlador y deja que genere todas las requests relacionadas.
- Las docs se auto-generan y auto-mantienen — sin actualizaciones manuales.

## Requisitos

- VS Code `^1.95.0` (o un IDE compatible basado en VS Code).
- Node.js 20+ y npm para desarrollo local.

## Inicio rápido

1. Abre una carpeta de workspace en tu IDE.
2. Abre **RequestFlow** en la barra lateral.
3. Haz clic en **Inicializar RequestFlow** para crear `.requestsflow/`.
4. Agrega APIs, crea requests y selecciona un entorno.
5. Haz clic en **Generar docs LLM** para que tu agente IA entienda tu proyecto.

Tip: puedes cambiar la raíz gestionada con la configuración `requestflow.rootDirectory`.

## Guía operativa multi-root

- Mantén raíces HTTP gestionadas explícitas con `requestflow.http.managedRoots` para compartir límites consistentes entre equipos e IDEs.
- Usa standalone solo para descubrimiento y ejecución puntual; los archivos standalone no cargan entornos de RequestFlow.
- Si una request standalone contiene placeholders `{{variable}}`, RequestFlow bloquea la ejecución hasta migrarla a una raíz gestionada.
- Usa **RequestFlow: Centralizar Standalone Requests** para migrar con `copy` o `move` y revisar el preview antes de aplicar.
- Usa **RequestFlow: Undo Last Standalone Centralization** para deshacer la última centralización.

### Seguridad y comportamiento de rollback

- RequestFlow persiste el manifiesto de la última centralización en `.requestsflow/_migration/last-centralization.json`.
- El undo detecta conflictos y puede ser parcial:
  - `move`: restaura solo si el target no cambió y el source no existe.
  - `copy`: elimina targets generados solo si el contenido coincide con el hash original.
- Si hay conflictos, el manifiesto se conserva para inspección y resolución manual.

### Buenas prácticas de rendimiento

- Agrupa roots gestionados bajo una base común cuando sea posible para reducir coste de watchers en modo optimizado.
- Prefiere pocas raíces bien definidas en lugar de muchas raíces fragmentadas.
- Mantén carpetas generadas o de terceros fuera de los roots gestionados para evitar refrescos innecesarios.

## Estructura del proyecto

```plaintext
<requestflow-root>/                   # por defecto: .requestsflow (configurable)
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
