# 03.01 — Command Palette, search, symbols, and platform shortcuts
- [Overview](#overview)
  - [interactive-navigation-lab](https://sbhrwl.github.io/cursor/editor-fluency/03-01-CommandPaletteSearchSymbols/interactive-navigation-lab.html)
- [Starting point](#starting-point)
- [Choose a tool by the question](#choose-a-tool-by-the-question)
- [Repeat the filmed investigation](#repeat-the-filmed-investigation)
- [Common reference shortcuts](#common-reference-shortcuts)
- [Files](#files)
## Overview
- By the end, trace a behavior from its implementation to the server that uses it and a specific test assertion, while preserving the working copy.
## Starting point
- Use the fresh clone from lesson 02.06, or clone that lesson's supplied `operations-hub-starter.bundle` for offline practice.
- Open the repository root in Cursor and install its documented dependencies so TypeScript language support has the project context.
- The filmed installation is Cursor 3.19.13 on Linux.
- The recorded GitHub revision is `b11a543939b6c760e45af5b1c78157373a4cdbec`.
  - The supplied offline bundle has separate practice history and its own commit ID.
## Choose a tool by the question

| What you know | Tool | What to inspect |
|---|---|---|
| An action name | Command Palette | Exact command label; similar JSON commands open different views |
| A filename or path | Quick Open | Matching path and breadcrumb |
| Text in the active file | Find | Match options and surrounding control flow |
| Text somewhere in the workspace | Search | Open root, include/exclude filters, match options, results grouped by file |
| A function in the current file | Go to Symbol in Editor | Recognized language symbols |
| A use of a symbol | Go to Definition | Resolved declaration/implementation location |
| A symbol's relationships | References | Each location; declaration may be included |

## Repeat the filmed investigation
- Open Command Palette and search `Keyboard Shortcuts`.
  - Select **Preferences: Open Keyboard Shortcuts**, without a JSON suffix.
  - In that page, search `Go to Definition`; inspect the keybinding and its `When` condition.
- Use Quick Open to open `src/handler.ts`.
- Find `Cache-Control`.
  - In this version, one match sets `no-store` at line 15 inside the `/health` condition.
- Search the workspace for `createHandler`.
  - The filmed scope returns five text matches in three files.
- Include `src/**`; this returns three matches in two source files.
  - Clear the include field to restore the test results.
  - Confirm other filters if your results differ.
- Focus the handler editor.
  - Use Go to Symbol in Editor to locate `createHandler` at line 10.
- Open `src/server.ts`, place the caret on `createHandler` at line 5 and invoke Go to Definition.
  - Inspect the resolved function.
- Invoke References at that definition.
  - The filmed TypeScript view shows five locations, including its declaration.
  - Expand the test file to inspect its use.
- Open `test/health.test.ts` and find `cache-control`.
  - The healthy GET case asserts `no-store` at line 38.
  - Read the setup at lines 29–35 and the actual assertion together.
- Check Source Control and download an evidence map from the accompanying HTML lab.
  - Keep the checkout unchanged.
- Finding a test is not running it.
  - Lesson 02.06 ran the six HTTP handler tests; this lesson focuses on navigating and reading their evidence.
  - Text matches are not runtime invocation counts, and a filtered search cannot establish absence of coverage.
## Common reference shortcuts

| Command | Linux / Windows | macOS |
|---|---|---|
| Command Palette | Ctrl+Shift+P | Cmd+Shift+P |
| Quick Open | Ctrl+P | Cmd+P |
| Find in active file | Ctrl+F | Cmd+F |
| Search workspace | Ctrl+Shift+F | Cmd+Shift+F |
| Go to Symbol in Editor | Ctrl+Shift+O | Cmd+Shift+O |
| Go to Definition | F12 | F12 |
| References | Shift+F12 | Shift+F12 |

- Linux behavior was verified in the recorded Cursor installation.
  - Windows and macOS are reference defaults.
  - Inspect the installed bindings; Cursor customizations, extensions, remapping, layout and focus can change behavior.
  - Laptop function keys may require Fn.
  - Current documentation and the installed keyboard-settings chord differ, so use the palette to discover the command by name.
- If symbol navigation fails, check the active language, language support, dependency installation and project configuration.
- If a key opens a different feature, inspect its command binding and focus condition.
- If a file is absent from search, check scope and exclusions before drawing conclusions.
- The symbol picker's `@` prefix is editor navigation; agent-chat context mentions serve a different purpose.
## Files
- [interactive-navigation-lab.html](https://sbhrwl.github.io/cursor/editor-fluency/03-01-CommandPaletteSearchSymbols/interactive-navigation-lab.html)
- [practice.md](practice.md)
- [evidence-map-template.md](evidence-map-template.md)
- [observed-navigation-evidence-map.md](observed-navigation-evidence-map.md)
- [operations-hub-starter.bundle](operations-hub-starter.bundle)
- [PROMPTS.md](PROMPTS.md)
- [narration-script.md](narration-script.md)
  - [03-01-command-palette-search-symbols-and-platform-shortcuts.en.srt](03-01-command-palette-search-symbols-and-platform-shortcuts.en.srt)
- [sources-and-credits.md](sources-and-credits.md)
- [chapters.json](chapters.json)
