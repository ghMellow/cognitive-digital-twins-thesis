# SKILL-html-presentation — Interactive HTML Presentation Generator

**Purpose:** Transform any markdown or text content into an elegant, interactive single-file HTML presentation. Before generating, elicit style preferences to tailor the output precisely.

**When to use:** When you need a polished, self-contained `.html` presentation from thesis materials, research summaries, technical deep-dives, or any structured content.

---

## Step 0 — Elicit Style Before Generating

Before writing any code, ask the user the following questions. Do **not** skip this step.

```
Prima di generare la presentazione, ho bisogno di alcune preferenze:

1. **Tema visivo** — quale preferisci?
   a) Dark (sfondo quasi-nero, accenti oro) ← default consigliato
   b) Light (sfondo bianco, accenti blu/navy)
   c) Slate (grigio scuro, accenti cyan o verde)
   d) Personalizzato — dimmi tu colori e mood

2. **Densità dei contenuti** — quanto testo per slide?
   a) Minimalista (titolo + 3-4 punti max)
   b) Normale (5-7 punti, con sottopunti se necessario)
   c) Densa (tutto il contenuto, anche tabelle e code block)

3. **Stile tipografico** — quale tono?
   a) Editoriale (serif per i titoli, sans per il corpo) ← default consigliato
   b) Tecnico (tutto monospace / sans)
   c) Elegante (serif ovunque)

4. **Lingua dei label UI** (counter, sidebar, hint navigazione)
   a) Italiano ← default
   b) Inglese

Rispondi con le lettere (es. "a, b, a, a") oppure descrivi liberamente.
```

Use the answers to configure the variables in the prompt template below before generating.

---

## Prompt Template

```
You are an expert Frontend Developer and UI/UX Designer. Transform the [TEXT] below into a polished, single-file interactive HTML presentation.

---

### STYLE CONFIGURATION
(Fill these in based on the user's answers from Step 0)

THEME: [dark-gold | light-navy | slate-cyan | custom]
DENSITY: [minimal | normal | dense]
TYPOGRAPHY: [editorial | technical | elegant]
UI_LANGUAGE: [it | en]

---

### Technical Requirements

1. **Single file** — all CSS and JS inline in `<style>` and `<script>`. Zero external dependencies except Google Fonts (one `<link>` tag is allowed).

2. **Slide structure** — each slide is a `<section>` at 100% viewport. Slides are absolutely positioned; only the `.active` class is visible.

3. **Keyboard & touch navigation:**
   - → / Space / ↓ → next slide
   - ← / ↑ → previous slide
   - ESC → toggle sidebar
   - Touch swipe left/right on mobile
   - Smooth fade + translateY(16px) transition, duration 0.45s, easing cubic-bezier(0.4,0,0.2,1)

4. **Persistent UI elements:**
   - Bottom-left: slide counter in monospace font (e.g., `03 / 12`)
   - Bottom: thin progress bar that fills as slides advance
   - Bottom-right: navigation hint (auto-hides after 2.5s of inactivity, reappears on mousemove/keydown)
   - Top-left: hamburger icon (3 lines, 22px wide) that opens the sidebar

5. **Sidebar:**
   - Slides in from the left (translateX), width 300px
   - Semi-transparent dark overlay behind it when open
   - Each item shows zero-padded slide number + title
   - Active slide highlighted with accent color + left border

6. **Slide types to generate from content:**
   - **Title slide** — large serif title, italic tagline, decorative rule, eyebrow label
   - **Section slides** (left-aligned) — h3 eyebrow label (uppercase, accent color, 11px), h2 title, bullet list
   - **Diagram slides** — centered, monospace pre block with decorative label
   - **Code slides** — syntax-colored code block (left border accent, monospace)
   - **Callout element** — highlighted box for key objectives or quotes
   - **Closing slide** — centered, large title, spaced lines, italic accent phrase

7. **Left decorative bar** — on left-aligned slides, a 3px vertical line appears on the left edge, gradient from transparent → accent → transparent.

8. **Grain overlay** — a subtle SVG noise texture fixed over the entire page at low opacity (0.6) for depth.

---

### Design Tokens by Theme

#### dark-gold (default)
```css
--bg: #0a0a0f;
--surface: #111118;
--surface2: #18181f;
--border: rgba(255,255,255,0.07);
--accent: #c9a84c;
--accent-dim: #8a6e32;
--text: #f0ede8;
--muted: #6b6880;
--code-highlight: #4a9eff;
```
Fonts: `Playfair Display` (serif, titles) + `IBM Plex Mono` (mono) + `Inter` (body)

#### light-navy
```css
--bg: #ffffff;
--surface: #f5f5f7;
--surface2: #ebebef;
--border: rgba(0,0,0,0.08);
--accent: #003580;
--accent-dim: #6b8ab8;
--text: #1d1d1f;
--muted: #888899;
--code-highlight: #0066cc;
```
Fonts: `DM Serif Display` (serif, titles) + `JetBrains Mono` (mono) + `DM Sans` (body)

#### slate-cyan
```css
--bg: #0d1117;
--surface: #161b22;
--surface2: #21262d;
--border: rgba(255,255,255,0.08);
--accent: #39d0c8;
--accent-dim: #1e7a75;
--text: #e6edf3;
--muted: #7d8590;
--code-highlight: #79c0ff;
```
Fonts: `Space Grotesk` (titles) + `Fira Code` (mono) + `Inter` (body)

---

### Typography Scale

| Element       | Size (clamp)               | Weight | Family  |
|---------------|----------------------------|--------|---------|
| h1 (title)    | clamp(52px, 7vw, 88px)     | 700    | serif   |
| h2 (section)  | clamp(32px, 4vw, 52px)     | 700    | serif   |
| h3 (eyebrow)  | 11px, uppercase, 4px spaced| 500    | sans    |
| body / li     | clamp(16px, 1.6vw, 20px)   | 300-400| sans    |
| code inline   | 0.85em                     | 400    | mono    |
| counter       | 12px                       | 400    | mono    |

---

### Content Structure Rules

Analyze [TEXT] and divide into slides following these rules:

1. One idea per slide. Never cram multiple unrelated points.
2. Each section header in the text → new slide with h3 eyebrow + h2 title.
3. Bullet lists → `<ul>` with `<li>` items. Max 7 items. Split into two slides if more.
4. Code blocks → dedicated `<section>` with `.code-block` div.
5. ASCII diagrams or flowcharts → dedicated `<section>` with `.diagram` div.
6. Tables with 4+ columns → simplify to bullet comparison or split across slides.
7. Opening → always a title slide. Closing → always a closing slide with the key takeaway.

---

### Content to Transform

[INSERT_TEXT_HERE]

---

Output ONLY the complete, ready-to-use HTML file. No explanations, no markdown fences around it.
```

