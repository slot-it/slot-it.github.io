# Slot-it Project Rules

## Overview
Static playground demonstrating the `<slot-it>` custom element managing a grid of `<slot-cell>` elements wrapping unnamed `<slot>` nodes.

## Component Architecture

### `<slot-it>` Web Component
- Standalone custom element owning its template, styling, and keyboard listeners
- Manages a grid of `<slot-cell>` children
- Centralizes state: current position [x,y], known bounds
- Dispatches custom "update" events to coordinate state across cells

### `<slot-cell>` Web Component
- Lightweight view wrapping an unnamed `<slot>`
- Tracks position via id pattern: `cell_${x}_${y}`
- Maintains edge flags: `edge="N"`, `edge="E"`, `edge="S"`, `edge="W"`, `edge="NE"`, `edge="SE"`, `edge="SW"`, `edge="NW"`
- Listens for "update" events to refresh state
- Renders user cursor marker when active

## Grid System

### Initial Grid
- 3×3 grid with coordinates from `[-1,-1]` to `[1,1]`
- Cell ids: `cell_-1_-1`, `cell_-1_0`, `cell_-1_1`, `cell_0_-1`, etc.
- Center cell `[0,0]` is the starting position

### Coordinate System
- `[x,y]` where x increases east, y increases south
- North: y decreases (y-1)
- South: y increases (y+1)
- East: x increases (x+1)
- West: x decreases (x-1)

### Grid Expansion Rules
Movement stops at grid bounds. When active cell reaches an edge, expand the grid:

- **North edge (edge="N")**: Insert new row with translation `[0,-1]`, assign `edge="N"` to new northern cells, clear old north flags
- **East edge (edge="E")**: Append column with translation `[1,0]`, assign `edge="E"` to new eastern cells, clear old east flags
- **South edge (edge="S")**: Append row with translation `[0,1]`, assign `edge="S"` to new southern cells, clear old south flags
- **West edge (edge="W")**: Insert column with translation `[-1,0]`, assign `edge="W"` to new western cells, clear old west flags
- **Diagonal edges**: Handle compound expansions (e.g., NE expands both N and E)

After structural updates, dispatch "update" event with payload describing mutations and active [x,y].

## Keyboard Controls
- Arrow keys: 4-direction navigation (↑↓←→)
- Numpad: 8-direction navigation
  - 8: North
  - 9: Northeast
  - 6: East
  - 3: Southeast
  - 2: South
  - 1: Southwest
  - 4: West
  - 7: Northwest

## Events & Communication

### "update" Event
Custom event for cross-cell communication with payload:
- `activePosition`: Current `[x,y]` coordinates
- `gridBounds`: Current min/max coordinates
- `mutations`: Description of structural changes (optional)

Each `<slot-cell>` listens and updates:
- Edge attributes
- Active/cursor state
- Local position data

## Implementation Guidelines

### Code Style
- Vanilla JS only, no bundlers or frameworks
- Use helper: `const createElement = (tag, props = {}) => Object.assign(document.createElement(tag), props);`
- Default to ASCII in source files
- Terse comments for non-obvious logic only

### HTML Structure
- Keep `index.html` minimal
- Must link back to https://github.com/slot-it/slot-it.github.io
- Components compose DOM via template strings and createElement helper

### State Management
- `<slot-it>` owns grid state
- `<slot-cell>` instances are stateless views
- Custom events flow from parent to children

## Development
- Open `index.html` directly in browser or via static server
- No build step required
- Test keyboard navigation in browser devtools
- Verify grid expansion in all 8 directions
- Ensure new cells respect edge/coordinate rules
