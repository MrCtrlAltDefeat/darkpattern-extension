# Contributing to darkpattern-extension

Thanks for helping make the web a less manipulative place. Here's how to contribute.

---

## Getting Started

```bash
git clone https://github.com/YOUR_USERNAME/darkpattern-extension.git
cd darkpattern-extension
npm install
```

**Load the extension in Chrome:**

1. Go to `chrome://extensions`
2. Enable **Developer Mode**
3. Click **Load Unpacked** → select the repo folder

Any changes to `scripts/content.js` take effect after refreshing the target page. Changes to `popup/popup.js` or `popup/popup.html` take effect after reopening the popup.

---

## Project Structure

```
darkpattern-extension/
├── manifest.json           # Extension config (Manifest V3)
├── scripts/
│   └── content.js          # Core detection engine — runs on every page
├── popup/
│   ├── popup.html          # Extension popup shell
│   └── popup.js            # Popup logic — queries content script findings
├── demo-site.html          # Test page with all 6 dark pattern types embedded
└── screenshots/            # Used in the README
```

---

## Adding a New Dark Pattern Detector

Each detector follows the same pattern:

```js
function detectMyPattern(root = document) {
    const findings = [];

    // Query elements, check conditions
    root.querySelectorAll("...").forEach((el) => {
        if (/* matches pattern */) {
            findings.push({
                id: createFindingId(),
                type: "my_pattern_type",     // snake_case, add to FINDING_TYPES
                severity: "high",            // "high" | "medium" | "low"
                description: "Human-readable description of what was found",
                element: el,                 // the DOM element to highlight
            });
            highlightElement(el, "color");
        }
    });

    return findings;
}
```

Then add it to the `detectors` array in `scanPage()` and add a label for it in `popup.js`'s `typeLabels` object.

**Before submitting, test your detector against:**
- `demo-site.html` (should trigger)
- Google.com, Wikipedia.org (should NOT trigger — avoid false positives)

---

## Branch Naming

| Prefix | Use for |
|---|---|
| `feat/` | New detector or feature |
| `fix/` | Incorrect detection (false positive or negative) |
| `docs/` | Documentation only |
| `refactor/` | Code cleanup, no behavior change |
| `chore/` | Tooling, config, CI |

---

## Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: add roach motel detector
fix: reduce false positives in countdown timer detector
docs: improve README installation steps
refactor: extract keyword matching into shared utility
```

---

## Code Style

- Vanilla JS only — no build step, no frameworks, no dependencies
- Keep detectors self-contained functions
- Avoid broad queries that will slow down page scanning
- `console.info` / `console.warn` are fine; avoid `console.log` in committed code
- Run `npm run lint` before opening a PR

---

## Questions?

Open a [Discussion](../../discussions) or file an issue.
