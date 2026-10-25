# UI YAIWES

Fuente única de **UI YAIWES** y **UI YAIWES interface** (decisión del Director, Antonio). Antes vivían repartidas entre `maxbry123-commits/frontend` ("fromtend") y copias dentro del repo del router; este repo es la referencia.

## Resumen

1. **UI YAIWES es un sistema operativo de interfaz con triggers (disparadores)**: gestiona ventanas, pantallas, llamadas, permisos y reacciona a eventos. No es un agente ni un sistema de memoria.
2. Conviven **dos sistemas separados**: el **Sistema 2** (UI YAIWES, controla el chat) y el **Sistema 1** (memoria, almacenamiento y gobierno de agentes, aparte). Ambos hablan solo por acciones y eventos.
3. UI YAIWES **pide y muestra**; el Sistema 1 **decide, guarda y responde**. La verdad (estado, memoria, auditoría) vive fuera de la UI.
4. Un **trigger** es una regla declarativa `evento -> condición -> acción de interfaz`. Solo cambia la pantalla; nunca ejecuta trabajo de agentes ni escribe memoria. Sin evento válido no hay efecto (fail-closed).
5. Los componentes reales ya existen como piezas de SO (host, slots, action bus, manifiestos, clave de acceso, conectores, `postMessage`); ver el mapa de la sección 4.
6. Lo que **ya existe** en código está separado de lo que es **PROPUESTA**: el motor de triggers y los eventos del Sistema 1 aún no existen.
7. Estado del backend que necesita la UI: **33 % (estimación, no medición)**; el kernel que la UI espera es el Sistema 1.
8. Quedan **39 ventanas** y la fábrica F0–F12 (F0–F3 hechas); ninguna ventana tiene todavía "OK por ID del director".
9. Los documentos anteriores que describen otra cosa (IA local WebGPU, "Local Router") **se conservan sin tocar** como referencia; ver sección 11.
10. Dos fallos conocidos del frontend esperan autorización para corregirse (sección 12). Del repo `frontend` faltan 743.244 archivos, casi todos de terceros o de volumen (sección 13).

## Índice

