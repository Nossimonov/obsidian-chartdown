# Chartdown for Obsidian

Write TTRPG maps as plain text in your notes; see them as maps. [Chartdown](https://github.com/Nossimonov/Chartdown) is a Markdown-inspired language for battlemaps, hex charts, and region maps — this plugin renders every ` ```chartdown ` fence in place, entirely on your machine.

````markdown
```chartdown
# Ambush at Redford Crossing
map: battlemap
grid: square 20x15
scale: 5ft
[terrain]
river redford "The Redford" : path A9 F9 K9 P10 T10 width=2
road tollroad "Old Toll Road" : path K1 K15
ford : on redford on tollroad difficult
[tokens]
goblins g1 g2 : C12 E13
ogre "Gruk" : G9 size=2 hidden
party start : J14..L15
```
````

## What you get

- **Maps in your prep notes** — versionable, diffable, no graphical editor. Edit the fence, reopen the note, the map follows.
- **GM/player split, fail-closed** — `hidden` tokens, `[gm]` notes, and triggers render only in GM view. Each map has a toolbar toggle; the settings tab sets the default.
- **Export SVG** — one click writes the map (in the current view) next to the note and reveals it in your system file explorer.
- **Export UVTT** — one `.dd2vtt` per map level, with walls, doors, windows, and lights mapped for VTT import (Foundry, Roll20 via importers, Arkenforge, …) and the map image rasterized in-app. Note: `.dd2vtt` files are hidden in Obsidian's own file explorer (unknown extension) — they're real files in your vault folder, and the export reveals them.
- **Multi-level battlemaps, themes, light and sight** — the full [Chartdown v0.1 language](https://github.com/Nossimonov/Chartdown/tree/main/docs/spec).

Try the language first in the [playground](https://nossimonov.github.io/Chartdown/) — no install, runs in your browser.

## Manual installation

Until the plugin is in the community store: download `main.js`, `manifest.json`, and `styles.css` from the [latest release](https://github.com/Nossimonov/obsidian-chartdown/releases), place them in `<your vault>/.obsidian/plugins/chartdown/`, then enable Chartdown under **Settings → Community plugins**. (Or point [BRAT](https://github.com/TfTHacker/obsidian42-brat) at `Nossimonov/obsidian-chartdown`.)

## Development

Development happens in the [Chartdown monorepo](https://github.com/Nossimonov/Chartdown) (`packages/obsidian`), which is where the tests and issue tracker live — please file issues and PRs there. This repository carries the store-facing artifact: [`src/`](src/) and `styles.css` are synced verbatim from the monorepo by the release workflow (every release commit pins the exact source it was built from), and release assets carry [build-provenance attestations](https://github.com/Nossimonov/obsidian-chartdown/attestations). The plugin imports [`@chartdown/core`](https://www.npmjs.com/package/@chartdown/core) and [`@chartdown/render-svg`](https://www.npmjs.com/package/@chartdown/render-svg), published from the same monorepo.

## License

[MIT](LICENSE). The Chartdown language specification is CC-BY-4.0.
