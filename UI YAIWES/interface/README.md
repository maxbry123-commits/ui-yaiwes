# Interface — UI YAIWES

Destino aprobado para **61 componentes visuales** (ventanas, chat, editores, formularios, gráficos, diseño y empaquetado de interfaz) y el **código propio visual** que resulte identificado por ruta.

- [Índice nominal cerrado (61)](INDICE.md).
- [Handoff y condiciones de reutilización](HANDOFF_INTERFACE.md).
- [Índice general de material seleccionado](../INDICE-TRASLADO.md).
- `/README.md` principal del repositorio se conserva sin sobrescribir.

En big-AGI, Jan, LibreChat y Open WebUI **solo se permite reutilizar interfaz**; no trasladar servidores, inferencia, bucles ni agentes autónomos. Revisar el límite de imports antes de extraer el subconjunto UI.

ZIP/cola: un motor procesa **varios componentes**, con límite por parte/lote de 90.000.000 bytes (objetivo 85 MiB). Ningún componente se declara trasladado o integrado sin lectura remota y cotejo completo de archivos. **Estado de esta carpeta: documentación del paso 1; traslado pendiente.**
