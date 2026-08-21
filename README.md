# trohit920.github.io

Personal site for **Rohit Thakur** — AI/ML engineer, Seoul.

Live at **https://trohit920.github.io**

## Design

A single self-contained `index.html`. No frameworks, no build step, no
dependencies beyond a Google Fonts stylesheet. Roughly 34 KB of HTML, CSS and
JavaScript, which is smaller than most hero images.

The hero renders a **live token-level uncertainty trace** on a canvas: a
stylised version of the entropy curve produced by the
[LLM uncertainty quantification project](https://github.com/trohit920/llm-uncertainty-quantification).
Entropy stays flat while the model is on familiar ground and spikes where it
starts guessing, at which point the readout flips to low confidence and the
page suggests abstaining. The site demonstrates the thing it describes.

## Accessibility and performance

- Honours `prefers-reduced-motion`: the animation is replaced with a static
  trace and scroll reveals are disabled.
- Canvas carries a descriptive `aria-label`; no information is conveyed by
  colour alone.
- Animation pauses when the tab is hidden, and the interval is cleared on
  `pagehide`.
- Responsive from 390 px upward with no horizontal overflow.
- Visible focus rings on every interactive element.

## Local preview

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire site |
| `Rohit_Thakur_Resume.pdf` | Downloadable résumé, linked from the hero and contact section |
