# WhiteboardIQ

A [Google AI Edge Gallery](https://github.com/google-ai-edge/gallery) agent skill that reads a whiteboard photo and extracts every action item, decision, and open question into a structured visual summary card — with voice narration.

## What it does

Point your camera at a whiteboard after a meeting and ask the on-device Gemma model to analyse it. The skill returns a rich card showing:

- **Action items** — task, owner, deadline, and priority (High / Medium / Low) with colour-coded indicators
- **Decisions** — every decision recorded on the board
- **Open questions** — blockers and unresolved items
- **Voice narration** — tap ▶ Play to have the summary read aloud; pause and resume at any time

All inference runs on-device. No photo leaves your phone.

## How to load it

1. Open the **AI Edge Gallery** app on Android or iOS.
2. Go to **Agent Skills → Load from URL**.
3. Enter:
   ```
   https://github.com/samirzubair/GEMMA4
   ```
4. The skill appears in your skill list immediately.

## Usage examples

- "Analyse this whiteboard"
- "Extract action items from this photo"
- "Who owns what from this meeting?"
- "Turn this whiteboard into action items"

## Repository structure

```
SKILL.md              ← skill metadata and LLM instructions
scripts/
  index.html          ← ai_edge_gallery_get_result entry point
assets/
  webview-v2.html     ← visual summary card UI with voice narration
  webview.html        ← original UI (kept for reference)
```

## Tech stack

- **Gemma 4** running on-device via [Google AI Edge](https://ai.google.dev/edge)
- **LiteRT** for optimised model execution
- **Web Speech API** for voice narration
- **GitHub Pages** for hosting the webview assets

## License

Apache 2.0
