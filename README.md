# slot-it.github.io

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
