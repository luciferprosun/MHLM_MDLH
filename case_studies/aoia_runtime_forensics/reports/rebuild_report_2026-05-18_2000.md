# codex_clone rebuild report

Date: 2026-05-18
Reference architecture: gptme-style local commands, provider layer, tool registry

## Savepoints
- Before rebuild: /mnt/lsc_data/AI_WORKSPACE/backups/codex_clone_savepoints/codex_clone_before_rebuild_20260518_195134.tar.gz

## Major changes

### 1. Local commands layer
Added:
- commands/base.py
- commands/local_commands.py

Implemented local slash commands that do not call the model:
- /status
- /model
- /model NAME
- /tools
- /help

### 2. Provider abstraction
Added:
- providers/base.py
- providers/config.py
- providers/gemini_provider.py
- providers/openai_compatible.py

The runtime now talks to ProviderManager instead of directly hardcoding Gemini in main.py.
Supported provider names:
- gemini/...
- openai/...
- openrouter/...

Provider loading is lazy. Local commands can run even if an API key is missing or the model provider is unavailable.

### 3. Local router before LLM
Added:
- router/local_router.py

Handled locally without model calls:
- help/pomoc
- status
- model
- date questions
- pwd
- ls/list files
- curl --version
- simple desktop folder creation
- link capability questions

### 4. Executor tool registry
Refactored tools/executor.py from a long if/elif dispatcher into a tool registry.
This keeps the current JSON action format but makes new tools easier to add.

### 5. Token-saving behavior
The app now avoids Gemini for:
- slash commands
- plain help/status/model prompts
- simple desktop folder creation
- simple local shell queries like pwd/ls/curl version
- URL browser bootstrap before analysis

Gemini is still used for ambiguous planning, multi-step reasoning, and final interpretation.

## Tests
Final full test suite:
- 14 tests
- 14 passed

Commands run:
- python py_compile on main.py, commands, providers, router, tools, tests
- unittest discover -s tests -v

## Known limitations
- Local router is intentionally conservative; ambiguous tasks still go to the model.
- /model switches provider config, but real OpenAI/OpenRouter calls require local API key files.
- Browser tests require running outside Codex sandbox because Chromium sandboxing fails inside the tool sandbox.
- Old patch helper files still exist in the project root and should be cleaned in a later maintenance pass.
