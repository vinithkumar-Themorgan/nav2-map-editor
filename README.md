# nav2 Map Editor

A tiny, dependency-free **occupancy-grid map editor** that runs entirely in your
browser. Load a [ROS 2 nav2](https://navigation.ros.org/) map (`.pgm` + `.yaml`),
clean up phantom obstacles left over from SLAM, draw missing walls, mark unknown
areas — then download the edited `.pgm` + `.yaml` back out.

**No install, no build, no server, nothing uploaded.** It's a single `index.html`.

## ✨ Features

- **Load** `map.pgm` + `map.yaml` (drag & drop or file picker). Supports binary
  **P5** and ASCII **P2** PGM, plus **PNG/JPG** maps.
- **Tools:** Erase → free (remove wrong obstacles), Draw wall, Mark unknown, Pan.
- Adjustable **brush size**, **undo** (button or `Ctrl+Z`), **revert all**.
- **Zoom to cursor** (wheel) and **pan** (drag with the Pan tool, or right/middle‑drag anytime).
- Keeps your map's **resolution / origin / thresholds** from the `.yaml` (editable),
  and writes a clean nav2‑compatible `.pgm` + `.yaml` — **exact orientation round‑trip**.
- 100% client‑side. Your maps never leave your machine.

## 🚀 Use it

**Option A — just open it.** Download `index.html` and double‑click it.

**Option B — GitHub Pages.** Push this folder to a repo, enable Pages
(Settings → Pages → deploy from branch), and share the URL.

```bash
# one-file, so hosting is trivial:
python3 -m http.server   # then open http://localhost:8000
```

## 🖱️ How to edit a map

1. **Drop** your `map.pgm` and `map.yaml` onto the window (or click *Load map*).
2. Pick a tool — **Erase → free** to delete obstacles that shouldn't be there.
3. Set the **brush** size and paint over the mistakes (drag to paint). `Ctrl+Z` undoes.
4. Set a **map name** and click **Download .pgm + .yaml**.
5. Drop the two files into your robot's map folder and relaunch `map_server` /
   localization. Done.

## 🎨 Color / value convention (nav2 standard)

| Meaning | Grayscale value written to the PGM |
|---|---|
| Free space | `254` (white) |
| Occupied / wall | `0` (black) |
| Unknown | `205` (gray) |

`negate`, `occupied_thresh`, and `free_thresh` are carried over from your input
`.yaml` unchanged.

## ⚠️ Notes

- Edit maps **offline** — don't overwrite the map a running Nav2/AMCL is using; save,
  verify, then swap it in.
- Waypoints saved against the map still line up because resolution/origin are preserved.
- Big maps (multi‑million pixels) load fine; painting stays fast (per‑cell updates).

## Contributing

It's one file of vanilla JS — PRs welcome (e.g. line/rectangle tools, keep‑out zones,
`.png` export, multi‑map tabs). Open an issue with your map if something fails to load.

## License

[MIT](LICENSE) — do whatever you like, attribution appreciated.
