# Studio Router

Herramienta visual e interactiva para mapear el ruteo de audio, MIDI, CV y digital de tu estudio de música.

![Studio Router](https://img.shields.io/badge/Studio-Router-00CEC9?style=for-the-badge)

## Características

- **Nodos arrastrables** para cada dispositivo de tu estudio
- **Conexiones visuales** con colores por tipo: Audio (turquesa), MIDI (amarillo), CV (rosa), Digital (azul), ADAT (violeta, cable tipo fibra óptica)
- **Cables ADAT** con modo de canales (8 ch a 44.1/48 kHz o 4 ch S/MUX a 88.2/96 kHz) y quién es clock master
- **Vistas** Full / Audio / MIDI / CV / Digital / ADAT: oculta nodos y puertos que no son del tipo (nodos compactos)
- **Vistas combinables**: Shift/Ctrl+click en los botones de tipo para mezclar (ej. MIDI + CV + ADAT); **→ In / Out →** muestran solo entradas o salidas (los cables llegan al encabezado del otro equipo)
- **Dirección de señal**: flecha en cada cable; al seleccionar un nodo, lo que entra se ve menta y lo que sale coral
- **Páginas de cables**: páginas globales (‹ › en la barra, ← → del teclado) y páginas por módulo (ej. cables virtuales del Hapax; ‹ › en el nodo o ← → con el nodo seleccionado)
- **Puertos I/O ⇄** (USB): una sola fila; el cable sale por el lado que mira al otro equipo
- **Filtro de modo** de operación (DAW / Jam / Ambos)
- **Undo/Redo** (Ctrl+Z / Ctrl+Shift+Z o Ctrl+Y) y botones ↶ ↷
- **Duplicar** nodos seleccionados con sus cables internos (Ctrl+D o ícono ⧉)
- **Notas** en cada dispositivo y notas libres (sticky notes) en el canvas
- **Editor de puertos** para agregar, quitar y modificar puertos de cada módulo
- **Plantillas de dispositivo**: en "Nuevo dispositivo" elige una plantilla (tus plantillas ★ o los equipos incluidos) para rellenar nombre, categoría, color, puertos y páginas del módulo; guarda con "★ Plantilla" o click derecho en un nodo → "Guardar como plantilla". Se guardan aparte y sobreviven a Reset
- **Categorías propias**: en el selector de tipo, "＋ Nueva categoría…" con nombre e ícono (emoji o símbolo); también se puede cambiar la categoría al editar un dispositivo; las categorías propias se renombran (✎, nombre e ícono) o borran (×, sus dispositivos pasan a "synth") junto al selector
- **Generar N puertos** de golpe (ej. 8 × "MIDI Out" → MIDI Out 1..8, la numeración continúa)
- **Setups** (plantillas de estudio): guarda el estudio completo (equipos, cables, notas, páginas, categorías) como punto de partida y cárgalo cuando quieras; incluye "Estudio de ejemplo"
- **Versiones/Snapshots** guardados internamente para comparar configuraciones
- **Exportar/Importar** vía JSON (copiar y pegar)
- **Exportar CSV**: patch list (un cable por fila) + inventario de puertos
- **Zoom y pan** con scroll y arrastrar
- **Tema claro y oscuro** (botón ☀/☾ en la barra o click derecho en el fondo); se recuerda y la primera vez sigue el tema del sistema
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
| Cancelar cable | Click derecho (mientras conectas) / Esc / Click en fondo |
| Zoom | Scroll del mouse |
| Pan (mover canvas) | Click + arrastrar en el fondo |
| Editar puertos | Seleccionar nodo → ícono ⚙ (azul) |
| Agregar nota al nodo | Seleccionar nodo → ícono ✎ (amarillo) |
| Borrar nodo | Seleccionar nodo → ícono × (rojo) |
| Duplicar nodo(s) | Ctrl+D / ícono ⧉ (turquesa) |
| Selección con caja | Shift + arrastrar en el fondo (suma a la selección) |
| Seleccionar todo | Ctrl+A |
| Cambiar página | ← → (con un nodo con páginas seleccionado: sus páginas) |
| Combinar vistas | Shift/Ctrl + click en MIDI, CV, ADAT… |
| Menú contextual | Click derecho en nodo, puerto, cable, nota o fondo |
| Renombrar puerto | Doble click en el puerto / click derecho → Renombrar |
| CSV de un módulo | Click derecho en nodo → Exportar CSV del módulo |
| Deshacer / Rehacer | Ctrl+Z / Ctrl+Shift+Z (o Ctrl+Y) |
| Borrar selección | Delete / Backspace |
| Cerrar ventanas / deseleccionar | Esc |
| Reset | Vacía todo (lienzo en blanco); conserva categorías, plantillas, setups, versiones y layouts; Ctrl+Z lo deshace |
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
- **Búsqueda** de dispositivos y puertos
- **Exportar PNG/SVG** del canvas completo
- **Modo presentación** (pantalla completa sin toolbar)
- **Pathfinding cables** que evite módulos intermedios
- **Handles bezier** arrastrables (puntos C1/C2)
- **Migración a Vite + React modular** cuando agreguemos más features
- **Soporte mobile** (drag-drop touch, gestos)

---
Creado con Claude | Anthropic
