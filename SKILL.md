---
name: whiteboard-iq
description: Analyse a whiteboard photo and extract structured action items, decisions, and open questions into a visual summary card.
metadata:
  homepage: https://github.com/samirzubair/GEMMA4
---

# WhiteboardIQ

This skill reads a whiteboard image and extracts every action item, decision, and open question into a structured visual summary card.

## Examples

* "Analyse this whiteboard"
* "Extract action items from this photo"
* "What are the tasks on this whiteboard?"
* "Turn this whiteboard into action items"
* "Read the whiteboard and give me a summary"
* "Who owns what from this meeting?"

## Instructions

When the user shares a whiteboard image or asks you to analyse one, carefully read every piece of text visible on the whiteboard. Then call the `run_js` tool using `index.html` and a JSON string for `data` with the following fields:

- **meeting_context**: String. A short title describing what this whiteboard session was about.
- **summary**: String. A 2-3 sentence plain-English executive summary of the whiteboard.
- **action_items**: Array of objects, each with:
  - id: Number. Sequential starting from 1.
  - task: String. Clear description of the task.
  - owner: String. Person's name visible near the task, or "Unassigned".
  - deadline: String. Any date or time reference visible, or "No deadline".
  - priority: String. Exactly "High", "Medium", or "Low". Circled or starred = High, boxed = Medium, plain = Low.
  - notes: String. Any extra context. Empty string if none.
- **decisions**: Array of strings. Each decision recorded on the whiteboard.
- **questions**: Array of strings. Open questions or blockers noted on the whiteboard.

DO NOT fabricate tasks, owners, or deadlines not visible on the whiteboard.
DO NOT use `run_intent`. DO NOT call any other tool.

After returning the result, say: "Found X action items across Y owners."
