# SKILL-apple-presentation — Interactive HTML Presentation Generator

**Purpose:** Transform any markdown or text content into an elegant, interactive HTML presentation with full keyboard navigation and Apple Design System aesthetics.

**When to use:** When you need to create a professional, single-file presentation from thesis materials, research summaries, or technical deep-dives.

---

## Prompt Template

```
You are an expert Frontend Developer and UI Designer. Your task is to transform the [TEXT] provided into an elegant, interactive single-page HTML presentation with full functionality.

**Technical Requirements:**
1. **Structure:** Generate a single, self-contained HTML file (CSS and JS included in <style> and <script> tags). Each slide must be a <section> element occupying 100% of the viewport.

2. **Interactivity:** Implement keyboard navigation:
   - Right Arrow / Space / Down Arrow: Next slide
   - Left Arrow / Up Arrow: Previous slide
   - Smooth fade-in/out or horizontal scroll transition between slides
   - Display current slide number (e.g., "3 / 12") in bottom-right corner
   - Auto-hide controls after 3 seconds of inactivity, show on mouse movement or key press

3. **Design (Apple Style):**
   - **Colors:** Pure white background (#FFFFFF), Apple black text (#1D1D1F). Use Apple blue (#0066CC) only for key terms, links, or icons.
   - **Typography:** System sans-serif fonts (San Francisco, -apple-system, Helvetica Neue, Arial). Large titles (60-80px), readable body text (18-24px), generous line-height (1.6+).
   - **Layout:** Extreme minimalism. Abundant whitespace. Center or left alignment with generous margins (80px+).
   - **Details:** Elegant bullet points as thin horizontal lines or minimal icons. Code blocks with subtle gray background (#F5F5F7).
   - **Animations:** Smooth transitions, no jarring effects. Fade duration 0.4s.

4. **Content Structure:** Analyze the provided text and divide it logically into slides:
   - Title slide (with subtitle if applicable)
   - Section headers as new slides
   - Key points as bullet-based slides
   - Code or examples as dedicated slides
   - Concluding/summary slide

5. **Optional Enhancements:**
   - Add a collapsible left sidebar with slide index, clickable to jump to any slide
   - Display total slide count
   - Add visual slide indicator dots at the bottom

**Content to Transform:**
[INSERT_TEXT_HERE]

Output ONLY the complete HTML file, ready to save and open in any browser.
```

---

## Workflow Steps

1. **Copy the prompt above**
2. **Replace [INSERT_TEXT_HERE] with your markdown/text content**
3. **Paste into your LLM (Claude, GPT-4, etc.)**
4. **Save the HTML output as `presentation.html`**
5. **Open in browser (Chrome, Safari, Firefox)**
6. **Navigate with keyboard: arrow keys, space, or mouse click**

---

## Example Usage

```bash
# 1. Prepare your content (markdown or plain text)
cat raw/project/approfondimenti/your-file.md

# 2. Feed it through the prompt (copy-paste or piped)
# 3. Save the generated HTML
# 4. Open locally
open presentation.html
```

---

## Best Practices

- **Content:** Keep text concise. Aim for 5-8 bullet points per slide maximum.
- **Images:** If referencing images, use inline SVG or base64-encoded data URIs (keeps file self-contained).
- **Formulas:** Use KaTeX or MathJax if mathematical notation is needed.
- **Customization:** After generation, edit the `<style>` section to adjust colors, fonts, or sizing.
- **Sharing:** The `.html` file is self-contained — email it, share it, open it offline anywhere.

---

## Quality Checklist

- [ ] Single HTML file, no external dependencies
- [ ] Keyboard navigation works smoothly
- [ ] White background, black text (Apple style)
- [ ] Slide counter visible (e.g., "3 / 12")
- [ ] Transitions are smooth (<0.5s)
- [ ] Content is readable on desktop (1080p+)
- [ ] File size <5MB (typical for non-image-heavy presentations)
