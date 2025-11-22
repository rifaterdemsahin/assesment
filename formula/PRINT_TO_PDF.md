# Printing `video_script.md` to PDF

This document lists simple, reliable ways to export `formula/video_script.md` to PDF on macOS (zsh). Pick the method that best matches your setup.

**Quick tips before you start**
- Ensure images use relative paths (from this file: `../imaginary/act1.png`).
- If using VS Code, "Trust" the workspace if the preview blocks local image loading.
- For best layout control, use `pandoc` with a PDF engine (requires TeX or `wkhtmltopdf`).

---

**Method A — VS Code Preview (fast, WYSIWYG)**
- Open the file in VS Code: `code formula/video_script.md`
- Open the Markdown Preview: `Cmd+Shift+V` (or right-click -> "Open Preview")
- In the Preview page, open the print dialog: `Cmd+P` and choose "Save as PDF".
- Important: enable "Background graphics" (if present) to include images/backgrounds.

Pros: Quick and visual. Cons: Depends on VS Code preview rendering and workspace trust settings.

**Method B — Render in browser via `grip` (good with GitHub-style rendering)**
- Install `grip` (Python):

```
pip install --user grip
```

- Launch the renderer and open in browser:

```
grip formula/video_script.md
# then open http://localhost:6419 in your browser
```

- Use the browser's Print -> Save as PDF (Cmd+P). Adjust scale/margins as needed.

Pros: Uses GitHub-flavored Markdown rendering. Cons: Requires Python package.

**Method C — `pandoc` (best for reproducible PDFs)**
- Install `pandoc` (and a PDF engine):

```
brew install pandoc
# For a TeX engine (recommended):
brew install --cask mactex
# Or use wkhtmltopdf for HTML-to-PDF conversion:
brew install wkhtmltopdf
```

- Convert to PDF (XeLaTeX example):

```
cd /Users/rifaterdemsahin/projects/assesment
pandoc formula/video_script.md -o formula/video_script.pdf --from markdown --pdf-engine=xelatex
```

- Or with `wkhtmltopdf` (may preserve webpage-like styling):

```
pandoc formula/video_script.md -o formula/video_script.pdf --pdf-engine=wkhtmltopdf
```

Pros: Produces high-quality, automatable PDFs. Cons: Requires external engines (TeX or wkhtmltopdf).

**Method D — Node tool `md-to-pdf` (simple, no TeX)**
- Install node tool:

```
npm install -g md-to-pdf
```

- Run:

```
md-to-pdf formula/video_script.md -o formula/video_script.pdf
```

Pros: Simple, good defaults. Cons: Node tool may not match Pandoc's advanced formatting.

---

**Extra tips**
- If images are missing in the PDF, check that the image paths are relative and correct from `formula/`.
- If you want consistent fonts and typography, use `pandoc` + `xelatex` and provide a simple LaTeX template.
- To include custom CSS when converting via an HTML path, convert Markdown -> HTML, then print the HTML in a browser (or use `wkhtmltopdf`).

If you want, I can:
- Run a quick export using one of these methods (tell me which), or
- Add a Makefile task `make pdf` to automate the conversion.
