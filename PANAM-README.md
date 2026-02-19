# Pan Am Centre Interactive Map - Quick Start

## What You Have

- ✅ `Panam23.svg` - Your pool/sports facility map (5769 x 3917 pixels)
- ✅ `panam-data.json` - Your location data (14 locations)
- ✅ `panam.html` - Your map viewer
- ✅ `mapplic.js` & `mapplic.css` - Mapplic library files

## Quick Start with Node.js

### 1. Install http-server (one-time setup)

```bash
npm install -g http-server
```

### 2. Start the Server

Navigate to this directory in your terminal and run:

```bash
http-server -p 8000
```

### 3. Open Your Browser

Go to: **http://localhost:8000/panam.html**

That's it! Your map should now be visible.

---

## Your Locations

The map includes these 14 locations:

1. **Stair Case** - Hidden marker
2. **Media Room** - Hidden marker
3. **First Aid** - Hidden marker
4. **Mens Change Room** - Washroom (hidden)
5. **Womens Change Room** - Washroom (hidden)
6. **Teaching Studio** - Hidden marker
7. **Dive Pool** - Hidden marker
8. **Training & Warm-up Pool** - Hidden marker
9. **Competition Pool** - Hidden marker
10. **Elevator** - Hidden marker
11. **Information** - Hidden marker
12. **Lot003** - Hidden marker
13. **Fitness Centre** - Hidden marker
14. **Field House** - Hidden marker

**Note:** All your locations are set to `"type": "hidden"` - this means they won't show markers by default, but they ARE clickable if you've set up the SVG correctly.

---

## Making SVG Elements Interactive (Optional)

If you want clickable rooms/areas in your SVG:

### In Your SVG Editor (Illustrator, Inkscape, etc.):

1. Create a group named `MLOC-rooms` (must start with "MLOC-")
2. Inside that group, add elements with IDs matching your location IDs:
   - `Lot014`
   - `lot013`
   - `lot012`
   - etc.

Example SVG structure:
```xml
<g id="MLOC-rooms">
  <path id="Lot014" d="..." />
  <path id="lot013" d="..." />
  <rect id="lot012" x="..." y="..." />
</g>
```

The locations will automatically attach to these SVG elements!

---

## Customization

### Change Colors

Edit `panam-data.json` and modify:

```json
"primaryColor": "#1476FF"
```

### Show Marker Pins

If you want to show marker pins instead of hidden locations, edit each location in `panam-data.json`:

```json
{
  "id": "lot013",
  "title": "Media Room",
  "type": "pin",  // ← Change from "hidden" to "pin"
  ...
}
```

### Add Descriptions

Add a `desc` field to any location:

```json
{
  "id": "lot013",
  "title": "Media Room",
  "about": "Short description",
  "desc": "<p>Full HTML description with <strong>formatting</strong></p>",
  ...
}
```

### Add Images

Add image fields:

```json
{
  "id": "lot013",
  "title": "Media Room",
  "image": "assets/media-room.jpg",
  "thumb": "assets/media-room-thumb.jpg",
  ...
}
```

---

## Alternative: Python SimpleHTTPServer

If you don't have Node.js:

```bash
python3 -m http.server 8000
```

Then go to: `http://localhost:8000/panam.html`

---

## Alternative: PHP

```bash
php -S localhost:8000
```

Then go to: `http://localhost:8000/panam.html`

---

## Alternative: VS Code Live Server

1. Install the "Live Server" extension in VS Code
2. Right-click on `panam.html`
3. Select "Open with Live Server"

---

## Troubleshooting

### Map Not Showing?

1. **Check browser console** (F12)
2. **Make sure you're using a web server** (not opening the file directly)
3. **Verify file paths:**
   - `assets/Panam23.svg` should exist
   - `mapplic.js` and `mapplic.css` should be in the same directory

### Locations Not Working?

1. Your locations have `"type": "hidden"` - they won't show pins
2. To see them work, either:
   - Add matching SVG elements with MLOC- groups
   - OR change `"type"` to `"pin"` in panam-data.json

### Wrong Map Size?

The SVG dimensions (5769 x 3917) are already set in `panam-data.json`:

```json
"mapWidth": 5769,
"mapHeight": 3917
```

If your map still looks wrong, verify your SVG's actual dimensions:
- Open `Panam23.svg` in a text editor
- Look for `width="5769px" height="3917px"`

---

## Files

```
mapplic-starter/
├── panam.html              ← Your main file
├── panam-data.json         ← Your location data
├── mapplic.js              ← Mapplic library
├── mapplic.css             ← Mapplic styles
├── assets/
│   └── Panam23.svg        ← Your map
├── data.json              ← Demo mall data
└── index.html             ← Demo mall viewer
```

---

## Need Help?

Check the full documentation in `README.md` or the `docs/` folder from the original download.

Good luck with your map!
