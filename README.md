# UI YAIWES

Fuente única de **UI YAIWES** y **UI YAIWES interface** (decisión del Director, Antonio). Antes vivían repartidas entre `maxbry123-commits/frontend` ("fromtend") y copias dentro del repo del router; este repo es la referencia.

## Qué es

UI YAIWES es el **sistema de control del chat**: la interfaz (ventanas, botones, paneles, manifiestos) **sin lógica propia**. Pide y muestra; no decide ni guarda la verdad. Habla con "el kernel" (el Harness del router) por acciones y recibe eventos. No lleva tokens en las ventanas.

## Estructura real del repo

```
README.md
UI YAIWES/
└── UI YAIWES interface/
    ├── DOWNLOAD_EXTRACT_MANIFEST.json
    ├── _archives/            bundle .zip en partes (UI YAIWES interface.bundle.zip.part-NNNN)
    └── code/UI YAIWES interface/
        ├── Ui Yaiwes interface beta/   01-original (HTML subidos por el director, INVENTARIO-39.json),
        │                               02-fromted (las 39 ventanas + HOST.html + FICHAS/ + INDEX.json),
        │                               04-panels/PANEL-01-CHAT
        ├── fabrica-ui/                 fábrica DAG (PLAN-DAG-DETERMINISTA.json, bitacora-fabrica/),
        │                               runtime/ (ABS.js, security.js, connectors.js, lote-01-nucleo-host/ 01..10)
        ├── Fromtend/                   modules/M_RUNTIME_ORCHESTRATION, project-memory/ (mapas T2-R1..R5)
        ├── Backend/                    Motor3 approved donors (OSS aprobado), project-memory/
        ├── empaque/  seguridad/  qa/   PWA/Capacitor/Tauri stubs, CSP, pruebas Playwright
        ├── workflow/  skills/          contrato, DAG y DSL del frontend; skills de implementación y QA
        ├── frontend-repo-UI-YAIWES/    movido desde el repo frontend (ver REGISTRO-MOVIDOS-T1.md)
        ├── host-router-yaiwes/         variantes de host traídas del router (ver REGISTRO-MOVIDOS-T1.md)
        └── *.md / LOOP-SCHEMA.json     contratos y guías (AGENTS, ACCEPTANCE, DESIGN_SYSTEM, SKILL, ...)
```

## Las 39 ventanas

Definidas en `02-fromted/INDEX.json` (n = 39, cada una con ficha en `FICHAS/` y sha12):

| Grupo | IDs | Qué son |
|---|---|---|
| RUN | RUN-01..08 | Cascade, Tren, Auditor, Ventanas V-01..V-04, Orquesta, panel Sandbox, panel Código YAML, panel nodo/input/out |
| WALL | WALL-01..16 | Crazy Wall: bloques, árbol, archivos, modos preguntar/tap, 6 raíces, hojas, guardar/compartir, bitácora state.json |
| GBOT | GBOT-01 | Cáscara Grok Bot (sin source oficial) |
| FOTO | FOTO-01..14 | Referencias de pantallas (grafo de conocimiento, versionado, assets, skills, capas, almacenamiento, contexto, modelos, timeline, personalidad, evidencia) |

**Estado:** las 39 están partidas, con ficha y copiadas a `02-fromted/` (fábrica F0–F3). **Ninguna tiene aún "OK por ID del director"** (F11) ni validación de las 39 (F10): siguen pendientes de aprobación. Los módulos de producto derivados son 11 (M_AGENT_CHAT_SHELL, M_KNOWLEDGE_MEMORY_CONTEXT, M_GIT_VERSION_TIMELINE, M_STORAGE, M_EVIDENCE_AUDIT, M_ASSETS_SKILLS_MODELS, M_RUNTIME_ORCHESTRATION, M_TERMINAL_SANDBOX, M_WORKSPACE_FILES_BLOCKS, M_LAYERS_COMPOSITION, M_PERSONALITY_SETTINGS).

## Fábrica DAG F0–F12

Fuente: `fabrica-ui/PLAN-DAG-DETERMINISTA.json` y `fabrica-ui/bitacora-fabrica/state.json`.

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

## Cómo se sirve desde el chat

El chat del router (Vercel) sirve esta interfaz en la ruta **`/yaiwes`** (carpeta `chat/frontend/yaiwes/` del router, protegida por su guardia de cableado). El **puente `puente-yaiwes.js`** conecta el panel PANEL-01 con el Harness `puente_chat` por HTTP (misma ruta que usa `api.js`): COMPONENTE -> HARNESS -> HTTP -> FICHA -> MODELO. Las variantes de host del router están copiadas en `host-router-yaiwes/`.

## Reglas

- **Fail-closed:** toda acción sin backend debe fallar, nunca fingir éxito (`failClosed: true` en el manifiesto).
- **Sin tokens en las ventanas:** los conectores `github`, `huggingface`, `gdrive` y `database` responden `KERNEL_ONLY`; los abre el kernel.
- **Kernel externo:** la UI no decide ni guarda la verdad; en el navegador solo van preferencias de interfaz.
- No inventar HTML: las ventanas salen de los originales (`do_not_invent_html: true`).

## Relación con el Sistema de memoria de agentes

Conviven dos memorias con propósitos distintos: la **memoria del chat** (esta UI) y la **memoria de los agentes** (carpeta `chat-router/memoria/` del router). Ver el contrato y el mapa de los 11 módulos:
https://github.com/maxbry123-commits/router-universal-router-inteligente-/blob/main/chat-router/memoria/README-DOS-SISTEMAS-DE-MEMORIA.md

## Fallos conocidos a corregir en ESTE repo cuando se autorice

No se ha tocado el código. Pendiente de autorización de Antonio:

- (a) `puente-yaiwes.js` devuelve `{ok:true}` a toda acción distinta de `send_message` aunque no haga nada; contradice `failClosed` del manifiesto (debería devolver `{ok:false, reason:'SIN_BACKEND'}`).
- (b) `ABS.js` usa `postMessage(..., '*')` y el contrato de `runtime-orchestration` prohíbe el origen `*` (`POSTMESSAGE_WILDCARD_ORIGIN_DENIED`).

## Material de terceros que sigue solo en `maxbry123-commits/frontend`

No se ha movido aquí por volumen (cientos de miles de archivos de código abierto descargado: componentes OSS, `Download programas`, `Download librerías`, `runtime/vendor`, ENGINE ADAPTER). Hace falta decisión de Antonio sobre cómo y si se traslada. Ver `UI YAIWES/UI YAIWES interface/code/UI YAIWES interface/REGISTRO-MOVIDOS-T1.md`.
