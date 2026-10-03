# Studio Router — Claude Code Brief

## Qué es
Herramienta visual para mapear el ruteo de un estudio de música: dispositivos (nodos) con puertos y cables de audio, MIDI, CV, Digital y ADAT. Uso personal del dueño (dony01001). Idioma de la UI y de la comunicación: español.

## Stack
- **Un solo archivo: `index.html`** (~3800 líneas). React 18 UMD + Babel standalone desde cdnjs; JSX dentro de `<script type="text/babel">`. Sin build, sin npm.
- Estilo de código: ES5 (`var`, `function`, `Object.assign`), estilos inline. Mantener ese estilo.
- Persistencia: `localStorage` (no hay servidor).
- Deploy: GitHub Pages desde `main` → https://dony01001.github.io/studio-router/
- Repo: github.com/dony01001/studio-router

## Probar en local
```bash
python -m http.server 8765 --bind 127.0.0.1
# abrir http://127.0.0.1:8765/index.html
```
`file://` no sirve en el browser pane; usar el servidor. Visores tipo htmlpreview/githack no funcionan (Babel inline / aviso intermedio).

## Subir cambios
`git push` directo falla por auth ("Invalid username or token"). Usar las credenciales de `gh` solo para el comando (sin tocar config global):
```bash
git -c credential.helper= -c "credential.helper=!gh auth git-credential" push
```

## Estado (2026-10-03)
- PR #1 (undo/redo, vistas, páginas, ADAT, tema, plantillas, setups…) **mergeado a `main`** (`1b33cd5`) y publicado en GitHub Pages.
- Trabajar desde esta carpeta (`D:iles\dev\studio-router`). Existe otro clon viejo del repo en otra carpeta (`studio-router/repo`) y un `index.html` suelto en `claude code/files/`: ambos desactualizados, no usarlos.
- Pendiente de decidir: si la primera carga (sin datos guardados) debe empezar vacía o con el "Estudio de ejemplo" (hoy: ejemplo).

## Mapa de `index.html`
Nivel módulo (antes de `StudioRouter`):
- Constantes: `NODE_W`, `PORT_H`, `PORT_PAD`, `HEADER_H`, `KIND_COLORS` (audio, midi, cv, digital, adat), `TYPE_ICONS`, `DEFAULT_DEVICES` (estudio de ejemplo).
- Vistas: `FULL_VIEW`, `viewIsFull`, `kindOk`, `dirOk`, `visiblePorts(dev, view)`; vista = `{kinds: [], dir: null|"in"|"out"}`.
- Layout de nodos: `portRows`, `portRowY`, `nodeHeight(dev, view)`; puertos `dir: "both"` (I/O, USB) van en fila propia al fondo.
- Cables: `roundedPath`, `idSeed` (carriles para cables "hacia atrás").
- Tema: `kindInk(kind)` (color de texto legible), `darkenHex`.
- CSV: `csvCell` (neutraliza `= + - @` para Excel), `toCSV` (BOM), `MODE_LABEL`, `DIR_LABEL`, `kindLabel`, `chStr`, `mpeStr`, `adatStr`, `downloadText`.
- `normalizeData(d)`: valida/normaliza JSON importado, versiones, setups y la carga inicial; migra puertos "digital" con "ADAT" en el nombre a `adat`.

Dentro de `StudioRouter`:
- **Historial undo/redo**: automático vía `useEffect` sobre `[devices, connections, stickyNotes, pages, customTypes]`, agrupa ráfagas <500 ms; `histBreak()` cierra la ráfaga antes de acciones discretas; `applyHistory`, `undo`, `redo`.
- **Listeners globales registrados una vez** con `latest.current.*` (teclado `onKey`, `pointerup`, `wheel` no pasivo).
- **Auto-save** con debounce 300 ms + flush en `beforeunload`.
- **Páginas de cables**: globales (`pages`, `curPage`) y por módulo (`dev.pages`, `modPage`); cada cable tiene `page` y `mpage: {devId: pageId}`; filtro con `connPageOk`; `pageConns` = cables de la página visible.
- **Posiciones**: `portPos` (useMemo) = `"devId|portId" → {x, y, nx, dir, both?, anchor?}`; `endPt` elige el lado de un puerto I/O; `devById`.
- **Render de cables**: bezier/ortho/straight; cables "hacia atrás" rodean por el hueco entre nodos; flecha de dirección (markers `arr-*`); con un nodo seleccionado, entradas `--flow-in` y salidas `--flow-out`.
- Menús de click derecho: `openCtx`, `ctxItems` (dev, port, conn, note, bg), `renderCtxMenu`.
- Categorías propias: `customTypes`, `renderTypePicker`, `addCustomType`, `renameCustomType`, `deleteCustomType`, `typeIcon`, `allTypes`.
- Plantillas de dispositivo: `templates`, `BUILTIN_TEMPLATES`, `saveTemplate`, `applyTemplate` (incluyen nombres de páginas del módulo).
- Setups (plantillas de estudio completo): `setups`, `BUILTIN_SETUPS`, `saveSetup`, `loadSetup`, `renameSetup`, `deleteSetup`.
- Otros: `duplicateSelection`, `startConnect` (evita duplicados), marquee (Shift+arrastrar), `renderPort`, renombrar puerto (`startRenamePort`/`commitRenamePort`), `makeBulkPorts`, `exportCSV`, `exportModuleCSV`, layouts (`animateTo` cancelable, `fitToView(posOverride, devList)`), `resetStudio` (vacía todo).

## Claves de localStorage
| Clave | Contenido |
|---|---|
| `studio-router-data` | estudio actual (devices, connections, stickyNotes, pages, curPage, modPage, customTypes, pan, zoom) |
| `studio-router-snapshots` | Versiones |
| `studio-router-user-layouts` | Mis Layouts (posiciones) |
| `studio-router-templates` | Plantillas de dispositivo |
| `studio-router-setups` | Setups |
| `studio-router-theme` | `light` / `dark` |

Reset solo vacía `studio-router-data`; el resto se conserva.

## Tema claro/oscuro
Colores como variables CSS en `:root[data-theme=...]` (`--fg` como `rgba(var(--fg),a)`, `--panel`, `--node`, `--shade`/`--shade-k`, `--*-ink`, `--flow-in/out`, `--danger-ink`, `--note-rgb/--note-k`). No usar colores fijos para texto/fondos: usar estas variables. `KIND_COLORS[k].line` solo para trazos.

## Cómo verificar cambios
Abrir con el servidor local en el browser pane, revisar consola sin errores y probar con eventos sintéticos vía JS (los clicks de puerto se disparan en el `<g>` padre del `<text>` del puerto). Limpiar `localStorage` de prueba al terminar.

## Roadmap pendiente
Pathfinding de cables que esquive nodos intermedios, búsqueda de dispositivos/puertos, exportar PNG/SVG, filtros MIDI por cable (clock/notes/CC/PC), transpose por cable, adjuntar archivos a dispositivos (IndexedDB), modo presentación, soporte mobile.
