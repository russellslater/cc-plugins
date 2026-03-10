# Apple Notes Plugin

MCP server plugin for Claude Code that provides read and write access to the macOS Apple Notes app.

## Requirements

- macOS (uses AppleScript to interact with Notes.app)
- Node.js >= 16

## Tools

| Tool | Description |
|---|---|
| `list_notes` | List all notes, optionally filtered by folder |
| `get_note_content` | Get the content of a note by name |
| `add_note` | Create a new note |
| `update_note_content` | Update an existing note's content |

## Development

Source code is in `server/index.js`. The bundled output in `dist/index.js` is what runs at runtime.

To set up the development environment:

```bash
cd server
npm install
```

To rebuild after making changes:

```bash
cd server
npm run build
```

This bundles the server and all dependencies into a single file at `dist/index.js` using esbuild.
