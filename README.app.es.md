<p align="center">
  <img src="https://raw.githubusercontent.com/miguelmatg/requestflow-feedback/main/assets/logo.png" alt="RequestFlow Logo" width="128" />
</p>

# RequestFlow

**Tu cliente API nativo del proyecto para VS Code.**

<p align="center">
  <a href="https://marketplace.visualstudio.com/items?itemName=requestflow.requestflow"><img src="https://img.shields.io/visual-studio-marketplace/v/requestflow.requestflow?label=Marketplace" alt="Marketplace Version" /></a>
  <a href="https://marketplace.visualstudio.com/items?itemName=requestflow.requestflow"><img src="https://img.shields.io/visual-studio-marketplace/i/requestflow.requestflow?label=Instalaciones" alt="Marketplace Installs" /></a>
  <a href="https://marketplace.visualstudio.com/items?itemName=requestflow.requestflow"><img src="https://img.shields.io/visual-studio-marketplace/r/requestflow.requestflow?label=Valoraci%C3%B3n" alt="Marketplace Rating" /></a>
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/miguelmatg/requestflow-feedback/main/assets/preview.jpg" alt="RequestFlow Preview" width="800" />
</p>

RequestFlow guarda tus requests HTTP como archivos `.http` nativos en tu repositorio. Organiza, envía e inspecciona tus requests sin salir de tu editor — sin herramientas externas.

## Estado del release

- v2.2.0 — Módulo de Entornos re-habilitado con modelo fijo de 3 capas (Global, Por-API, Personal).
- MQTT y WebSocket están ocultos intencionalmente y regresan en fases siguientes.

## README publico (todos los idiomas)

- English: <https://github.com/miguelmatg/requestflow-feedback/blob/main/README.app.md>
- Espanol: <https://github.com/miguelmatg/requestflow-feedback/blob/main/README.app.es.md>

## ¿Por qué RequestFlow?

- **Nativo del proyecto** — cada raíz de API guarda archivos `.http` dentro del repo. Versionalo, compártelo y revísalo en PRs.
- **Cero cambio de contexto** — envía e inspecciona requests HTTP sin salir de tu editor.
- **Listo para equipos** — comparte colecciones por control de versiones y revisa requests en PRs.
- **UX enfocada** — alcance HTTP-only para máxima estabilidad y menor fricción inicial.
- **Funciona donde programas** — VS Code, Cursor, Windsurf y otros IDEs basados en VS Code.

## Funcionalidades

### HTTP

- Trata cada API como una raíz gestionada.
- Organiza requests HTTP dentro de `http/` con carpetas por controlador o funcionalidad.
- Drag & drop para reorganizar requests y carpetas en la colección.
- Multi-selección en el sidebar para eliminar varios elementos a la vez.
- Envía requests con `GET`, `POST`, `PUT`, `PATCH`, `DELETE`.
- Configura headers, params, body y auth (`Bearer`, `Basic`, `API Key`).
- Visor de respuestas con árbol JSON colapsable (con colores de sintaxis), XML/HTML formateado con números de línea y vista raw.
- Pestaña de previsualización para respuestas binarias (`image/*`) con detección automática.
- Selector de content-type (JSON/XML/HTML/Text/Auto) para controlar el formato Pretty.
- Código de estado, tiempo, tamaño, cookies y headers en layout de pestañas.
- Panel de respuesta colapsable — siempre visible, sin cambio de contexto al enviar requests.
- Exportación cURL desde la pestaña Debug.

### Entornos

- **Modelo de 3 capas**: Global → Por-API → Personal, con resolución automática según la ubicación del request.
- Variables globales y por-API almacenadas en `requestflow.config.json`. Variables personales en el estado del workspace de VS Code (nunca se commitean).
- Vista de árbol de entornos en el sidebar mostrando todos los scopes con conteo de elementos.
- Editor de entornos basado en tabla con toggles de activar/desactivar e indicadores de override.
- Tooltips enriquecidos en archivos `.http` y en la barra de URL del webview: badge de origen, valor resuelto, info de override y navegación con Ctrl+Clic.
- Clic en una variable o en el badge de API para saltar directamente al editor de entornos.
- Botón en la barra de estado para acceso rápido a la gestión de entornos.
- La caché del resolver se invalida automáticamente cuando cambia `requestflow.config.json`.

### Modo de compatibilidad HTTP (.http/.rest)

- Abre y ejecuta requests directamente desde archivos `.http` y `.rest` con CodeLens inline.
- Parsea archivos multi-request con bloques `###` y ejecuta por bloque.
- Usa modo standalone para archivos fuera del directorio raíz gestionado.

### Nota de roadmap de modulos

- WebSocket vuelve en v2.3.0.
- MQTT vuelve en v2.4.0.

## Próxima mejora

**v2.3.0 — SSE (Server-Sent Events)**: Streaming de eventos en tiempo real sobre HTTP con connect/disconnect, auto-reconnect y log de mensajes. Primera extensión del árbol unificado multi-protocolo.

## Requisitos

- VS Code `^1.95.0` (o un IDE compatible basado en VS Code: Cursor, Windsurf, VSCodium, etc.).

## Inicio rápido

1. Abre una carpeta de workspace en tu IDE.
2. Abre **RequestFlow** en la barra lateral.
3. Haz clic en **Inicializar RequestFlow** para crear tu primera raíz de API.
4. Usa las acciones del título del sidebar: **+ API** para agregar raíces, **+ Request** para crear requests en la API o carpeta seleccionada.
5. Abre una request desde el árbol del sidebar para editarla y enviarla.
6. Usa el icono **?** en el título del sidebar para revisar la guía rápida.

Tip: cada raíz puede ser cualquier carpeta en tu workspace — el valor por defecto es `.requestsflow/`, pero puedes elegir `http`, `src/api`, o cualquier nombre.

## Estructura del proyecto

Una raíz es cualquier carpeta que tú elijas. Puedes colocar archivos `.http` directamente o usar subcarpetas para organizar.

Repo simple:

```plaintext
my-project/
├── requestflow.config.json        # configuración de raíces de API + variables de entorno
└── http/                          # raíz llamada "http" (tú eliges el nombre)
    ├── users/
    │   ├── list-all.http
    │   └── create.http
    └── orders/
        └── get-by-id.http
```

Monorepo con múltiples raíces:

```plaintext
my-monorepo/
├── requestflow.config.json        # declara múltiples raíces + entornos
├── src/api/                       # raíz: "Backend API"
│   └── users/
│       └── list.http
└── apps/payments/http/            # raíz: "Payments"
    └── orders/
        └── create.http
```

Variables de entorno en `requestflow.config.json`:

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

Las variables personales (secretos, config local) se almacenan en el estado del workspace de VS Code y nunca aparecen en control de versiones.

Las subcarpetas dentro de una raíz solo organizan. No son APIs separadas.

## Licencia

Propietaria — Todos los derechos reservados. La visibilidad pública del código no concede permiso de reutilización, modificación o redistribución. Consulta [LICENSE](./LICENSE).
