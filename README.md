# 🌬️ Wisp

[![GitHub CI](https://github.com/rotsl/wisp/actions/workflows/analysis.yml/badge.svg)](https://github.com/rotsl/wisp/actions/workflows/analysis.yml)
[![GitHub Pages](https://github.com/rotsl/wisp/actions/workflows/pages/pages-build-deployment/badge.svg)](https://github.com/rotsl/wisp/actions/workflows/pages/pages-build-deployment)
[![GitHub Release](https://img.shields.io/github/v/release/rotsl/wisp)](https://github.com/rotsl/wisp/releases)
[![GitLab Release](https://img.shields.io/gitlab/v/release/79488041)](https://gitlab.com/rotsl/wisp/-/releases)
[![GitLab CI](https://gitlab.com/rotsl/wisp/badges/main/pipeline.svg)](https://gitlab.com/rotsl/wisp/-/pipelines)
[![License](https://img.shields.io/github/license/rotsl/wisp)](LICENSE)
[![Repo Size](https://img.shields.io/github/repo-size/rotsl/wisp)](https://github.com/rotsl/wisp)
[![Last Commit](https://img.shields.io/github/last-commit/rotsl/wisp)](https://github.com/rotsl/wisp/commits/main)

> Context-aware, zero-dependency UI engine. Your HTML structure dictates the design.

**~5KB total** • **Zero config** • **Zero dependencies** • **Semantic-first**

Wisp bridges the gap between "dumb beautiful" classless CSS and "smart complex" frameworks. It analyzes your HTML structure and automatically applies context-appropriate styling—no classes, no build step, no learning curve.

Current release: **v0.1.0**

* GitHub: [https://github.com/rotsl/wisp/releases/tag/v0.1.0](https://github.com/rotsl/wisp/releases/tag/v0.1.0)
* GitLab: [https://gitlab.com/rotsl/wisp/-/tags/v0.1.0](https://gitlab.com/rotsl/wisp/-/tags/v0.1.0)

---

## ✨ The Problem

Current solutions force a choice:

| Approach                      | Limitation                                    |
| ----------------------------- | --------------------------------------------- |
| **Classless CSS** (Pico, OAT) | Beautiful but static—doesn't adapt to content |
| **Utility-first** (Tailwind)  | Powerful but verbose, requires build step     |
| **Micro-frameworks** (Alpine) | Interactive but adds 15KB+ runtime            |

**Wisp occupies the missing middle**: intelligent, adaptive, and lighter than a PNG.

---

## 🚀 Quick Start

### Option 1: Runtime (Dynamic)

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/rotsl/wisp@main/dist/wisp.min.css">
</head>
<body>
  <main>
    <h1>Your Content</h1>
    <p>Wisp automatically detects this is narrative content...</p>
  </main>
  <script src="https://cdn.jsdelivr.net/gh/rotsl/wisp@main/dist/wisp.min.js"></script>
</body>
</html>
```

### Option 2: Auto-Fetch (CLI)

```bash
# Install
git clone https://github.com/rotsl/wisp.git
cd wisp
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Fetch and optimize any webpage
./wisp-fetch https://en.wikipedia.org/wiki/Wiki --open
```

---

## 🧠 How It Works

### 1. Content Analysis

Wisp scans your DOM and calculates:

* **Density**: Text-to-element ratio
* **Pattern**: Prose vs. structured vs. technical
* **Context**: Narrative, dashboard, form, or minimal

### 2. Dynamic Styling

Generates CSS custom properties:

```css
:root {
  --wisp-context: narrative;
  --wisp-density: 0.45;
  --wisp-spacing-unit: 1rem;
  --wisp-line-height: 1.7;
  --wisp-max-width: 65ch;
}
```

### 3. Semantic Enhancements

* Auto-expands `<details>` for narrative content
* Adds skip links for deep nesting
* Respects `prefers-reduced-motion`
* Respects `prefers-color-scheme`

---

## 📐 Contexts

Wisp automatically detects four contexts:

| Context       | Trigger            | Characteristics                                |
| ------------- | ------------------ | ---------------------------------------------- |
| **Narrative** | >50% paragraphs    | Increased line-height, reading-optimized width |
| **Dashboard** | Tables or 4+ cards | Compact spacing, full-width, smaller text      |
| **Form**      | 2+ inputs          | Medium width, comfortable touch targets        |
| **Minimal**   | Default            | Balanced defaults                              |

---

## 🛠️ Installation & Development

### macOS / Linux Setup

```bash
# Clone repository
git clone https://github.com/rotsl/wisp.git
cd wisp

# Create virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Build distribution files
python scripts/build.py

# Run tests
python tests/test_scanner.py

# Install CLI tool (optional)
sudo ln -s $(pwd)/wisp-fetch /usr/local/bin/wisp-fetch
```

GitLab CI configuration is located in `.gitlab-ci.yml`.

---

## 🎯 Usage Examples

### CLI Auto-Fetcher

```bash
# Basic usage - fetch and optimize
wisp-fetch https://en.wikipedia.org/wiki/Wiki

# Output to specific file
wisp-fetch https://example.com -o my-site.html

# Generate CSS only
wisp-fetch https://example.com --css-only -o styles.css

# Minified output
wisp-fetch https://news.ycombinator.com -m

# Open immediately in browser
wisp-fetch https://example.com --open

# Extract specific section
wisp-fetch https://github.com/readme -s '.markdown-body'
```

### Python API

```python
from src.core.scanner import WispScanner

html = "<your-html-content>"
scanner = WispScanner(html)
analysis = scanner.analyze()

print(f"Context: {analysis.context}")  # narrative/dashboard/form/minimal
print(f"Pattern: {analysis.pattern}")  # prose/structured/technical/navigational

css = scanner.generate_css()
```

---

## 📁 Project Structure

```
wisp/
├── .github/
│   ├── ISSUE_TEMPLATE/
│   └── PULL_REQUEST_TEMPLATE.md
├── .gitlab-ci.yml
├── CHANGELOG.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── SECURITY.md
├── dist/
├── docs/
│   └── examples/
├── requirements.txt
├── scripts/
├── src/
├── tests/
└── wisp-fetch
```

---

## 📊 Benchmarks

| Metric            | Wisp     | Pico     | Tailwind  | Alpine |
| ----------------- | -------- | -------- | --------- | ------ |
| **Size**          | ~5KB     | 15KB     | 0KB*      | 15KB   |
| **Runtime**       | ~2KB     | 0KB      | 0KB       | 15KB   |
| **Config**        | None     | CSS vars | Extensive | JS     |
| **Content-aware** | ✅        | ❌        | ❌         | ❌      |
| **Build step**    | Optional | No       | Required  | No     |

*Tailwind requires build process; purged CSS varies.

---

## 📚 Examples

### Wikipedia Demo

Located in `docs/examples/wikipedia-demo.html`

```bash
wisp-fetch https://en.wikipedia.org/wiki/Wiki \
  -o docs/examples/wikipedia-demo.html \
  --open
```

**What it shows:**

* Automatic detection of `narrative` context
* `prose` pattern recognition
* Reading-optimized typography (1.7 line-height, 65ch width)
* Clean extraction of main content
* Live analysis overlay

**Generated CSS Variables:**

```css
--wisp-context: narrative
--wisp-pattern: prose
--wisp-density: 0.25
--wisp-line-height: 1.7
--wisp-max-width: 65ch
```

---

## 🎯 Intent Attributes

Control behavior without classes:

```html
<details data-wisp-expand="auto">
  <summary>More info</summary>
</details>

<aside data-wisp-fold="mobile">
  Sidebar content
</aside>

<section data-wisp-priority="critical">
  Important information
</section>
```

---

## 🌐 Browser Support

* Chrome 88+
* Firefox 78+
* Safari 14+
* Edge 88+

Legacy browsers gracefully degrade to semantic HTML.

Screen readers are fully supported, with ARIA enhancements where needed.

---

## 🤝 Philosophy

1. **HTML First** — Semantic markup should look good
2. **Zero Config** — Sensible defaults
3. **Progressive Enhancement** — Works without JavaScript
4. **Performance Budget** — Sub-5KB target

---

## 📝 License

MIT License
See `LICENSE` file.

---

## 🗺️ Roadmap

* [ ] Vue/React wrapper components
* [ ] More contexts (e-commerce, documentation, wizard)
* [ ] CSS-only fallback mode
* [ ] Theme customization API
* [ ] Browser extension for one-click optimization

---

<!-- 🌬️ Wisp Signature -->
<div align="center">

   

  <h1>🌬️ Wisp </h1>

  <p>✨ Design that thinks for you ✨</p>
  <p>🚫 Zero Classes • ⚙️ Zero Config • 💎 Pure HTML 🚫</p>

  <p>🚀⚡ Adaptive • Intelligent • Lightweight ⚡🚀</p>

  <p><em>🧠 Context-aware UI. No framework. No noise.</em></p>

  <br/>

  <strong>👨‍💻 Built by Rohan · @rotsl 💙</strong>

  <br/><br/>

   

</div>
