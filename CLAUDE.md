# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file web application for creating custom clearing names on Root board game maps. The app allows users to:
- Load different map images (autumn.webp, lake.webp)
- Place draggable, editable text overlays on the maps
- Save/load positions as JSON files
- Export the final map as a PNG image

## Architecture

The entire application is contained in `index.html` with embedded CSS and JavaScript. There is no build process or dependencies.

### Core Components

- **Image Management**: Uses a dropdown selector to switch between map variants. Each map has a corresponding `{map_name}_positions.json` file that stores text overlay positions
- **Text Overlays**: Dynamically created DOM elements positioned using percentage-based coordinates (relative to image dimensions). This ensures positions scale correctly across different screen sizes
- **Drag System**: Custom drag implementation using mousedown/mousemove/mouseup events. Positions are stored as percentages to maintain layout when the image resizes
- **Edit System**: Double-click text to edit inline. Enter saves, Escape cancels
- **Export System**: Canvas API used to render the image with text overlays for PNG download

### Data Format

Position JSON files (`autumn_positions.json`, `lake_positions.json`) contain arrays of:
```json
{
  "text": "Label text",
  "left": 12.3456,  // percentage from left edge
  "top": 45.6789    // percentage from top edge
}
```

### Responsive Design

Font size is dynamically calculated as 3% of image height (minimum 12px) using CSS custom properties (`--responsive-font-size`). This ensures text remains readable across different screen sizes.

## Development

To run: `python -m http.server` in the root of this repo.

To add a new map:
1. Add the image file
2. Create a corresponding `{map_name}_positions.json` file
3. Add an option to the `<select class="image-selector">` element in the HTML
