# 🕵️ darkpattern-extension

<p align="center">
  <strong>A Chrome extension that detects dark patterns on websites in real time.</strong><br/>
  Highlights manipulative UI patterns inline and surfaces findings in a popup panel.
</p>

<p align="center">
  <img alt="CI" src="https://github.com/YOUR_USERNAME/darkpattern-extension/actions/workflows/ci.yml/badge.svg" />
  <img alt="Manifest V3" src="https://img.shields.io/badge/manifest-v3-blue" />
  <img alt="License" src="https://img.shields.io/badge/license-MIT-green" />
  <img alt="Zero dependencies" src="https://img.shields.io/badge/dependencies-none-brightgreen" />
</p>

---

![Extension demo](screenshots/extension-demo.png)

---

## 🔍 Detected Dark Patterns

| Category | What it catches | Highlight color |
|---|---|---|
| **Confirm Shaming** | Opt-out buttons with guilt-inducing copy ("No thanks, I hate saving money") | 🟠 Orange |
| **Obscured Interface** | Large fixed/absolute overlays with high z-index that block the page | 🔴 Red |
| **Preselected Opt-in** | Pre-checked consent checkboxes for newsletters, marketing, or data sharing | 🟣 Purple |
| **Trick Question** | Double-negative consent copy designed to confuse ("Uncheck if you don't want emails") | 🟤 Brown |
| **Fake Urgency** | Countdown timers and scarcity claims ("Only 2 left!", "Deal ends in 3:00") | 🟢 Green |
| **Disguised Ads** | Sponsored content cards with tiny, hard-to-read "Ad" labels | 🔵 Blue |

---

## 🚀 Installation

### From source (developer mode)

1. Clone or download this repo
2. Go to `chrome://extensions` in any Chromium-based browser
3. Enable **Developer Mode** (top right)
4. Click **Load Unpacked** → select the repo folder

The extension is now active on all pages.

### Test it locally

Open `demo-site.html` in your browser after loading the extension — it contains examples of all 6 dark pattern categories and is designed to trigger every detector.

---

## 📁 Project Structure

```
darkpattern-extension/
├── manifest.json           # Extension config (Manifest V3)
├── scripts/
│   └── content.js          # Detection engine — injected into every page
├── popup/
│   ├── popup.html          # Extension popup shell
│   └── popup.js            # Popup UI — displays findings from content script
├── demo-site.html          # Test page with all 6 pattern types embedded
└── screenshots/
    └── extension-demo.png
```

---

## ⚙️ How It Works

1. `content.js` is injected into every page by the browser (via `manifest.json`)
2. On load and on DOM mutations, it runs 6 detector functions over the page
3. Detected elements are highlighted with a colored outline and a tooltip
4. A floating panel summarizes findings in the bottom-right corner
5. The popup (click the extension icon) queries `content.js` for the current findings via `chrome.runtime.sendMessage`

Detectors use keyword matching, DOM structure analysis, and computed styles — no network requests, no external dependencies, no data leaves the browser.

---

## 🧪 Development

```bash
git clone https://github.com/YOUR_USERNAME/darkpattern-extension.git
cd darkpattern-extension
npm install      # installs ESLint for linting only — no runtime deps
npm run lint
```

After editing `scripts/content.js`, refresh the target tab to pick up changes. After editing popup files, close and reopen the popup.

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add new detectors.

---

## 🤝 Contributing

Contributions are welcome — new pattern categories, better keyword lists, false-positive fixes, UI improvements. See [CONTRIBUTING.md](CONTRIBUTING.md) to get started.

---

## 📄 License

[MIT](LICENSE)
