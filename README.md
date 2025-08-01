# TreeX - Advanced Tree Structure Visualizer & Exporter

TreeX is a cross-platform CLI tool for visualizing and exporting folder structures. It provides emoji-based directory trees with extensive export capabilities to multiple formats text documents and images.

[![npm version](https://img.shields.io/npm/v/@icodewith-ai/treex.svg)](https://www.npmjs.com/package/@icodewith-ai/treex)
[![Website](https://img.shields.io/badge/website-iCodeWith.ai-blue?style=flat&logo=world&logoColor=white)](https://icodewith.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)


## Features

- 🎨 **Emoji Display** - Folder 📂, file 📄, hidden 🫥, and locked 🔒 icons
- 📤 **Multi-Format Export** - SVG, PNG, WebP, and Markdown with perfect emoji rendering
- ⚡ **Smart Filtering** - Configurable ignore lists and display options
- 🔍 **Detailed Information** - File permissions, hidden file detection and more
- 🎯 **Flexible Output** - Console display or export to files
- 🌍 **Cross-Platform** - Works on Windows, macOS, and Linux
- 🎨 **Emoji Management** - Customize folder, file, and status emojis with easy list, update, and restore commands
- 📝 **Ignore File Management** - Configure which files and folders to exclude from tree display

## 🚀 Installation

### Option 1: Install from NPM (Recommended)
```bash
npm install -g @icodewith-ai/treex
```

**Note for Linux users:** You may need to use `sudo`:
```bash
sudo npm install -g @icodewith-ai/treex
```

### Option 2: Development Installation
```bash
# Clone the repository
git clone https://github.com/icodewith-ai/treex.git
cd treex

# Install dependencies
npm install

# Make it globally available
npm link
```

### System Requirements
- **Node.js**: Version 14.0.0 or higher
- **Image exports**: Currently supported on Windows and macOS only

**Note for Linux users:** Image exports (PNG, WebP, SVG) are not available on Linux due to rendering compatibility issues. Markdown export is fully supported on all platforms.

## ⚡ Quick Start

```bash
# Basic usage - scan current directory
treex

# Show help with styled interface  
treex --help

# Scan specific directory
treex ./my-project

# Export to multiple formats
treex -E "svg,png,md" -S my-tree ./my-project

# Show detailed information
treex -d ./my-project
```

## 📖 Command Reference

### Basic Syntax
```bash
treex [directory] [options]
```

### Core Options

| Option | Short | Description |
|--------|-------|-------------|
| `--details` | `-d` | Show extra details like locked files and hidden indicators |
| `--collapsed` | `-c` | Only show top-level folders/files (non-recursive) |
| `--folders-only` | `-f` | Show only folders recursively, omit files |
| `--help` | `-h` | Display help information |
| `--version` | `-V` | Show version number |

### Export Options

| Option | Short | Description |
|--------|-------|-------------|
| `--export-as <types>` | `-E` | Export format(s) - comma-separated (md, svg, png, webp) |
| `--save-to <filename>` | `-S` | Export filename without extension |

### File / Folder Ignore Management Options

| Option | Short | Description |
|--------|-------|-------------|
| `--show-ignored` | `-s` | List currently ignored files/folders and exit |
| `--add-ignored <items>` | `-a` | Comma-separated names to add to ignored list |
| `--remove-ignored <items>` | `-r` | Comma-separated names to remove from ignored list |

### Emoji Management Options

| Option | Short | Description |
|--------|-------|-------------|
| `--list-emojis` | `-le` | List current emoji configuration and exit |
| `--update-emoji <type> <emoji>` | `-ue` | Update emoji for specified type (folder, file, hidden, locked, permissionDenied) |
| `--restore-emojis` | `-re` | Restore all emojis to default configuration |

## 📁 Export Formats

TreeX supports multiple export formats with emoji support:

### Image Formats (Windows & macOS only)
- **PNG** (`png`) - High-quality raster image
- **WebP** (`webp`) - Modern compressed format  
- **SVG** (`svg`) - Vector graphics

### Text Formats (All platforms)
- **Markdown** (`md`) - Code blocks with emoji support

**Linux Note:** Image exports are currently disabled on Linux due to compatibility issues.

## Examples

### Basic Directory Scanning

```bash
# Scan current directory
treex

# Scan specific directory with details
treex -d ./my-project

# Show only top-level items
treex -c ./my-project

# Show only folders (no files)
treex -f ./my-project
```

### Exporting

```bash
# Export to single format
treex -E svg -S project-structure ./my-project

# Export to multiple formats
treex -E "svg,png,md" -S documentation ./my-project

# Export with options to subdirectory
treex -E webp -S ./exports/collapsed-view -c ./my-project

# Export with details shown
treex -E "svg,md" -S detailed-tree -d ./my-project
```

### File / Folder Ignore Management

```bash
# Show what's currently ignored
treex -s

# Add files/folders to ignore list
treex -a "node_modules,.env,dist"

# Remove items from ignore list
treex -r "temp"
```

### Emoji Management

```bash
# Show current emoji configuration
treex -le

# Update folder emoji
treex -ue folder "🗂️"

# Update file emoji
treex -ue file "📋"

# Update hidden file emoji
treex -ue hidden "👻"

# Restore all emojis to defaults
treex -re
```

## Sample Output

### Console Output
```
📂 my-project
├── 📂 src
│   ├── 📄 index.js
│   ├── 📄 utils.js
│   └── 📂 components
│       ├── 📄 Header.jsx
│       └── 📄 Footer.jsx
├── 📂 public
│   ├── 📄 index.html
│   └── 📄 favicon.ico
├── 🫥 .gitignore
├── 📄 package.json
└── 📄 README.md
```

### With Details (`-d` flag)
```
📂 my-project
├── 📂 src
│   ├── 📄 index.js 🔒
│   └── 📄 utils.js
├── 🫥 .env 🔒 🫥
└── 📄 package.json
```

### Export Results
```
Export Results:

✅ Completed:
  - project-structure.svg
  - project-structure.png
  - project-structure.md

❌ Failed:
  - project-structure.txt: Unsupported export type
```

## ⚙️ Configuration

### Emoji Mappings
Edit `config/emojis.json` to customize icons:

```json
{
  "folder": "📂",
  "file": "📄", 
  "hidden": "🫥",
  "locked": "🔒",
  "permissionDenied": "🚫"
}
```

### Ignored Files
Default ignored items in `config/ignored-names.json`:

```json
[
  "node_modules",
  ".git",
  ".DS_Store",
  "dist",
  "build"
]
```

### Glob Pattern Support

```bash
# Add pattern to ignore all text files starting with "test"
treex -a "test*.*"

# Add pattern to ignore all .tmp files
treex -a "*.tmp"

# Add pattern to match single character
treex -a "temp?.log"
```

Supported patterns:
- `*` matches any characters (e.g., `*.log` matches `app.log`, `error.log`)
- `?` matches single character (e.g., `test?.txt` matches `test1.txt`, `testa.txt`)
- Case insensitive matching

## 🛠️ Development

### Project Structure
```
treex/
├── bin/
│   └── treex.js              # CLI entry point
├── commands/
│   ├── export.js             # Export orchestration
│   ├── export-types/         # Export format modules
│   │   ├── export_md.js      # Markdown exporter
│   │   ├── export_svg.js     # SVG exporter
│   │   ├── export_png.js     # PNG exporter (Puppeteer)
│   │   └── export_webp.js    # WebP exporter (Puppeteer)
│   ├── emoji-management.js   # Emoji customization system
│   ├── cli-styling.js        # CLI styling with Figlet and Chalk
│   ├── ignored-files.js      # Ignore list management
│   └── scan-folder.js        # Core scanning logic
├── config/
│   ├── emojis.json          # Emoji mappings
│   └── ignored-names.json   # Default ignore list
└── package.json
```

### Dependencies
- **commander** - CLI framework and argument parsing
- **figlet** - ASCII art text generation for stylized headers
- **chalk** - Terminal text styling and colorization
- **puppeteer** - Headless browser for color emoji rendering
- **module-alias** - Clean import paths (`@emojis`, `@ignored`)



### Adding New Export Formats
1. Create `commands/export-types/export_newformat.js`
2. Export an object with: `{ format, extension, description, name, binary, contentType }`
3. The system auto-discovers new formats

## Release Notes

See [release-notes.md](release-notes.md) for detailed information about what's new in each version.

## License

MIT License - see [LICENSE](./LICENSE) file for details.

## About

Created by Marcelo Lewin from [iCodeWith.ai](https://icodewith.ai)


## Issues

Found a bug or have a feature request? Please open an issue on GitHub.