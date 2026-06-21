# Itinerary Quiz

Conduct the following quiz to build the story itinerary using the **opencode `question` tool** — **always** use it. The first question uses an **empty `options` array** (the "Type your own answer" field is added automatically by the tool) so the user types the map name freely. The user stops the quiz manually when done.

## Loop

Each step uses a **single `question` tool call with three questions** (three entries in the `questions` array). Before prompting, remind the user of the **current difficulty** — this is always the **last NUMERIC difficulty** (skipping any `-` steps), or `none` if no numeric difficulty has been set yet. Showing `-` here is not useful since it doesn't convey the point in the game; the numeric curve is what matters.

1. **Map name** — `options: []` (free text only via the auto-added "Type your own answer" field; no brackets, no preset name).

2. **Type** (single-select). Options (exactly as specified):
   - **Standard map** — Insert next map (Requirement = `-`).
   - **Unlocked by MN01 (Cut)** — Requirement = `Cut`.
   - **Unlocked by MN03 (Surf)** — Requirement = `Surf`.
   - **Unlocked by MN04 (Strength)** — Requirement = `Strength`.
   - **Unlocked by MN06 (Whirlpool)** — Requirement = `Whirlpool`.
   - **Unlocked by MN07 (Waterfall)** — Requirement = `Waterfall`.
   - **Unlocked by MT08 (Rock Smash)** — Requirement = `Rock Smash`.

3. **Difficulty** (single-select — "Type your own answer" available by default for custom values):
   - **Current: \<value\>** — accept the last **NUMERIC** difficulty (skipping `-` steps). Omit when no numeric difficulty has been set yet.
   - **Bump by 1** — increment the last numeric difficulty by 1.
   - **`-`** — no difficulty (for cities or maps gated behind a future unlock).

   The selected value becomes the map's difficulty. The **last numeric difficulty** is updated to the selected value if and only if it is numeric (i.e. a `-` selection does not clear or change the tracked last-numeric value — that value is preserved from the most recent numeric step).

4. From the answers, determine: **Map** (Q1), **Type** and **Requirement** (Q2), **Difficulty** (Q3).

5. Append an entry to `ITINERARY.md`:

   ```markdown
   ## Step N

   - **Map**: <name>
   - **Requirement**: <HM/move or `-`>
   - **Difficulty**: <integer> or `-`
   ```

6. Increment the step counter and return to step 1.

## Notes

- The user may rename or re-order steps later; the format above is the canonical shape.
- The user owns the difficulty curve — the quiz does not enforce monotonicity, only reminds the user of the current value.
- Trainers are not configured by this quiz — only their reference difficulty.
- When editing a step in the middle of the list, show context: the **precedent step's** difficulty and the **following step's** difficulty if any. For context, use the **last numeric** difficulty (skipping `-`) on each side, so the user sees the numeric curve.
