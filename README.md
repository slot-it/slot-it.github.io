# slot-it.github.io

<<<<<<< HEAD
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
=======
Static playground for the `<slot-it>` custom element that manages a grid of `<slot-cell>` elements wrapping unnamed `<slot>` nodes.

## Features

- **Grid Navigation**: Use arrow keys or numpad for 8-direction movement
- **Dynamic Expansion**: Grid automatically grows when reaching edges
- **Web Components**: Vanilla JS custom elements, no build step required
- **Coordinate System**: 3×3 initial grid with `[x,y]` coordinates from `[-1,-1]` to `[1,1]`

## Usage

Open `index.html` directly in a browser or serve it with any static server. Use keyboard controls to navigate:

- **Arrow keys**: 4-direction navigation (↑↓←→)
- **Numpad**: 8-direction navigation (8=N, 9=NE, 6=E, 3=SE, 2=S, 1=SW, 4=W, 7=NW)

## Architecture

- `<slot-it>`: Main component managing grid state and keyboard listeners
- `<slot-cell>`: Lightweight cells wrapping unnamed `<slot>` elements
- Custom "update" events coordinate state across components
- See `project-rules.md` for detailed specification
>>>>>>> 1363c560b9a763a8f94bed4d6fa6871a20dbc5d2
