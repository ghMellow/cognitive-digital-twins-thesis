# Skill: OCR Execution Protocol (GLM-OCR)
Description: Strict operational protocol for local PDF-to-Markdown conversion using Ollama. Acts as an executor bridge. NO development allowed.

## 1. PRE-FLIGHT VALIDATION
- Verify Ollama service: `curl -s http://localhost:11434/api/tags | grep "glm-ocr"`.
- If service is OFF: Stop immediately and alert the user to start Ollama.

## 2. SMART PATH DETECTION (PRIORITY)
Before asking any questions, the agent MUST parse the user's prompt for any folder structure or path pattern (e.g., `raw/papers/...`, `/<path>/<papername>`).
- **IF a path is found in the prompt:** Set it as `TARGET_DIR` automatically. DO NOT ASK.
- **IF NO path is found:** Stop and ask: *"Where should I save the converted files for [filename]? (e.g., current directory, a specific folder, or create a new subfolder)"*.
- **WORKSPACE PREP:** Ensure the `TARGET_DIR` exists: `mkdir -p "${TARGET_DIR}"`.

## 3. CONVERSION PIPELINE (OPERATOR MODE)
- **Image Extraction:** Convert PDF pages to images in `/tmp/ocr_pages/` using `pdftoppm` (poppler) or a one-off Python script with `pdf2image`.
- **OCR API Call:** For each page, send a POST request to `http://localhost:11434/api/generate`:
  - Model: "glm-ocr"
  - Prompt: "Convert image to clean Markdown. Output only the content, no talk."
  - Stream: false
- **Consolidation:** Merge all page outputs into a single Markdown string.

## 4. FILE & WORKSPACE FINALIZATION
- **Identical Naming:** Save the result to `${TARGET_DIR}/${base_name}.md`. The filename MUST be identical to the original PDF.
- **Strict Move:** Use the `mv` command to move the original PDF into `${TARGET_DIR}/`. 
  - *CRITICAL:* The PDF must be REMOVED from the source location and exist only in the target folder. No duplicates.
- **Cleanup:** Delete the `/tmp/ocr_pages/` directory and its contents immediately after success.

## 5. MANDATORY RULES (ZERO TOLERANCE)
1. **NO PROGRAMMING:** DO NOT suggest, write, or build a Web App, a GUI, or a permanent tool. You are an OPERATOR executing a task, not a DEVELOPER building a project.
2. **LOCAL ONLY:** No data must leave the local machine.
3. **USE SYSTEM TOOLS:** Use `curl`, `mv`, `mkdir`, and `pdftoppm` for orchestration.
4. **NO ASSUMPTIONS:** If the user hasn't specified a path, you are FORBIDDEN from choosing one automatically. You must ask.