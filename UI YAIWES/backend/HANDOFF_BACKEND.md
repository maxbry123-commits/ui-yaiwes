# HANDOFF BACKEND — 126 componentes

Origen de referencia: `maxbry123-commits/frontend`, commit `f24619095db85b6417e0b8227acf05c372846880`.
Destino: `maxbry123-commits/ui-yaiwes/UI YAIWES/backend/componentes/<nombre>/`.
La selección se limita a los 126 nombres de [INDICE.md](INDICE.md). No se autoriza añadir otros motores, servicios o agentes.

## Tres pasos (único alcance autorizado)

1. **Organizar:** carpetas, README, handoff, índice, origen/destino de cada componente y catálogo del código generado. Conservar `/README.md` principal.
2. **Limpiar y preparar:** separar lo seleccionado de lo descartado; empaquetar los componentes aprobados en ZIP por lotes. No borrar contenido necesario ni eliminar origen antes de verificar destino. Mantener licencias con sus paquetes.
3. **Trasladar y verificar:** un motor reutilizado procesa diversos componentes con una cola persistente, por destino. Partes ZIP inferiores a 90.000.000 bytes; se recomienda 85 MiB (89.128.960 bytes). Reconstrucción, CRC, SHA-256 de partes, ZIP y archivos, recuento de rutas, bytes, tipos, modos Git y enlaces. Comprobar en GitHub remoto el 100 % del material aprobado; **solo después** puede eliminarse el original exacto, no otras rutas.

## Motores ya identificados, sin declarar operación iniciada

- Motor 2: `UI YAIWES/➡️📂motores de descarga extracción copiado movimiento archivos frontend/📂Motor descarga de componentes y extracción de zip/motor_2_queue_download_extract.py`.
- Motor 1: `UI YAIWES/➡️📂motores de descarga extracción copiado movimiento archivos frontend/➡️📂 Motor de extracción zip/motor_1_extract_only.py`.
- Motor 3: `UI YAIWES/➡️📂motores de descarga extracción copiado movimiento archivos frontend/➡️📂motor de copiar archivos/motor_3_copy_batches.py`.

**Bloqueos actuales:** Motor 2 consume `source_repo` y ejecuta motor de descarga por componente externo, no resuelve automáticamente las 187 rutas internas. Motor 1 rechaza symlinks y no restaura modos Git. Motor 3 comprueba archivos por SHA-256 pero no certifica enlaces como enlaces ni modos del remoto. Ninguno impone por sí mismo la cuota de 90 MB por lote. Corregir estas incompatibilidades antes de ejecutar, sin introducir otro orquestador.

## Cierre exigido

`PENDIENTE → ZIP_PREPARADO → EXTRAÍDO_LOCAL → PUBLICADO → READBACK_100_POR_RUTA → APROBADO_PARA_LIMPIEZA`.

Si existe un solo faltante o hash/modo/tipo erróneo, no borrar su ruta original. La simple presencia de un directorio no es PASS. No iniciar GitHub Actions ni LFS. No exponer credenciales.
