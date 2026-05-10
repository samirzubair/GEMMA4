---
name: whiteboard-iq
description: Analyse a whiteboard photo and extract structured action items, decisions, and open questions into a visual summary card.
metadata:
  homepage: https://github.com/google-ai-edge/gallery/tree/main/skills/featured/whiteboard-iq
---

# WhiteboardIQ

This skill reads a whiteboard image provided by the user and extracts every action item, decision, and open question into a structured, visual summary card.

## Examples

- "Analyse this whiteboard"
- "Extract action items from this photo"
- "What are the tasks on this whiteboard?"
- "Turn this whiteboard into action items"
- "Read the whiteboard and give me a summary"
- "Who owns what from this meeting?"

## Instructions

When the user shares a whiteboard image or asks you to analyse one, carefully read every piece of text visible on the whiteboard. Then call the `run_js` tool with the following exact parameters:

- data: A JSON string with the following fields:
  - meeting_context: String. A short title describing what this whiteboard session was about (e.g. "Sprint planning", "Q3 roadmap").
  - summary: String. A 2-3 sentence plain-English executive summary of the whiteboard.
  - action_items: Array of objects, each with:
    - id: Number. Sequential starting from 1.
    - task: String. Clear description of the task.
    - owner: String. Person's name visible near the task, or "Unassigned".
    - deadline: String. Any date or time reference visible (e.g. "EOW", "Friday", "Next sprint"), or "No deadline".
    - priority: String. Must be exactly "High", "Medium", or "Low". Infer from visual cues — circled, starred, or underlined text = High; boxed text = Medium; plain text = Low.
    - notes: String. Any sub-tasks or extra context. Empty string if none.
  - decisions: Array of strings. Each decision visibly recorded on the whiteboard.
  - questions: Array of strings. Open questions or blockers noted on the whiteboard.

Priority rules:
- Text that is circled, starred (*), underlined, or marked URGENT = High
- Text inside a box or rectangle = Medium
- Plain unmarked text = Low
- A name written directly beside or below a task = that person is the owner

DO NOT fabricate tasks, owners, or deadlines that are not visible on the whiteboard.
DO NOT use `run_intent`.
DO NOT call any other tool.

After returning the skill result, give a one-line summary such as: "Found X action items across Y owners."
