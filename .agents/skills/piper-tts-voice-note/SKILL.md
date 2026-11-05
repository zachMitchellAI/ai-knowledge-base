---
name: piper-tts-voice-note
description: Render a markdown/text file into spoken audio (wav/mp3) with local Piper TTS on aibox and deliver it to the owner (e.g. attach to Matrix)
---

# Piper TTS Voice Note

Render a document as spoken audio using **local** Piper TTS (no cloud, no API keys, no cost),
optionally deliver the file to the owner over Matrix. Works on aibox (piper-tts 1.8.0 package).

## Pipeline overview

```
markdown file → strip to TTS-friendly text (md-to-tts-stripped rules) → piper-tts → .wav
             → (optional) ffmpeg → .mp3 → deliver via MEDIA: line (Matrix/voice chat)
```

## Prerequisites (verified live 2026-11-05)

- Binary: `/usr/bin/piper-tts` (package `piper-tts`; note the binary is NOT named `piper`)
- Converter: `/usr/bin/ffmpeg` (system package, present)
- Voice models: `~/.local/share/piper/voices/` — one `.onnx` + matching `.onnx.json` per voice.
  **Check this directory first** and use a voice that's already there (only `en_US-lessac-medium`
  is pre-installed, ~63 MB); download others only if the user asks for a specific voice:
  `https://huggingface.co/rhasspy/piper-voices/resolve/v1.0.0/en/en_US/<name>/<quality>/<name>-<quality>.onnx`
  (and `.onnx.json`) into that directory. The espeak-ng-data dependency is bundled with the
  package — no separate setup needed.

## Steps

1. **Prepare the text.** Apply the `md-to-tts-stripped` skill's rules to the source markdown
   (headers → `Title:`, strip `#`/`*`/links/tables → verbalized rows, lists → comma lists).
   Write the result to a temp `.txt` file. Read the whole file first — do not feed raw markdown to piper.
   For a *recently created* file, confirm with the user which file is meant if the cwd is ambiguous.
2. **Generate the wav:**

   ```bash
   /usr/bin/piper-tts \
     -m ~/.local/share/piper/voices/en_US-lessac-medium.onnx \
     -f /tmp/<name>.wav \
     -i /tmp/<name>.txt
   ```

   Useful knobs: `--length-scale` (higher = slower, e.g. 1.1 for dense docs), `--sentence-silence 0.6`
   (extra pause between sentences), `--volume 1.5`. Output is 16-bit mono 22050 Hz PCM.
3. **Optional mp3** (much smaller for Matrix — roughly 1/6 the size):

   ```bash
   ffmpeg -y -i /tmp/<name>.wav -codec:a libmp3lame -qscale:a 4 /tmp/<name>.mp3
   ```

   Default to mp3 for delivery unless the user asked for wav.
4. **Sanity-check before delivering:** file exists and is non-trivial in size
   (rough rule: ≥ ~20 KB of wav per sentence of input; a suspiciously small file means empty input text).
   Optionally run `ffprobe` to confirm duration looks proportional to the text length.
5. **Deliver (conditional on environment).**
   - **On OpenClaw:** include the file on its own line in the target chat:
     ```
     MEDIA:/path/to/<name>.mp3
     ```
   - **Outside OpenClaw** (plain CLI/other harness, no messaging tools available): skip the
     MEDIA step entirely — just generate the file and tell the user the output path. The
     audio file itself is the deliverable; do not assume a chat attachment mechanism exists.
   Keep the spoken/text reply short and say what the audio contains and its approximate length.
6. **Cleanup:** remove the temp `.txt`; keep the audio only if the user wants a copy
   (default: deliver then delete the temp, since the source doc remains).

## Notes and gotchas

- Long documents: piper handles long inputs fine, but for a 30+ minute read consider chunking and
  delivering multiple files, or warn the user about size first. Confirm before generating anything huge.
- Piper voices are all local — this costs zero tokens and zero API spend. The only token cost is the
  LLM's own stripping pass over the markdown.
- `--input-raw`/`--output-raw` exist for streaming; not needed for file-based delivery.
- If `piper-tts` errors with `No such file or directory` on a model, the voice files are missing —
  re-check the download step, not the binary.
- **Voice location on Arch:** check `/usr/share/piper/voices/` first (system-package voices) and
  use one from there if present; if none exist, download a voice from HuggingFace per the
  Prerequisites section.