1. [Qué es y qué NO es](#1-qué-es-y-qué-no-es)
2. [Los dos sistemas](#2-los-dos-sistemas)
3. [Estructura real del repo](#3-estructura-real-del-repo)
4. [Mapa sistema operativo -> componentes reales](#4-mapa-sistema-operativo---componentes-reales)
5. [Triggers](#5-triggers)
6. [Contrato con el Sistema 1 y estado del backend](#6-contrato-con-el-sistema-1-y-estado-del-backend)
7. [Las 39 ventanas](#7-las-39-ventanas)
8. [Fábrica DAG F0–F12](#8-fábrica-dag-f0f12)
9. [Cómo se sirve desde el chat](#9-cómo-se-sirve-desde-el-chat)
10. [Reglas](#10-reglas)
11. [Conciliación con documentos anteriores](#11-conciliación-con-documentos-anteriores)
12. [Fallos conocidos y observaciones](#12-fallos-conocidos-y-observaciones)
13. [Material movido y material que sigue fuera](#13-material-movido-y-material-que-sigue-fuera)

Convención de rutas: `§/` = `UI YAIWES/UI YAIWES interface/code/UI YAIWES interface/`.

## 1. Qué es y qué NO es

**Es** el sistema operativo de la interfaz del chat: un shell de ventanas (cada ventana es un HTML aislado), con un bus de acciones, un registro de aplicaciones/ventanas, sesión y permisos, drivers de conexión y un bus de eventos (triggers) que reacciona a lo que el Sistema 1 informa.

**No es**:
- un agente: no razona ni elige;
- un sistema de memoria: no guarda conocimiento, historial verdadero ni auditoría;
- un decisor: no aprueba, no enruta modelos, no planifica;
- un portador de secretos: no lleva tokens (los conectores externos solo los abre el kernel);
- un lanzador de trabajo: no arranca tareas por su cuenta; solo envía acciones que el usuario pidió y muestra los eventos que llegan.

Hoy el navegador guarda solo caché y preferencias de interfaz (ver observación 3 de la sección 12).

## 2. Los dos sistemas

```
SISTEMA 2 · UI YAIWES (sistema operativo de interfaz, con triggers)
  ventanas · slots · action bus · manifiestos · sesión · conectores · triggers
  guarda SOLO preferencias/caché de interfaz (localStorage) — nunca la verdad
        │  acciones (ABS/ActionBus) ↓          ↑  eventos (run.* / memory.* / audit.* ...)
        │  HTTP autenticado, sin tokens en la ventana
SISTEMA 1 · MEMORIA Y ALMACENAMIENTO / GOBIERNO DE AGENTES (aparte)
  estado · memoria · almacenamiento · auditoría · recursos · agentes
  única fuente de verdad
```

Son dos "sistemas operativos" distintos y no deben confundirse: el de **interfaz** (este repo) y el de **memoria y agentes** (documentado en el router, carpeta chat-router/memoria/arquitectura). Los agentes hablan solo con el Sistema 1, nunca con la UI. El contrato completo está en https://github.com/maxbry123-commits/router-universal-router-inteligente-/blob/main/chat-router/memoria/README-DOS-SISTEMAS-DE-MEMORIA.md

## 3. Estructura real del repo

```
README.md
UI YAIWES/
└── UI YAIWES interface/
    ├── DOWNLOAD_EXTRACT_MANIFEST.json
    ├── _archives/            bundle .zip en partes (UI YAIWES interface.bundle.zip.part-NNNN)
    └── code/UI YAIWES interface/                       (§/)
        ├── Ui Yaiwes interface beta/   01-original (HTML del director, INVENTARIO-39.json),
        │                               02-fromted (las 39 ventanas + HOST.html + FICHAS + INDEX.json),
        │                               04-panels/PANEL-01-CHAT
        ├── fabrica-ui/                 fábrica DAG (PLAN-DAG-DETERMINISTA.json, bitacora-fabrica),
        │                               runtime (ABS.js, security.js, connectors.js, lote-01-nucleo-host 01..10)
        ├── Fromtend/                   modules/M_RUNTIME_ORCHESTRATION, project-memory (mapas T2-R1..R5)
        ├── Backend/                    Motor3 approved donors (OSS aprobado), project-memory
        ├── empaque/  seguridad/  qa/   PWA/Capacitor/Tauri stubs, CSP, pruebas Playwright
        ├── workflow/  skills/          contrato, DAG y DSL del frontend; skills de implementación y QA
        ├── readme arquitectura UI YAIWES interface beta/   documentos de arquitectura vigentes
        ├── frontend-repo-UI-YAIWES/    movido desde el repo frontend, carpeta "UI YAIWES" (T1 y P1)
        ├── frontend-repo-raiz/         movido desde la raíz del repo frontend (P1)
        ├── host-router-yaiwes/         variantes de host traídas del router (T1)
        ├── REGISTRO-MOVIDOS-T1.md  REGISTRO-MOVIDOS-P1.md   registros de lo movido
        └── *.md / LOOP-SCHEMA.json     contratos y guías (AGENTS, ACCEPTANCE, DESIGN_SYSTEM, SKILL, ...)
```

## 4. Mapa sistema operativo -> componentes reales

Todos verificados en el código. "Estado hoy" indica lo que hace realmente.

| Concepto de SO | Componente UI YAIWES | Ruta | Estado hoy |
|---|---|---|---|
| Gestor de ventanas | Host: un iframe por ventana; chrome de ventana | `§/Ui Yaiwes interface beta/02-fromted/HOST.html`, `§/fabrica-ui/runtime/lote-01-nucleo-host/08-chrome-window.js` | HOST.html carga las 39 y registra los mensajes; el lote-01 pinta chrome y botones |
| Servidor de pantalla | SlotRegistry (slots `toolbar`, `group`, `body`, `footer`, `qat`) | `§/fabrica-ui/runtime/lote-01-nucleo-host/02-slot-registry.js` | Slot desconocido devuelve `null`: no se pinta (fail-closed) |
| Llamadas al sistema (syscalls) | ActionBus (lado host) y ABS (lado ventana) | `§/fabrica-ui/runtime/lote-01-nucleo-host/03-action-bus.js`, `§/fabrica-ui/runtime/ABS.js` | ActionBus: acción no registrada devuelve `action_missing`; error del handler devuelve `handler_throw`. ABS: ver fallo 2 |
| Registro de aplicaciones/ventanas | `validateManifest` + ManifestStore; índice de las 39 | `§/fabrica-ui/runtime/lote-01-nucleo-host/04-manifest-schema.js`, `§/fabrica-ui/runtime/lote-01-nucleo-host/05-manifest-store.js`, `§/Ui Yaiwes interface beta/02-fromted/INDEX.json` | Manifiesto inválido: REJECT. Se guarda en localStorage (clave `yaiwes.biblioteca.manifests.v1`) con exportación JSON |
| Sesión y permisos | AccessKey (compara hash de clave; si no coincide queda `locked`) y panel de configuración | `§/fabrica-ui/runtime/lote-01-nucleo-host/06-access-key.js`, `§/fabrica-ui/runtime/lote-01-nucleo-host/09-config-panel.js` | Protege solo el panel de configuración, no al usuario final |
| Drivers | `FROMTED_IO`: `local`, `web`, `github`, `huggingface`, `gdrive`, `database` | `§/fabrica-ui/runtime/connectors.js` | Solo `local` y `web` responden; los otros cuatro devuelven `KERNEL_ONLY` (los abre el kernel, la ventana no lleva token) |
| Aislamiento y CSP | Política CSP y reglas de seguridad | `§/seguridad/csp.json`, `§/seguridad/README.md` | CSP declarada (`default-src 'self'`; `script-src` permite `'unsafe-inline'`). `§/fabrica-ui/runtime/security.js` NO es CSP: cifra con AES-GCM/PBKDF2 los `wire.json` (fábrica F8 pendiente) |
| Comunicación entre procesos (IPC) | `postMessage` ventana -> host, mensaje `FROMTED_ABS` | `§/fabrica-ui/runtime/ABS.js`, `§/Ui Yaiwes interface beta/02-fromted/HOST.html` | El host solo muestra el mensaje en un log; no actúa |
| Shell / escritorio | PANEL-01 (chat), selectores de modelo/equipo/modo | `§/Ui Yaiwes interface beta/04-panels/PANEL-01-CHAT/index.html` | Funciona; envía `send_message` al Harness por el puente |
| Núcleo (kernel) | **Fuera de este repo**: Sistema 1 / Harness `puente_chat` | `§/host-router-yaiwes/chat/frontend/yaiwes/puente-yaiwes.js` (solo el puente) | El kernel completo no existe todavía |
| Bus de eventos / triggers | **No existe** | ver sección 5 | PROPUESTA |

Corrección de lectura: `security.js` no es el aislamiento; el aislamiento está en `seguridad/` (CSP; iframe sandbox para código interno según `§/seguridad/README.md`, aún sin aplicar en `HOST.html`, cuyo iframe no declara `sandbox`).

## 5. Triggers

### 5.1 Definición y reglas

Un trigger es una regla declarativa que une un **evento del Sistema 1** con una **acción de interfaz**. Reglas (todas obligatorias):

1. El trigger **solo cambia la interfaz** (abrir, enfocar o refrescar una ventana, insignia, barra, estado visual, aviso).
2. **Nunca ejecuta trabajo de agentes ni escribe memoria**; si necesita datos, los pide con una acción de lectura al Sistema 1 (por ejemplo `memory.context`).
3. Los eventos **vienen del Sistema 1** por HTTP autenticado; la UI no los inventa ni los reenvía a otros.
4. **Sin evento válido no hay efecto (fail-closed)**: un evento sin esquema reconocido, de otro proyecto o sesión, repetido (mismo `event_id`) o sin ventana destino registrada en el SlotRegistry se descarta y se registra.
5. El catálogo de acciones de interfaz es **cerrado** (sección 5.3); un trigger no puede invocar una acción fuera de él.
6. Un trigger no abre ventanas fuera de las 39 ni de los manifiestos registrados.

Nota de vocabulario: `§/EXECUTION-CONTRACT.md` usa "trigger" para el control que dispara el usuario (`trigger -> handler -> state/action -> visible_feedback -> deterministic_result`). Aquí "trigger" es el disparador por evento externo; ambos pueden convivir y el segundo reutiliza el primero.

### 5.2 Lo que YA existe en el código

| Mecanismo | Ruta | Qué hace hoy |
|---|---|---|
| Evento DOM `FROMTED_<id>` al despachar en ABS | `§/fabrica-ui/runtime/ABS.js` | Una ventana emite un evento local tras cada acción |
| Mensaje `FROMTED_ABS` ventana -> host | `§/Ui Yaiwes interface beta/02-fromted/HOST.html` | El host lo recibe y lo escribe en un log |
| Eventos obligatorios del panel de chat: `action.accepted`, `run.started`, `run.delta`, `run.completed`, `run.failed`, `run.cancelled` | `§/Ui Yaiwes interface beta/04-panels/PANEL-01-CHAT/src/panel-01-chat.manifest.json` | Solo **declarados** en `backendBoundary` (`failClosed: true`); nada los consume |
| Registro local de eventos del panel (últimos 12) | `§/Ui Yaiwes interface beta/04-panels/PANEL-01-CHAT/src/panel-01-chat.js` | Bitácora visual propia del panel, no eventos del Sistema 1 |
| Respuesta síncrona de `send_message` | `§/host-router-yaiwes/chat/frontend/yaiwes/puente-yaiwes.js` | Único viaje real de ida y vuelta: acción al Harness y `reply` de vuelta |
| Flujo `CONTROL -> actionId -> ACTION BUS -> BRIDGE/PLUGIN -> BACKEND (frontera) -> EVENTO -> STATESTORE -> UI` | `§/readme arquitectura UI YAIWES interface beta/ARQUITECTURA-FRONTEND-UI-YAIWES-V1.md` | Documentado; el `StateStore` como pieza propia no está en el runtime |

### 5.3 PROPUESTA: tabla declarativa evento -> condición -> acción

Nada de esto está implementado. Formato sugerido de regla (datos, no código): `{id, on, when, do, target}`. El motor sería una pieza nueva del núcleo que valida el evento y llama al ActionBus ya existente (fail-closed por `action_missing`).

Catálogo cerrado de acciones de interfaz (PROPUESTA): `ui.window.open`, `ui.window.focus`, `ui.window.refresh`, `ui.badge.set`, `ui.badge.clear`, `ui.progress.set`, `ui.state.set`, `ui.notice.show`.

| ID | Evento (Sistema 1) | Condición | Acción de interfaz | Destino |
|---|---|---|---|---|
| TR-01 | `action.accepted` | `run_id` pertenece a la sesión | `ui.state.set` = aceptada | PANEL-01 |
| TR-02 | `run.started` | `run_id` del chat activo | `ui.state.set` = running y habilitar `cancel_run` | PANEL-01 |
| TR-03 | `run.delta` | `run_id` activo y `seq` mayor que el último | `ui.state.set` (texto parcial) | PANEL-01 |
| TR-04 | `run.completed` | `run_id` conocido | `ui.window.refresh` si está abierta, si no `ui.badge.set`; estado done | RUN-01 Cascade, PANEL-01 |
| TR-05 | `run.failed` / `run.cancelled` | `run_id` conocido | `ui.state.set` = failed/cancelled y `ui.notice.show` con el motivo | PANEL-01 |
| TR-06 | `audit.conflict` | proyecto de la sesión | `ui.window.open` con el conflicto resaltado | RUN-03 Auditor |
| TR-07 | `watchdog.alert` | proyecto de la sesión | `ui.badge.set` (rojo) | RUN-05 Orquesta |
| TR-08 | `memory.updated` | `memory_version` mayor que la mostrada | `ui.window.refresh`; la ventana relee con `memory.context` | FOTO-01, FOTO-07, FOTO-10 |
| TR-09 | `storage.progress` | `job_id` en curso | `ui.progress.set` | FOTO-09 |
| TR-10 | `task.*` | tarea del plan visible | `ui.window.refresh` | RUN-02 Tren |

Prerrequisitos que hoy faltan: un canal de eventos desde el Harness (hoy solo hay sondeo por `proceso_id`), identificadores `event_id` y `seq`, y reconexión con `since=seq`.

## 6. Contrato con el Sistema 1 y estado del backend

Los 11 módulos de producto salen de `T2-R1-WINDOW-CAPABILITY-MAP` (mapas en `§/Fromtend/project-memory`). El enlace a servicios (S1 Estado, S2 Memoria, S3 Recuperación, S4 Almacenamiento, S5 Auditor, S6 Recursos, S7 Gobierno de agentes) y las acciones y eventos son **PROPUESTA**, definida en el README del router citado en la sección 2.

| Módulo (vista) | Servicio del Sistema 1 | Acciones -> eventos |
|---|---|---|
| M_AGENT_CHAT_SHELL (PANEL-01, GBOT-01) | S7 + Router | `send_message`, `cancel_run` -> `run.started/delta/completed/failed/cancelled` |
| M_KNOWLEDGE_MEMORY_CONTEXT (FOTO-01/07/10) | S2 + S3 | `memory.context`, `memory.search`, `memory.anchor.set` -> `memory.updated` |
| M_GIT_VERSION_TIMELINE (FOTO-03/12) | S1 | `state.history`, `state.rollback` (con autorización) |
| M_STORAGE (FOTO-09) | S4 | `storage.list`, `storage.pull` -> `storage.progress` |
| M_EVIDENCE_AUDIT (RUN-03, FOTO-14) | S5 | `audit.run`, `audit.resolve` -> `audit.conflict` |
| M_ASSETS_SKILLS_MODELS (FOTO-04/05/11) | S4 + S6 | `resource.status`, `dataset.get`, `adapter.get` |
| M_RUNTIME_ORCHESTRATION (RUN-01/02/04/05/07/08) | S7 | `plan.approve`, `task.run`, `task.cancel` -> `task.*`, `watchdog.alert` |
| M_TERMINAL_SANDBOX (RUN-06, FOTO-02) | S7 sandbox | `sandbox.exec` (solo con permiso temporal) |
| M_WORKSPACE_FILES_BLOCKS (WALL-01..16) | S1 + S2 | `sheet.get`, `sheet.delta` |
| M_LAYERS_COMPOSITION (FOTO-08) | S2 + S4 | `memory.layers` |
| M_PERSONALITY_SETTINGS (FOTO-13) | S2 + S7 | `profile.get/set` (escritura por el Sistema 1) |

Las **acciones** salen de la UI y los **eventos** llegan del Sistema 1; los triggers de la sección 5.3 consumen los eventos de esta tabla. La escritura de memoria es solo del Sistema 1; la UI no escribe.

**Estado real del backend: 33 % (ESTIMACIÓN, no medición).** Informe de avance del 25-oct-2026: los 11 módulos pesan igual (9,1 %) y se puntúan de 0 a 1 según lo que existe en el backend del router; total 3,65 de 11. Otros indicadores del mismo informe: conectores 4 de 6 (faltan `gdrive` y `database`); eventos de PANEL-01 deducibles 2 de 6; fábrica de la UI 4 de 13 (31 %); en vivo solo se comprobó `/health` del Space, nada de las ventanas contra el backend real. Casi todo lo que falta es el Sistema 1.

## 7. Las 39 ventanas

Definidas en `§/Ui Yaiwes interface beta/02-fromted/INDEX.json` (n = 39, cada una con ficha en FICHAS y sha12):

| Grupo | IDs | Qué son |
|---|---|---|
| RUN | RUN-01..08 | Cascade, Tren, Auditor, Ventanas V-01..V-04, Orquesta, panel Sandbox, panel Código YAML, panel nodo/input/out |
| WALL | WALL-01..16 | Crazy Wall: bloques, árbol, archivos, modos preguntar/tap, 6 raíces, hojas, guardar/compartir, bitácora state.json |
| GBOT | GBOT-01 | Cáscara Grok Bot (sin source oficial) |
| FOTO | FOTO-01..14 | Referencias de pantallas (grafo de conocimiento, versionado, assets, skills, capas, almacenamiento, contexto, modelos, timeline, personalidad, evidencia) |

En el modelo de SO son **vistas** (aplicaciones sin lógica propia): muestran lo que el Sistema 1 informa. **Estado:** las 39 están partidas, con ficha y copiadas a 02-fromted (fábrica F0–F3). **Ninguna tiene aún "OK por ID del director"** (F11) ni validación de las 39 (F10).

## 8. Fábrica DAG F0–F12

Fuente: `§/fabrica-ui/PLAN-DAG-DETERMINISTA.json` y `§/fabrica-ui/bitacora-fabrica/state.json`.

| Nodo | Paso | Estado |
|---|---|---|
| F0 | Inventario 39 + hashes | hecho |
| F1 | Copiar lote-01 a runtime fábrica | hecho |
| F2 | ABS + security + connectors | hecho |
| F3 | HOST iframe | hecho |
| F4 | PWA empaque web zip | pendiente |
| F5 | Tauri Linux/Windows | pendiente |
| F6 | Capacitor Android/iOS | pendiente |
| F7 | Conector elegido por el usuario | pendiente |
| F8 | Cifrar wires | pendiente |
| F9 | Quitar Factory del producto | pendiente |
| F10 | Acción que valida las 39 | pendiente |
| F11 | OK por ID del director | pendiente |
| F12 | Lock de 03-producto | pendiente |

## 9. Cómo se sirve desde el chat

El chat del router (Vercel) sirve esta interfaz en la ruta **/yaiwes** (carpeta chat/frontend/yaiwes del router, protegida por su guardia de cableado). El **puente `puente-yaiwes.js`** conecta el panel PANEL-01 con el Harness `puente_chat` por HTTP (misma ruta que usa `api.js`): COMPONENTE -> HARNESS -> HTTP -> FICHA -> MODELO. Las variantes de host del router están copiadas en `§/host-router-yaiwes`.

## 10. Reglas

- **Fail-closed:** toda acción sin backend debe fallar, nunca fingir éxito (`failClosed: true` en el manifiesto); todo trigger sin evento válido no produce efecto.
- **Sin tokens en las ventanas:** los conectores `github`, `huggingface`, `gdrive` y `database` responden `KERNEL_ONLY`; los abre el kernel.
- **Kernel externo:** la UI no decide ni guarda la verdad; en el navegador solo van preferencias y caché de interfaz.
- **Los triggers no tienen autoridad:** cambian la pantalla, no el estado del mundo.
- No inventar HTML: las ventanas salen de los originales (`do_not_invent_html: true`).

## 11. Conciliación con documentos anteriores

Ningún documento se borra ni se reescribe. Clave: (a) app de IA local o agente, (b) agente de memoria, (c) sistema operativo de ventanas.

| Documento | Tipo | Qué dice | Qué choca con el nuevo rol | Cómo se conserva |
|---|---|---|---|---|
| `§/frontend-repo-UI-YAIWES/Readme arquitectura UI YAIWES.md` | (a) | "YAIWES ejecuta IA desde móvil, PWA o navegador"; "YAIWES es la aplicación final."; un LOCAL ROUTER elige entre WebLLM, Transformers.js, wllama y remoto; "El router decide motor/proveedor." | La UI no es la aplicación final ni decide motor o proveedor; una inferencia local sería un recurso del Sistema 1 (S6), no de la UI | **Referencia histórica.** Su propia regla permite el módulo opcional: "5. Mantener UI separada de motores." y "6. Usar adapters intercambiables." Si algún día hay inferencia local, entra como módulo opcional que invoca el kernel |
| `§/readme arquitectura UI YAIWES interface beta/ARQUITECTURA-FRONTEND-UI-YAIWES-V1.md` | (c), con matiz (b) | Frontera de contrato; "Agente = YAIWES, CODE, NCT CODE, skills, roles, prompts, memoria y almacenamiento" (es un selector); "Dexie + IndexedDB para persistencia local"; flujo `... -> EVENTO -> STATESTORE -> UI` | "Agente" y "memoria y almacenamiento" son solo opciones de selector (los datos vienen del Sistema 1); la persistencia local debe quedar en caché y preferencias | **Vigente.** Es la base del modelo de SO; el flujo EVENTO -> STATESTORE -> UI es el punto de enganche de los triggers |
| `§/readme arquitectura UI YAIWES interface beta/PLAN-DE-TRABAJO-UI-YAIWES.md` | (c) | "`StateStore`: estado visual y local, sin duplicar memoria backend"; no implementar "memoria interna" ni "lógica de agentes" | Ninguno | **Vigente**; ya prohíbe que la UI sea agente de memoria |
| `§/readme arquitectura UI YAIWES interface beta/memoria.md` | (b) solo en el nombre | "Memoria de continuidad" del equipo de trabajo (bitácora y handoff entre IAs) | El nombre sugiere memoria de producto; no lo es | **Se mantiene** como memoria del equipo de desarrollo, ajena al Sistema 1 |
| `§/readme arquitectura UI YAIWES interface beta/COMO-SE-CONECTA-BACKEND.md` y `§/readme arquitectura UI YAIWES interface beta/NOTA-ARQUITECTURA-BACKEND-FRONTEND-Y-DISENO.md` | (c) | Botón -> ABS -> host -> kernel (local, web, github, huggingface, gdrive, database); nube solo por el kernel; tokens fuera de la ventana | Ninguno | **Vigentes**; sostienen las reglas de la sección 10 |
| `§/fabrica-ui/runtime/lote-01-nucleo-host/03-action-bus.js` y `§/Ui Yaiwes interface beta/02-fromted/HOST.html` | (c) | ActionBus "RibbonX onAction"; "1 iframe = 1 Lego" | Ninguno | **Vigentes**; son el núcleo del SO de ventanas |
| `§/frontend-repo-raiz/Skills arquitectura frontend Yaiwes/README-ARQUITECTURA-FROMTED-YAIWES.md` | (c) | "Modular Office 2007: agregar ventanas/botones desde fabrica interna." | Ninguno | **Vigente** (movido en P1) |
| `§/frontend-repo-UI-YAIWES/readme arquitectura UI YAIWES/ARQUITECTURA-FACTORY-SEGMENTADA-V10-2026-09-14.md` y `§/frontend-repo-UI-YAIWES/readme arquitectura UI YAIWES/DELTA-DEBATE-SOL123-RUNTIME-FABLES-2026-09-11.md` | fábrica de desarrollo | "Fables Universal Plugin + Capability Bus" es el enchufe de componentes de la fábrica; "Fables no es nuevo workflow owner ni nuevo registry." | Ninguno (Fables aquí es un plugin de la fábrica, no el autor de una arquitectura) | **Referencia de fábrica**; no entra en el producto |
| `§/fabrica-ui/HUGGINGFACE-Y-EXTRACT.md` | (c) | "HF no pinta botones. HF no es la fábrica. Es un **motor** enchufable al kernel." | Ninguno | **Vigente** |
| Router: README-DOS-SISTEMAS-DE-MEMORIA.md y LEEME.md (carpeta chat-router/memoria) | (b) | Llamaban a UI YAIWES "memoria del chat" y le asignaban conversaciones y sesiones | Choca: la UI no guarda memoria | Corregidos en el router en esta misma tarea (cambio mínimo) |

Los documentos de memoria y agentes (Memory OS, "sistema operativo de memoria por eventos", triggers de memoria) describen el **Sistema 1** y están en el router (carpeta chat-router/memoria/arquitectura); no se copian aquí.

## 12. Fallos conocidos y observaciones

**A corregir en ESTE repo cuando Antonio lo autorice** (no se ha tocado el código):

1. `puente-yaiwes.js` (`§/host-router-yaiwes/chat/frontend/yaiwes/puente-yaiwes.js`) devuelve `{ok:true}` a toda acción distinta de `send_message` sin hacer nada; contradice `failClosed`. Debería devolver `{ok:false, reason:'SIN_BACKEND'}`.
2. `ABS.js` (`§/fabrica-ui/runtime/ABS.js`) usa `postMessage(..., '*')` en dos llamadas y el contrato de `runtime-orchestration` prohíbe el origen `*` (`POSTMESSAGE_WILDCARD_ORIGIN_DENIED`). Además emite al host aunque no haya handler (`SIN_HANDLER`).

**Observaciones nuevas de esta revisión** (también sin tocar):

3. PANEL-01 guarda en `localStorage` (clave `yaiwes.panel01.chat.v2`) la lista de chats con sus mensajes, modo, herramientas y los últimos 12 eventos (`§/Ui Yaiwes interface beta/04-panels/PANEL-01-CHAT/src/panel-01-chat.js`). No son solo preferencias: es una **caché local**. Para cumplir "la verdad vive en el Sistema 1", esos datos deben tratarse como caché desechable y releerse del Sistema 1 cuando exista.
4. `HOST.html` escucha `message` sin comprobar `ev.origin` y su iframe no declara `sandbox`.
5. `§/seguridad/csp.json` permite `'unsafe-inline'` en `script-src`.
6. El panel de configuración usa una clave por defecto documentada en `§/fabrica-ui/runtime/lote-01-nucleo-host/10-wire.js`; debe cambiarse antes de producción.

## 13. Material movido y material que sigue fuera

Registros: `§/REGISTRO-MOVIDOS-T1.md` (2566 archivos, tarea 1) y `§/REGISTRO-MOVIDOS-P1.md` (3121 archivos, paso 1 de esta revisión). Copiado con `motor_3_copy_batches.py` (sha256 origen = destino, relectura), con manifiestos JSON junto a cada registro.

Frente a la raíz del repo `maxbry123-commits/frontend` (824.821 archivos): **faltan 743.244**, casi todos de terceros o de volumen: componentes open source descargados (carpetas "componentes open soure UI YAIWES", "componentes open soure fromtend" y "fabrica de UI INTERFACE fromtend"), `Download programas`, `Download librerías`, runtime/vendor de Wordflow, ENGINE ADAPTER, "todos los componentes" (Watchdog UI), `_work` y `.github`. Siguen solo en `frontend` (solo lectura) a la espera de que Antonio decida cómo y si se trasladan.
