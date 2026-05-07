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

## Roadmap

Features pendientes para versiones futuras:

- **Adjuntar archivos a dispositivos** — fotos del back panel, presets (.syx/.json), manuales (PDF). Storage en IndexedDB para soportar archivos binarios. Thumbnails inline + preview/download.
- **Filtros MIDI por cable** — clock, notes, CC, PC, start/stop (refleja config MRCC)
- **Transpose por cable MIDI** — semitonos -24 a +24
- **Grupos de puertos** — agrupar puertos visualmente con color compartido (ej. DIN 1-4 = "Bus A")
- **MPE member channels** — configurar rango de canales miembro (lower/upper zone)
- **Undo/Redo** (Ctrl+Z / Ctrl+Shift+Z)
- **Búsqueda** de dispositivos y puertos
- **Exportar PNG/SVG** del canvas completo
- **Modo presentación** (pantalla completa sin toolbar)
- **Pathfinding cables** que evite módulos intermedios
- **Handles bezier** arrastrables (puntos C1/C2)
- **Migración a Vite + React modular** cuando agreguemos más features
- **Soporte mobile** (drag-drop touch, gestos)

---
Creado con Claude | Anthropic
