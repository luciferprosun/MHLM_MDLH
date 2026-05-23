# gptme adaptation plan for codex_clone

Date: 2026-05-18
Reference repo: /mnt/lsc_data/AI_WORKSPACE/repos/gptme_reference
Target app: /home/l/APP2/codex_clone

## Goal
Use gptme as an engineering reference, not as a drop-in dependency. The local app must stay small, Linux-terminal-first, safe, and beginner-maintainable.

## What gptme does well
- Tool registry: tools are described, loaded, and dispatched independently.
- Slash commands: /model, /tools, /context are handled locally without LLM calls.
- Provider layer: model/provider selection is separate from the runtime loop.
- Shell safety: allowlist for read-only/simple commands, denylist for destructive commands, confirmation hook for risky actions.
- File editing: separate save/append/patch tools instead of relying on shell redirection.
- Context control: shell output is truncated/summarized before going back to the model.
- Browser tooling is a first-class tool, not a chat hack.

## What not to import from gptme
- Full server/web UI/ACP/Tauri architecture.
- Docker/computer-use heavy components.
- Plugin/MCP complexity for the first local MVP.
- Full markdown tool-call parser unless we decide to switch away from JSON actions.
- Full context compression machinery until the app has real long-session pressure.

## Current codex_clone status
- Already has JSON action format.
- Already has shell, filesystem, browser, validator, memory, executor modules.
- Already handles URL bootstrap locally before Gemini.
- Tests pass after the current startup fix.
- Still too Gemini-centric for simple local tasks.
- /model exists only as a local status message, not a real provider switch.

## Recommended rebuild order

### Phase 1: Local command registry
Create a small commands/ package:
- commands/base.py
- commands/status.py
- commands/model.py
- commands/tools.py
- commands/help.py

Purpose:
- /status, /model, /tools, /help must never call Gemini.
- User meta-questions like "czy mozesz otwierac linki" should be handled locally.

### Phase 2: Provider abstraction
Create providers/ package:
- providers/base.py
- providers/gemini_provider.py
- providers/openai_provider.py
- providers/openrouter_provider.py
- providers/config.py

Purpose:
- /model shows current provider/model.
- /model gemini/gemini-2.5-flash switches Gemini.
- /model openai/gpt-4.1-mini or configured OpenAI model switches provider later.
- API keys stay in ~/.config/* and are never committed/zipped.

### Phase 3: Local intent router before LLM
Create router/local_router.py.

It should handle obvious tasks without Gemini:
- status/help/model/tools
- open a raw URL
- unwrap Facebook redirect URL
- create folder when command is explicit and simple
- write/read files only when path and content are explicit
- pwd/ls/date/curl --version

Rules:
- Keep it conservative.
- If uncertain, ask LLM.
- Do not build huge regex spaghetti.
- Each local route must return the same action schema used by executor.

### Phase 4: Tool registry
Replace if/elif dispatch in executor with a registry:
- tool name
- schema/required fields
- handler
- safety mode
- description

Keep current tool modules, but register them cleanly.

### Phase 5: Safety model upgrade
Adopt gptme-like policy:
- safe allowlist auto-executes
- advanced requires confirmation
- dangerous blocks or requires explicit typed confirmation
- quoted strings should not trigger false positives
- redirection should be advanced unless using filesystem tools

### Phase 6: Context/token control
Reduce prompt size:
- include only active tools, not all examples every step
- send last N outputs, truncated by type
- summarize large browser text locally before model
- avoid repeated full system prompt when possible

### Phase 7: Tests
Add required tests:
- /status calls no model
- URL open calls no model until analysis step
- simple folder creation can be local or uses one model call max
- write_file does not use shell redirection
- /model switches provider config without API leak
- quota error preserves completed local actions

## Engineering decision
Use gptme as architecture reference, but keep codex_clone JSON-action-native and small.
