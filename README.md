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
- **Multi-level battlemaps, themes, light and sight** — the full [Chartdown language](https://github.com/Nossimonov/Chartdown/tree/main/docs/spec).

Try the language first in the [playground](https://nossimonov.github.io/Chartdown/) — no install, runs in your browser.

## Co-write your maps with an AI assistant

Chartdown is plain text, which means any LLM you already use can write it with you: describe the scene in prose ("the estate has a treasury, a ballroom, slave cells below…"), get a ` ```chartdown ` fence back, paste it in your note, and it renders. The plugin ships no AI, no API keys, and makes no network calls — you bring the assistant; you just have to teach it the language once per conversation:

- **Chat assistants** (ChatGPT, Claude, …): give it the single-file language reference — <https://nossimonov.github.io/Chartdown/llms-full.txt> — by pasting it into the chat (or just the link, for assistants that browse). Then describe your scene, or paste an existing map and describe the changes; ask it to reply with one ` ```chartdown ` block.
- **Tool-using agents** (Claude Code and other MCP clients): the [`@chartdown/mcp`](https://www.npmjs.com/package/@chartdown/mcp) server hands the agent the whole loop — the spec, fail-loud validation, and PNG rendering, so it can check its own work before you see it:

  ```
  claude mcp add chartdown -- npx -y @chartdown/mcp
  ```

Each map's toolbar closes the round trip: **Copy Chartdown** puts the map's source on your clipboard, opening with a comment that points at the language reference — so wherever you paste it, an LLM chat included, the reader knows what it's looking at and where the spec lives. **Paste Chartdown** brings the reply back: it accepts a bare document or a ` ```chartdown ` fence straight from the chat, validates it, and only then replaces the map in your note — an invalid paste changes nothing and tells you the offending line. (The paste button grays out while the clipboard is empty; the check looks only at clipboard format metadata, never the content — your clipboard is read exactly once, on an explicit paste click.)

## Manual installation

Until the plugin is in the community store: download `main.js`, `manifest.json`, and `styles.css` from the [latest release](https://github.com/Nossimonov/obsidian-chartdown/releases), place them in `<your vault>/.obsidian/plugins/chartdown/`, then enable Chartdown under **Settings → Community plugins**. (Or point [BRAT](https://github.com/TfTHacker/obsidian42-brat) at `Nossimonov/obsidian-chartdown`.)

## Development

Development happens in the [Chartdown monorepo](https://github.com/Nossimonov/Chartdown) (`packages/obsidian`), which is where the tests and issue tracker live — please file issues and PRs there. This repository carries the store-facing artifact: [`src/`](src/) and `styles.css` are synced verbatim from the monorepo by the release workflow (every release commit pins the exact source it was built from), and release assets carry [build-provenance attestations](https://github.com/Nossimonov/obsidian-chartdown/attestations). The plugin imports [`@chartdown/core`](https://www.npmjs.com/package/@chartdown/core) and [`@chartdown/render-svg`](https://www.npmjs.com/package/@chartdown/render-svg), published from the same monorepo.

## License

[MIT](LICENSE). The Chartdown language specification is CC-BY-4.0.
