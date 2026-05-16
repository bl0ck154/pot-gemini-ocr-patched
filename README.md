# Pot Gemini OCR patched plugin

Patched Pot App text recognition plugin for Google Gemini OCR.

## Install

If you already have the packaged `.potext` file, install it directly in Pot:

```text
Pot -> Preferences/Config -> Service Settings -> Text Recognition/Recognize/OCR -> Add External Plugin -> Install Plugin
```

Select:

```text
plugin.gemini-ocr-updated.potext
```

Then fully quit Pot from the system tray and start it again.

If Pot refuses to update the existing plugin because the plugin id is the same:

```text
1. Remove or disable the old Gemini OCR plugin in Pot.
2. Quit Pot from the system tray.
3. Start Pot again.
4. Install plugin.gemini-ocr-updated.potext.
```

## Build `.potext` from source

Download or clone this repository with these files:

```text
info.json
main.js
README.md
```

Also copy `gemini.svg` from the original plugin package/repository.

Create a zip archive with this exact root-level structure:

```text
info.json
main.js
gemini.svg
README.md
```

Do not put the files inside a parent folder in the archive.

Rename the archive from:

```text
plugin.zip
```

to:

```text
plugin.gemini-ocr-updated.potext
```

Install that `.potext` file in Pot as described above.

This version fixes the original plugin defaults and UI labels:

- English settings labels instead of Chinese-only labels.
- Default Gemini Developer API base URL.
- Streaming disabled by default for simpler OCR response parsing.
- OCR-focused prompt that preserves original language and formatting.
- `gemini-3.1-flash-lite` as the current fast default model from Google's API sample and `ListModels`.
- Presets generated from `ModelService.ListModels` results for a Gemini Developer API key on 2026-05-16.
- Custom model support that accepts either `gemini-*` or `models/gemini-*`.

## Recommended settings

```text
API Base URL: https://generativelanguage.googleapis.com/v1beta
Model preset: Custom model name (recommended)
Custom model name: gemini-3.1-flash-lite
Streaming output: No (recommended)
System Prompt: empty
Temperature: 0
Top P: 0.95
Thinking budget: empty
Extra generationConfig JSON: {"thinkingConfig":{"thinkingLevel":"MINIMAL"}}
```

OCR prompt:

```text
Extract all visible text from the image exactly as written. Preserve the original language, alphabet, punctuation, line breaks, and casing. Do not translate. Do not explain. Return only the recognized text.
```

## Check available models for your API key

Google model availability depends on your API key, region, account, and API version.

Open this URL after replacing `YOUR_API_KEY`:

```text
https://generativelanguage.googleapis.com/v1beta/models?key=YOUR_API_KEY
```

Use a model whose `supportedGenerationMethods` includes `generateContent`.

The preset list in this patch is intentionally small. It avoids preview models and duplicate versioned aliases unless they are useful for OCR:

```text
gemini-3.1-flash-lite
gemini-flash-latest
gemini-flash-lite-latest
gemini-pro-latest
gemini-2.5-flash
gemini-2.5-flash-lite
gemini-2.5-pro
gemini-2.0-flash
gemini-2.0-flash-lite
gemini-2.5-flash-image
```

If the returned model name is `models/gemini-3.1-flash-lite`, you can paste either of these into the plugin:

```text
gemini-3.1-flash-lite
models/gemini-3.1-flash-lite
```

The plugin strips the `models/` prefix automatically.

## Notes

Do not enable Google Search tools for OCR. Search grounding is not needed for reading text from screenshots and may increase latency or quota usage.
