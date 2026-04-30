# Studio Router

Herramienta visual e interactiva para mapear el ruteo de audio, MIDI, CV y digital de tu estudio de música.

![Studio Router](https://img.shields.io/badge/Studio-Router-00CEC9?style=for-the-badge)

## Características

- **Nodos arrastrables** para cada dispositivo de tu estudio
- **Conexiones visuales** con colores por tipo: Audio (turquesa), MIDI (amarillo), CV (rosa), Digital (azul)
- **Filtros** por tipo de señal y modo de operación (DAW / Jam / Ambos)
- **Notas** en cada dispositivo y notas libres (sticky notes) en el canvas
- **Editor de puertos** para agregar, quitar y modificar puertos de cada módulo
- **Versiones/Snapshots** guardados internamente para comparar configuraciones
- **Exportar/Importar** vía JSON (copiar y pegar)
- **Zoom y pan** con scroll y arrastrar
- **Persistencia automática** en localStorage del navegador

## Uso

### Opción 1: Abrir directamente
Solo abre `index.html` en tu navegador (Chrome, Firefox, Edge).

### Opción 2: GitHub Pages
1. Haz fork de este repositorio
2. Ve a Settings → Pages
3. En "Source" selecciona "Deploy from a branch"
4. Selecciona `main` y `/ (root)`
5. Accede desde `tunombre.github.io/studio-router`

## Controles

| Acción | Control |
|--------|---------|
| Mover nodo | Arrastrar |
| Conectar puertos | Click en puerto → Click en otro puerto |
| Cancelar cable | Click derecho / Esc / Click en fondo |
| Zoom | Scroll del mouse |
| Pan (mover canvas) | Click + arrastrar en el fondo |
| Editar puertos | Seleccionar nodo → ícono ⚙ (azul) |
| Agregar nota al nodo | Seleccionar nodo → ícono ✎ (amarillo) |
| Borrar nodo | Seleccionar nodo → ícono × (rojo) |
| Editar conexión | Click en el cable |

## Datos

Todo se guarda en el `localStorage` de tu navegador. No se envía nada a ningún servidor.

---
Creado con Claude | Anthropic
