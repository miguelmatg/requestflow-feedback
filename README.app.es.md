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

RequestFlow guarda tus requests HTTP como archivos `.http` nativos en tu repositorio. Tu agente de código puede leer esa estructura y generar, actualizar o completar requests automáticamente — sin copiar y pegar, sin herramientas externas.

## Estado del release

- v2.0.0 es una versión enfocada solo en HTTP.
- MQTT, WebSocket y la UI de Entornos están ocultos intencionalmente en esta versión y regresan en fases siguientes.

## README publico (todos los idiomas)

- English: <https://github.com/miguelmatg/requestflow-feedback/blob/main/README.app.md>
- Espanol: <https://github.com/miguelmatg/requestflow-feedback/blob/main/README.app.es.md>

## ¿Por qué RequestFlow?

- **Nativo del proyecto** — cada raíz de API guarda `.http` y su propia estructura de RequestFlow dentro del repo. Versionalo, compártelo y revísalo en PRs.
- **Preparado para LLM** — genera docs estructuradas que tu agente IA lee para entender tus APIs, y después crea o actualiza requests por controlador.
- **Cero cambio de contexto** — envía e inspecciona requests HTTP sin salir de tu editor.
- **Listo para equipos** — comparte colecciones por control de versiones y revisa requests en PRs.
- **UX enfocada** — alcance HTTP-only en v2.0.0 para máxima estabilidad y menor fricción inicial.
- **Funciona donde programas** — VS Code, Cursor, Windsurf y otros IDEs basados en VS Code.

## Funcionalidades

### HTTP

- Trata cada API como una raíz gestionada.
- Organiza requests HTTP dentro de `requests/` con carpetas por controlador o funcionalidad.
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

### Nota de roadmap de modulos

- Entornos vuelve en v2.1.0.
- WebSocket vuelve en v2.3.0.
- MQTT vuelve en v2.4.0.

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
3. Haz clic en **Inicializar RequestFlow** para crear tu primera raíz de API.
4. Agrega raíces de API y crea requests dentro de `requests/`.
5. Envía requests y itera directamente desde el panel HTTP.

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

Ejemplo de repo simple:

```plaintext
<requestflow-root>/                   # por defecto: .requestsflow (configurable)
├── settings.json
├── requests/
│   └── list-all.http
└── .gitignore
```

Ejemplo de monorepo:

```plaintext
.requestsflow/                      # raíz compartida opcional
├── settings.json
└── requests/

apps/payments/.requestsflow/
├── settings.json
├── requests/
│   └── orders/
│       └── create.http
└── .gitignore
```

Las carpetas dentro de `requests/` solo organizan requests. No son APIs.

## Licencia

Propietaria — Todos los derechos reservados. La visibilidad pública del código no concede permiso de reutilización, modificación o redistribución. Consulta [LICENSE](./LICENSE).
