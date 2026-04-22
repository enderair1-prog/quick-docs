<div align="center">

# 📄 Quick Docs

**Capture text snippets from any webpage. Write markdown notes. Stay organized — all inside a Chrome side panel.**

[![Version](https://img.shields.io/badge/version-2.0-blue?style=flat-square)](https://github.com/)
[![Manifest](https://img.shields.io/badge/manifest-v3-orange?style=flat-square)](https://developer.chrome.com/docs/extensions/mv3/intro/)
[![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)
[![Discord](https://img.shields.io/badge/Discord-Join%20Us-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/kNHPy56tT5)

</div>

---

## 📦 Project Structure

```
Quick-Docs/
├── manifest.json       # Extension manifest (Manifest V3)
├── background.js       # Service worker — context menu registration & storage
├── content.js          # Content script (lightweight, capture via context menu)
├── popup.html          # Side panel entry point
├── popup.js            # Core UI logic: tabs, markdown, export/import
├── style.css           # All extension styles
└── docs.html           # Embedded Google Docs viewer
```

---

## ✨ Features

- 🖱️ **Right-click capture** — select any text on any site, right-click → *Add to Quick Docs*
- 🔗 **Auto source tagging** — saves page title, URL, and timestamp with every snippet
- 📝 **Markdown notes editor** — write with full markdown support, toggle live preview
- 📄 **Docs tab** — access Google Docs directly from the panel
- 📋 **Copy All** — copy every snippet to clipboard instantly
- 💾 **Export / Import** — save everything to `.txt` and reload it anytime
- 🗑️ **Delete entries** — remove individual snippets
- 🔒 **100% local** — all data stored with `chrome.storage.local`, nothing leaves your device

---

## 🚀 Installation

> The extension is not on the Chrome Web Store. Install it manually in a few steps.

```bash
# 1. Clone the repository
git clone https://github.com/enderair1-prog/quick-docs.git

# 2. Open Chrome and navigate to
chrome://extensions

# 3. Enable Developer Mode (toggle in the top-right corner)
# 4. Click "Load unpacked"
# 5. Select the cloned project folder
```

The Quick Docs icon will appear in your toolbar — click it to open the side panel.

---

## 🛠️ Usage

### Capture a Snippet
```
1. Highlight any text on a webpage
2. Right-click → "Add to Quick Docs"
3. Snippet is saved with source URL + timestamp
```

### Write Markdown Notes

The Notes tab supports full markdown syntax:

```markdown
# Heading 1
## Heading 2

**bold**, *italic*, ~~strikethrough~~, `inline code`

- unordered item
- another item

1. ordered item
2. another

> blockquote

```js
console.log("fenced code blocks work too")
```

---
```

Switch between **Edit** and **Preview** mode inside the Notes tab.

### Export Your Data
```
Click Export → choose Snippets / Notes / Both → .txt file downloads
```

### Import Data
```
Click Import → select a previously exported .txt file → data reloads instantly
```

---

## ⚙️ Manifest Overview

```json
{
  "manifest_version": 3,
  "name": "Quick Docs",
  "version": "2.0",
  "description": "Capture text from any page and save to Google Docs",
  "permissions": ["storage", "activeTab", "sidePanel", "contextMenus"],
  "background": {
    "service_worker": "background.js"
  },
  "content_scripts": [
    {
      "matches": ["<all_urls>"],
      "js": ["content.js"]
    }
  ],
  "side_panel": {
    "default_path": "popup.html"
  }
}
```

---

## 🔒 Permissions

| Permission | Why it's needed |
|---|---|
| `storage` | Persist snippets and notes locally in the browser |
| `activeTab` | Read the current tab's title and URL for source tagging |
| `sidePanel` | Render the UI as a Chrome side panel |
| `contextMenus` | Register the right-click *"Add to Quick Docs"* menu item |

> ⚠️ No data is ever sent to an external server. Everything stays on your machine.

---

## 🧠 How It Works

```
User selects text on any webpage
            │
            ▼
  Right-click → "Add to Quick Docs"
            │
            ▼
  background.js fires contextMenus.onClicked
  captures: selectionText + pageUrl + tab.title
            │
            ▼
  chrome.storage.local.set({ entries: [...] })
            │
            ▼
  popup.js reads storage on load
  → renders snippets in the side panel UI
```

---

## 🤝 Contributing

Pull requests are welcome! To get started:

```bash
# 1. Fork the repository

# 2. Create a feature branch
git checkout -b feature/your-feature-name

# 3. Make your changes, then commit
git commit -m "feat: describe your change here"

# 4. Push to your fork
git push origin feature/your-feature-name

# 5. Open a Pull Request on GitHub
```

---

## 💬 Community & Support

Have a question, found a bug, or want to share feedback? Join the Discord!

<div align="center">

[![Discord](https://img.shields.io/badge/Discord-Join%20the%20Server-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/kNHPy56tT5)

</div>
```
MIT License — free to use, modify, and distribute.
```
