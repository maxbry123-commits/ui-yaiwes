# Transferencia de 187 componentes — colas máximo 20

**Paso de inicio:** 11 colas creadas para ejecuciones independientes; el controlador canónico se reutiliza sin modificarlo.

| Cola | Componentes | Estado |
|---|---:|---|
| [INTERFACE-M01](colas/INTERFACE-M01.json) | 20 | PREPARADA |
| [INTERFACE-M02](colas/INTERFACE-M02.json) | 20 | PREPARADA |
| [INTERFACE-M03](colas/INTERFACE-M03.json) | 20 | PREPARADA |
| [INTERFACE-M04](colas/INTERFACE-M04.json) | 1 | PREPARADA |
| [BACKEND-M01](colas/BACKEND-M01.json) | 20 | PREPARADA |
| [BACKEND-M02](colas/BACKEND-M02.json) | 20 | PREPARADA |
| [BACKEND-M03](colas/BACKEND-M03.json) | 20 | PREPARADA |
| [BACKEND-M04](colas/BACKEND-M04.json) | 20 | PREPARADA |
| [BACKEND-M05](colas/BACKEND-M05.json) | 20 | PREPARADA |
| [BACKEND-M06](colas/BACKEND-M06.json) | 20 | PREPARADA |
| [BACKEND-M07](colas/BACKEND-M07.json) | 6 | PREPARADA |

Totales: 61 interface + 126 backend = 187. Origen `maxbry123-commits/frontend@f24619095db85b6417e0b8227acf05c372846880`. Destino `maxbry123-commits/ui-yaiwes`.

**IMPORTANTE:** estos son manifiestos de selección de rutas internas del repositorio, no el formato de entrada de Motor 2, que espera repositorios externos. Su ejecución exige preparar staging de cada componente o un adaptador externo a los motores inmutables. Los motores no se han arrancado; no hay ZIP nuevos, no hay componentes transferidos por estas colas, ni se ha borrado el origen. Los campos `source_path_verified=false` necesitan corroboración por Git antes de transferir. No usar Motor 4 para limpiar hasta verificaciones 100 %.

Cada ZIP/parte debe ser inferior a 90 MB decimales; usar 85 MiB (89.128.960 bytes) por parte. Revisar symlinks, modos y blob SHA tras publicar. No incluir agentes autónomos.
