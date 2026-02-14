# 🌬️ Wisp

> Context-aware, zero-dependency UI engine. Your HTML structure dictates the design.

**5KB total** • **Zero config** • **Zero dependencies** • **Semantic-first**

Wisp bridges the gap between "dumb beautiful" classless CSS and "smart complex" frameworks. It analyzes your HTML structure and automatically applies context-appropriate styling—no classes, no build step, no learning curve.

---

## ✨ The Problem

Current solutions force a choice:

| Approach | Limitation |
|----------|------------|
| **Classless CSS** (Pico, OAT) | Beautiful but static—doesn't adapt to content |
| **Utility-first** (Tailwind) | Powerful but verbose, requires build step |
| **Micro-frameworks** (Alpine) | Interactive but adds 15KB+ runtime |

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
- **Density**: Text-to-element ratio
- **Pattern**: Prose vs. structured vs. technical
- **Context**: Narrative, dashboard, form, or minimal

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
- Auto-expands `<details>` for narrative content
- Adds skip links for deep nesting
- Respects `prefers-reduced-motion` and `prefers-color-scheme`

---

## 📐 Contexts

Wisp automatically detects four contexts:

| Context | Trigger | Characteristics |
|---------|---------|-----------------|
| **Narrative** | >50% paragraphs | Increased line-height, reading-optimized width |
| **Dashboard** | Tables or 4+ cards | Compact spacing, full-width, smaller text |
| **Form** | 2+ inputs | Medium width, comfortable touch targets |
| **Minimal** | Default | Balanced defaults |

---

## 🛠️ Installation & Development

### macOS Setup
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
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   └── PULL_REQUEST_TEMPLATE.md
├── .gitignore
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
├── venv/
└── wisp-fetch
```

---

## 📊 Benchmarks

| Metric | Wisp | Pico | Tailwind | Alpine |
|--------|------|------|----------|--------|
| **Size** | 5KB | 15KB | 0KB* | 15KB |
| **Runtime** | 2KB | 0KB | 0KB | 15KB |
| **Config** | None | CSS vars | Extensive | JS |
| **Content-aware** | ✅ | ❌ | ❌ | ❌ |
| **Build step** | Optional | No | Required | No |

*Tailwind requires build process; purged CSS varies

---

## 📚 Examples

### Wikipedia Demo
Located in `docs/examples/wikipedia-demo.html`

Live demonstration of Wisp processing Wikipedia's "Wiki" article:

```bash
# Generate the demo
wisp-fetch https://en.wikipedia.org/wiki/Wiki -o docs/examples/wikipedia-demo.html --open
```

**What it shows:**
- Automatic detection of `narrative` context
- `prose` pattern recognition for encyclopedia content
- Reading-optimized typography (1.7 line-height, 65ch width)
- Clean extraction of main content (removes nav/ads/footer)
- Live analysis overlay showing detected metrics

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
<!-- Auto-expand details when in narrative context -->
<details data-wisp-expand="auto">
  <summary>More info</summary>
</details>

<!-- Hide on mobile -->
<aside data-wisp-fold="mobile">Sidebar content</aside>

<!-- Mark priority for high contrast -->
<section data-wisp-priority="critical">
  Important information
</section>
```

---

## 🌐 Browser Support

- **Modern browsers**: Full support (Chrome 88+, Firefox 78+, Safari 14+, Edge 88+)
- **Legacy**: Graceful degradation to standard semantic HTML
- **Screen readers**: Fully accessible, auto-generated ARIA where needed

---

## 🤝 Philosophy

1. **HTML First**: If it's semantic, it should look good
2. **Zero Config**: Sensible defaults, escape hatches when needed
3. **Progressive Enhancement**: Works without JavaScript, enhanced with it
4. **Performance**: Sub-5KB budget, zero blocking resources

---

## 📝 License

MIT © [rotsl](https://github.com/rotsl)

---

## 🗺️ Roadmap

- [ ] Vue/React wrapper components
- [ ] More contexts (e-commerce, documentation, wizard)
- [ ] CSS-only fallback mode
- [ ] Theme customization API
- [ ] Browser extension for one-click optimization


---

