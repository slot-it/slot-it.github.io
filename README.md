# slot-it.github.io

Keyboard playground for the custom `slot-it` web component. Open `index.html` in a browser to try the expanding grid of `slot-cell` elements.

## Quick Start
- Open `index.html` directly or serve the root directory with any static HTTP server.
- Focus the component and move with arrow keys or the numeric keypad (diagonals supported).
- Watch the grid grow as you push against its edges; new rows and columns follow the rules in `project-rules.md`.

## Project Notes
- Implementation lives completely in `index.html` using vanilla JavaScript.
- The helper `createElement(tag, props)` is reused to build all DOM nodes.
- `slot-it` manages grid state and emits `update` events so each `slot-cell` can refresh edge flags and the active cursor marker.
- Structural updates always trigger another `update` broadcast to keep every cell in sync.
- Keep `README.md` and `project-rules.md` aligned when behaviour changes.
