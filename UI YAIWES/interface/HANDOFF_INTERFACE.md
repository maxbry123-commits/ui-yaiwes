# HANDOFF INTERFACE — 61 componentes

Origen de referencia: `maxbry123-commits/frontend`, commit `f24619095db85b6417e0b8227acf05c372846880`.
Destino: `maxbry123-commits/ui-yaiwes/UI YAIWES/interface/componentes/<nombre>/`.
Catálogo cerrado: [INDICE.md](INDICE.md). No añadir agentes ni librerías fuera de la lista.

## Flujo autorizado

1. **Organizar:** crear README, índice, handoff y correspondencia origen/destino; preservar el `README.md` principal.
2. **Limpiar y preparar:** separar piezas visuales y código propio aprobado. En `big-AGI`, `Jan`, `LibreChat`, `Open WebUI`: copiar **solo la interfaz y sus imports necesarios**, excluyendo backend y agentes. Licencias y procedencia siempre presentes.
3. **Trasladar y verificar:** ZIP en lotes/partes menores de 90.000.000 bytes, usando idealmente 85 MiB por parte; un motor con múltiples componentes en cola persistente. Reconstruir, validar CRC/SHA-256, comparar el 100 % de rutas, tamaño, hash, permisos Git, enlaces y presencia remota. **Eliminar origen únicamente después de PASS remoto 100 % por ruta**.

## Componentes solapados

Alternativas de empaque (Electron, Flutter, Tauri, Wails, Neutralino-JS, AppJS, NodeGui) no deben convertirse simultáneamente en runtimes obligatorios. yup, zod y vest son opciones de validación; React, Radix, shadcn-ui y Tailwind son capas visuales complementarias. No duplicar routers, memoria ni motores de workflow.

## Precauciones técnicas

El Motor 2 actual descarga repositorios descritos mediante `source_repo`, por lo que **no basta** para copiar los árboles ya adquiridos. El Motor 1 rechaza symlinks y puede perder modos; el Motor 3 no comprueba integridad remota de tipos/permisos. Reutilizarlos sólo después de adaptar esa frontera; no inventar un PASS ni activar procesos no observados.

**Estado actual:** índice y handoff preparados; no hay copia de los 61 componentes acreditada por este documento. No GitHub Actions, LFS, credenciales en git ni borrados anticipados.
