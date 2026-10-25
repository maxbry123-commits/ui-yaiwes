# Registro de material movido a esta fuente única (PASO 1)

Orden del Director: mover la raíz completa de UI YAIWES al destino único y revisar de nuevo. Copiado con `motor_3_copy_batches.py` (`COLLISION_POLICY=fail`, lotes de 100, sha256 origen = destino, relectura), a partir de un directorio de preparación con exactamente los archivos faltantes. Después se volvió a comprobar sha256 de los 3121 archivos origen frente a destino: 0 diferencias. Lista completa con tamaños y sha256 en `REGISTRO-MOVIDOS-P1.manifest.json`.

Origen: repo `maxbry123-commits/frontend`, commit f24619095db8 (clon superficial, solo lectura). Destino: este repo.

| Carpeta aquí | Origen | Archivos | Contenido |
|---|---|---|---|
| `frontend-repo-UI-YAIWES/` | `frontend`, carpeta `UI YAIWES/` | 517 | Lo propio que T1 había dejado fuera: `watchdog UI YAIWES/Astra plan fábrica UI YAIWES` (465), `Wordflow LOOP UI YAIWES` (documentos, notas de auditoría, Crazy Wall Orquestador, capas de workflow, PIPELINE, HANDOFF y readme), checkpoint Astra |
| `frontend-repo-raiz/` | raíz de `frontend`, mismas rutas | 2604 | `Skills arquitectura frontend Yaiwes` completa (incluida `lote-zips-extraidos`, 2417), `copia-1-input-block-verbatim`, `scripts`, `forensics`, `diseño Video 3d`, `diseño web`, `Maxbry web`, `Maxbry AGI`, `NCT neuronas code turbo`, `UI Osquestador Maxbry`, `UI Osquestador auditor memoria`, `UI router inteligente universal`, `T-3000 MOTOR AUTOEVOLUTION`, `conectividad con Router inteligente universal`, motores de descarga (2 carpetas), HANDOFF.md, extraction-result.json, Indice de componentes |

Total: 3121 archivos (7 MB + 19 MB aprox.), 0 fallidos.

## Método de comparación

Los rutas del origen y del destino no coinciden (el destino reorganiza), así que la comparación fue por contenido: identificador de blob de git (SHA-1 del contenido) de cada archivo del árbol de `frontend` frente al conjunto de blobs de este repo. "Falta" = contenido que no está en ningún sitio de este repo. Cifras del árbol de `frontend`: 824.821 archivos; antes de P1 faltaban 746.365; tras P1 faltan 743.244.

## Lo que sigue solo en `frontend` (743.244 archivos)

Material de terceros o de volumen, sin tocar: componentes open source descargados (`componentes open soure UI YAIWES` 302.543, `componentes open soure fromtend` 176.606, `fabrica de UI INTERFACE fromtend` 73.473), `Fabrica Empaque-local YAIWES` (Download programas, 94.930), `todos los componentes/Watchdog UI` (25.579), `Wordflow LOOP UI YAIWES/runtime/vendor` (24.282), `watchdog UI YAIWES/Download librerías` (14.362), descarga extracción 14 faltantes (14.274), ENGINE ADAPTER (11.274), `_work` (6.183) y `.github` (204). Hace falta decisión de Antonio sobre cómo y si se trasladan; un traslado en bloque excede los límites de empuje (HTTP 413) y de tamaño de este repo.
