# Mapplic Setup Instructions

## What You Have

This folder contains everything you need to create an interactive map with Mapplic v8:

- `mapplic.js` - Main Mapplic JavaScript library
- `mapplic.css` - Mapplic stylesheet
- `index.html` - Demo with mall example
- `data.json` - Mall demo data
- `my-map.html` - **YOUR starter template**
- `my-data.json` - **YOUR starter data file**
- `assets/` - Demo images and SVG maps

## Quick Start with Your SVG

### Step 1: Add Your SVG Map

1. Put your SVG file in the `assets/` folder (or keep it in the root)
2. Name it something like `my-building.svg`

### Step 2: Update the Data File

Edit `my-data.json`:

```json
{
    "settings": {
        "mapWidth": 1000,    // ← Change to your SVG width
        "mapHeight": 800,    // ← Change to your SVG height
        ...
    },
    "layers": [
        {
            "id": "main",
            "name": "Main Floor",
            "file": "assets/my-building.svg"  // ← Path to your SVG
        }
    ],
    "locations": [
        {
            "id": "room101",
            "title": "Room 101",
            "x": 0.5,  // ← X coordinate (0 to 1, where 0.5 is center)
            "y": 0.5,  // ← Y coordinate (0 to 1, where 0.5 is center)
            "zoom": 3
        }
    ]
}
```

### Step 3: Update the HTML

Edit `my-map.html` and change the data-json path if needed:

```html
<mapplic-map data-json="my-data.json"></mapplic-map>
```

### Step 4: Run a Web Server

**IMPORTANT:** You MUST use a web server - you cannot just open the HTML file directly!

**Option 1: Python (if installed)**
```bash
# Python 3
python3 -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000
```

**Option 2: Node.js (if installed)**
```bash
npx http-server -p 8000
```

**Option 3: VS Code**
- Install "Live Server" extension
- Right-click on `my-map.html` → "Open with Live Server"

**Option 4: PHP (if installed)**
```bash
php -S localhost:8000
```

Then open: `http://localhost:8000/my-map.html`

## Making SVG Elements Interactive

If you want clickable rooms/areas in your SVG (not just markers):

### In Your SVG Editor (Illustrator, Inkscape, etc.):

1. Create a group named `MLOC-rooms` (must start with "MLOC-")
2. Inside that group, add elements with IDs like:
   - `room101`
   - `room102`
   - `room103`

SVG structure:
```
MLOC-rooms (group)
  ├─ room101 (path/rect/etc)
  ├─ room102 (path/rect/etc)
  └─ room103 (path/rect/etc)
```

3. In your data.json, create locations with matching IDs:
```json
{
    "id": "room101",
    "title": "Room 101",
    "layer": "main"
}
```

The location will automatically attach to the SVG element!

## Location Coordinates

For marker-based locations (not SVG elements), use x/y coordinates:
- `x: 0` = left edge
- `x: 0.5` = horizontal center
- `x: 1` = right edge
- Same for `y` (vertical)

## Using the Map Builder (Optional)

To use the visual editor:

1. Copy the `packages/editor/dist` folder from the download
2. Run `node save.js` in that folder
3. Open `http://localhost/editor/dist/index.html?map=../your-project/my-data.json`

## File Structure

```
your-project/
├── mapplic.js          ← Required
├── mapplic.css         ← Required
├── my-map.html         ← Your HTML page
├── my-data.json        ← Your map data
└── assets/
    └── my-building.svg ← Your SVG map
```

## Common Issues

### "Map not showing"
- Check browser console for errors (F12)
- Make sure you're using a web server
- Verify SVG path in data.json is correct
- Check that mapWidth/mapHeight match your SVG dimensions

### "Locations in wrong place"
- Double-check mapWidth and mapHeight in settings
- Verify your SVG's actual dimensions (viewBox or width/height attributes)

### "SVG elements not clickable"
- Make sure group name starts with `MLOC-`
- Element IDs must match location IDs exactly
- Element IDs must start with a letter (not a number)

## Next Steps

1. ✅ Add your SVG to the `assets/` folder
2. ✅ Update `my-data.json` with your map dimensions and path
3. ✅ Add locations with coordinates
4. ✅ Start a web server and test
5. 🎨 Customize colors, sidebar, and other settings in `my-data.json`

## Documentation

Full documentation is in the `docs/` folder from the original download.

Key points:
- Use `<mapplic-map data-json="...">` element
- Always include `type="module"` on the script tag
- Coordinates are 0-1 scale (percentages)
- SVG groups starting with "MLOC-" become interactive

Good luck with your map!
