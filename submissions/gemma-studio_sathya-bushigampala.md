# GemmaStudio

## Team / attendee

- Team name (if applicable): GemmaStudio Team
- Members and GitHub usernames: Sathya Bushigampala (@SathyaBushigampala)
- Profile links (optional): https://github.com/SathyaBushigampala

## Challenge

Select the challenge you are entering:

- [ ] Best Open-Source AI Project
- [x] Best Use of Gemma 4

If listing both categories, confirm eligibility with the organizers and complete evidence for each.

## Project links

- Public GitHub repository: https://github.com/SathyaBushigampala/GemmaStudio
- Open-source license (link to the license file): https://github.com/SathyaBushigampala/GemmaStudio/blob/main/LICENSE

## Problem and solution

Running open-weights models like Gemma locally typically requires dedicated high-end server-grade GPUs (16GB–64GB VRAM), complex CUDA/PyTorch configurations, and hours of setup. 

GemmaStudio solves this barrier completely by providing a developer-focused, full-stack web playground and studio designed specifically for Google's Gemma 4 open-weights models hosted directly on the Google Gemini API with zero local GPU requirements.

**Main input → output workflow:**
1. The user inputs prompts, system instructions/personas, optional image uploads, and configures reasoning levels (High / Minimal).
2. The Flask backend interfaces directly with Google's cloud-hosted Gemma 4 endpoints via the official `google-genai` SDK.
3. GemmaStudio cleanly separates and visualizes the model's internal thinking process tokens (`part.thought == True`) from final response tokens, displays multimodal analysis, provides live token latency, and features an Experiment Studio with automated AST code verification.

## Approach and technologies

- **AI SDK & Models:** Official `google-genai` SDK (v2.29.0) communicating with hosted `gemma-4-26b-a4b-it` (MoE) and `gemma-4-31b-it` (Dense).
- **Backend:** Python 3.14 / Flask 3.1.3, Werkzeug, Pillow (safe in-memory image validation capped at 10MB), and Python `ast` for static code syntax verification.
- **Frontend:** Vanilla JavaScript (ES6+), HTML5, CSS3, `DOMPurify 3.0.8` (strict XSS sanitization), `marked.min.js`, and `highlight.js`.
- **Security & Reliability:** Masked API keys, CSRF-safe headers, 16MB maximum payload limit, and strict path validation for session storage.

## Challenge evidence

Complete the relevant section(s) and remove those that do not apply.

### Best Use of Gemma 4

- Gemma 4 model identifier and Gemini API integration:
  - Models: `gemma-4-26b-a4b-it` (26B MoE, default) and `gemma-4-31b-it` (31B Dense reasoning).
  - Integration: Uses `google-genai` SDK (`from google import genai; from google.genai import types`) with `client.models.generate_content`.
- Code link showing the integration: https://github.com/SathyaBushigampala/GemmaStudio/blob/main/app.py
- Input and useful output; multimodal value where applicable:
  - **Thinking Mode Telemetry:** Captures Google's internal chain-of-thought tokens (`part.thought == True`) distinctly from final answer tokens and surfaces them in an interactive accordion.
  - **Multimodal Vision:** Safely parses, validates, and serializes image uploads to base64 `types.Part.from_bytes` payloads for visual reasoning and debugging.
  - **Experiment Studio & Benchmarks:** Built-in benchmarking suite running math reasoning, algorithmic code generation, and multimodal vision QA against live endpoints with real latency telemetry.

## Current status

- What works:
  - Hosted Gemma 4 chat generation (`gemma-4-26b-a4b-it` and `gemma-4-31b-it`).
  - Separation and rendering of internal thinking tokens vs final output.
  - Multimodal image upload and analysis.
  - System persona presets (Kyoto Tea Master, Senior Code Architect, Math & Proofs Tutor).
  - Multi-language export (Python, JavaScript, cURL).
  - Experiment Studio automated benchmarks, AST validation, and report exports (Markdown/JSON).
  - Full automated unit test suite passing (9 tests).
- Known limitations / incomplete features:
  - Streaming responses currently aggregate per-candidate tokens in the studio view.
- What you would improve next:
  - WebSocket / SSE streaming for real-time token-by-token typewriter rendering.
  - Additional pre-configured benchmark datasets and expanded multimodality with audio/video.

## Submission checklist

- [x] Project repository is public and links work.
- [x] Required challenge evidence is included.
- [x] Project uses an open-source license where required by the challenge.
- [x] Work and reused materials are represented honestly.
- [x] No API keys, tokens, passwords, or private data are included.
- [x] I followed the organizers' build window and submission instructions.
