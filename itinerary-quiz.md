# Itinerary Quiz

Conduct the following quiz to build the story itinerary. Repeat the loop until the user selects **Stop**.

## Loop

1. Ask a multi-answer question with these options:
   - **Insert next map** — add a map to the itinerary (routes, cities, etc.)
   - **Unlock MN map** — unlock a map previously inaccessible due to a missing requirement (e.g. a Hidden Machine like Surf)
   - **Stop** — finish the quiz

   Use the `question` tool with `multiple: true`. Always include **Stop** in the list. If the user picks **Stop** alongside other options, treat it as terminating the quiz and discard the other selections.

2. For each map selected (in the order the user listed them), ask (single free-text prompt):
   ```
   Map: <name> | Requirement: <HM/move or `-`> | Difficulty: <integer or `-`>
   ```
   - **Map**: name/identifier (free text).
   - **Requirement**: only for "Unlock MN map" picks — e.g. `Surf`, `Cut`, `Strength`, `Waterfall`, `Flash`. Use `-` otherwise.
   - **Difficulty**: a single integer (e.g. `1`, `2`, `3`, ...), or `-` for maps with no wild encounters. The number is up to the user — they decide when to increment it and by how much. Track the current difficulty in memory and remind the user of it before each prompt.

3. Append an entry to `ITINERARY.md` in the following format:

   ```markdown
   ## Step N — <Insert next map | Unlock MN map>

   - **Map**: <name>
   - **Requirement**: <HM/move or `-`>
   - **Difficulty**: <integer> or `-`
   ```

   **Difficulty** is a single integer that grows as the user decides to raise it. Use `-` for cities and for maps whose encounters are gated behind a move that will be unlocked later (e.g. a city with surfable water that needs `Surf`); the same map can be revisited later with a real integer once the gating move is acquired.

4. Increment the step counter and return to step 1.

## Notes

- The user may rename or re-order steps later; the format above is the canonical shape.
- The user owns the difficulty curve — the quiz does not enforce monotonicity, only reminds the user of the current value.
- Trainers are not configured by this quiz — only their reference difficulty.