---

## Workflow

```
1. User provides content (markdown, plain text, notes)
2. Run Step 0 — ask the 4 style questions
3. Fill in STYLE CONFIGURATION in the prompt template
4. Generate the HTML
5. Save as presentation.html
6. Open in browser — navigate with ← →, Space, ESC
```

---

## Quick-Start (skip elicitation)

If the user says "just generate it" or is in a hurry, use these defaults:
- Theme: `dark-gold`
- Density: `normal`
- Typography: `editorial`
- Language: `it`

---

## Content Authoring Tips

- **Concise beats complete.** Ruthlessly cut filler. The slide is a prompt for speech, not a transcript.
- **One claim per bullet.** If a bullet needs a sub-bullet, that sub-bullet is probably its own slide.
- **Code examples.** Include only the minimal snippet that proves the point. Strip imports and boilerplate.
- **Diagrams.** ASCII/monospace diagrams work well. Label the box with a `diagram` tag in the corner.
- **Images.** Use inline SVG or base64 data URIs to keep the file self-contained.
- **Math.** If needed, load KaTeX from cdnjs for LaTeX rendering.

---

## Quality Checklist

- [ ] Single HTML file, zero broken external dependencies
- [ ] Keyboard navigation: ← → Space ESC all work
- [ ] Slide counter visible (monospace, bottom-left)
- [ ] Progress bar fills correctly
- [ ] Sidebar opens/closes, active slide highlighted
- [ ] Grain overlay present (subtle, not distracting)
- [ ] Transitions ≤ 0.5s, no layout jumps
- [ ] Left decorative bar visible on section slides
- [ ] Title slide and closing slide are distinct from section slides
- [ ] File size < 5MB (no external images embedded)
- [ ] Readable at 1280px+ desktop width

---

## Customization After Generation

The easiest things to tweak post-generation:

```css
/* Change accent color globally */
:root { --accent: #your-color; }

/* Adjust font size for projector (larger room) */
li { font-size: 22px; }

/* Disable grain overlay */
body::after { display: none; }
```