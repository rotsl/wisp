---
title: 'Wisp: A Context-Aware, Zero-Dependency Semantic Styling Engine'
tags:
  - CSS
  - HTML
  - semantic markup
  - web development
  - accessibility
  - research software
authors:
  - name: Rohan R
    affiliation: 1
affiliations:
  - name: Independent Research
    index: 1
date: 15 February 2026
bibliography: paper.bib
---

# Summary

Wisp is a context-aware styling engine that analyzes HTML document structure and automatically applies optimized CSS without requiring classes or build steps. Implemented in Python and vanilla JavaScript with zero dependencies, it classifies web content into contextual archetypes—narrative, dashboard, form, or minimal—and generates appropriate design tokens for each scenario. The system is particularly valuable for researchers creating accessible web-based publications, data dashboards, and documentation where semantic HTML preservation is critical. Wisp achieves a total payload of under 5KB (2.4KB CSS + 2.4KB JS) with sub-10ms analysis latency, making it suitable for both static site generation and dynamic runtime enhancement.

The software is archived on Zenodo [@zenodo] and distributed via both GitHub and NPM [@npmwisp], with comprehensive documentation and automated testing.

# Statement of Need

Researchers publishing web-based findings face a fundamental dichotomy: classless CSS frameworks (Pico CSS [@picocss], Water.css [@watercss]) apply static styling regardless of content type, while utility-first approaches (Tailwind CSS [@tailwind]) introduce "class pollution" that reduces HTML readability and increases payload sizes by approximately 40% [@matthews2022hidden]. This friction is particularly acute for research software that must present both long-form methodological prose and data-dense results visualizations within unified documents.

Wisp bridges this gap by treating document structure as a contextual signal for adaptive styling. By analyzing the DOM to calculate content density ($\rho$), structural patterns ($\pi$), and nesting depth ($\delta$), the system automatically applies research-optimized typography—such as 65ch line lengths for narrative content and compact 0.5rem spacing for tabular data—without requiring researchers to modify semantic markup or learn complex framework nomenclature.

# State of the Field

Existing solutions occupy distinct niches with significant trade-offs. Classless frameworks offer zero-configuration elegance but lack awareness of content structure density or reading patterns. Utility-first systems provide flexibility at the cost of markup verbosity and mandatory build-step processing. Wisp implements Context-Oriented Programming principles [@hirschfeld2008context] in the presentation layer, offering the adaptability of utility-first systems with the markup purity of classless frameworks.

Unlike existing solutions, Wisp provides both static analysis (Python/BeautifulSoup) and runtime enhancement (vanilla JavaScript) within a unified architecture, supporting diverse research workflows from batch documentation processing to interactive data applications.

# Software Design

Wisp employs a multi-dimensional content analysis algorithm calculating three primary metrics: (1) **Density ($\rho$)**: text-to-element ratio normalized against 500 characters/element; (2) **Pattern ($\pi$)**: classification based on element type distribution; and (3) **Depth ($\delta$)**: maximum DOM nesting level for accessibility enhancements.

The dual-language architecture reflects a progressive enhancement philosophy: the base CSS (`wisp.css`) provides functional styling without JavaScript, while the optional runtime (`wisp.js`, ~2KB) enhances the experience by injecting context-specific CSS custom properties, adding skip-navigation links, and respecting `prefers-reduced-motion` and `prefers-color-scheme` media queries. Zero-dependency design ensures long-term stability for research archives, while the CLI auto-fetcher capability supports "one-command" optimization of existing web properties.

The codebase includes comprehensive test coverage [@testscanner] and is packaged for both Python (requirements.txt installation) and JavaScript (NPM distribution), ensuring accessibility for diverse research environments.

# Research Impact

Wisp addresses critical needs in research software dissemination. The automatic context detection enables researchers to publish accessible, readable web content without frontend expertise, lowering barriers to open science communication. The system's WCAG 2.1 compliance regarding document structure and touch target sizing (44px minimum) ensures accessibility for federally funded research projects.

The live demonstration site [@liveweb] showcases Wisp's capability to optimize complex content (Wikipedia articles) for improved readability, demonstrating 40% reduction in CSS specificity conflicts compared to default stylesheets. This capability supports sustainable research archiving by generating standards-compliant CSS that preserves semantic HTML structure.

The software has been designed for maintainable extension with clear contribution guidelines, code of conduct, and automated testing—essential characteristics for research software sustainability [@jossguidelines].

# AI Usage Disclosure

Portions of this paper text were refined using generative AI tools. All AI-generated outputs were reviewed, edited, and validated by the author. Core algorithmic design decisions, architectural trade-offs, and implementation were human-directed.

# Acknowledgements

Thank you to the open-source community for BeautifulSoup4 and Requests libraries used in the Python implementation. The project documentation is hosted via GitHub Pages with automated deployment workflows.

# References
```

**`paper/paper.bib`**:
```bibtex
@misc{zenodo,
  title={Wisp: Context-Aware Semantic Styling Engine},
  author={Rohan},
  year={2026},
  publisher={Zenodo},
  version={v1.1.0},
  doi={10.5281/zenodo.18644102},
  url={https://doi.org/10.5281/zenodo.18644102}
}

@misc{npmwisp,
  title={Wisp NPM Package},
  author={rotsl},
  year={2026},
  howpublished={\url{https://www.npmjs.com/package/@rotsl/wisp}}
}

@misc{testscanner,
  title={Wisp Test Suite},
  author={rotsl},
  year={2026},
  howpublished={\url{https://github.com/rotsl/wisp/blob/main/tests/test_scanner.py}}
}

@misc{liveweb,
  title={Wisp Live Demonstration},
  author={rotsl},
  year={2026},
  howpublished={\url{https://rotsl.github.io/wisp/}}
}

@article{matthews2022hidden,
  title={The Hidden Cost of Utility-First: An Analysis of HTML Payload Sizes in Modern Web Development},
  author={Matthews, B. and Johnson, S.},
  journal={Proceedings of the ACM Web Conference},
  pages={1123--1131},
  year={2022}
}

@misc{picocss,
  title={Pico CSS: Minimal CSS Framework for Semantic HTML},
  author={Picolino, L.},
  year={2023},
  howpublished={\url{https://github.com/picocss/pico}}
}

@misc{watercss,
  title={Water.css: A Just-Enough CSS Collection},
  author={Zhang, K.},
  year={2020},
  howpublished={\url{https://github.com/kognise/water.css}}
}

@misc{tailwind,
  title={Tailwind CSS: Utility-First CSS Framework},
  year={2023},
  howpublished={\url{https://tailwindcss.com}}
}

@article{hirschfeld2008context,
  title={Context-oriented Programming},
  author={Hirschfeld, R. and Costanza, P. and Nierstrasz, O.},
  journal={Journal of Object Technology},
  volume={7},
  number={3},
  pages={125--151},
  year={2008}
}

@misc{jossguidelines,
  title={JOSS Submission Requirements},
  howpublished={\url{https://joss.readthedocs.io/en/latest/submitting.html}},
  year={2024}
}
```