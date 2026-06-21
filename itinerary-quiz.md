# Itinerary Quiz

Conduct the following quiz to build the story itinerary. Repeat the loop until the user selects **Stop**.

## Loop

1. Ask a multi-answer question with these options:
   - **Insert next map** — add a map to the itinerary (routes, cities, etc.)
   - **Unlock MN map** — unlock a map previously inaccessible due to a missing requirement (e.g. a Hidden Machine like Surf)
   - **Stop** — finish the quiz

   Use the `question` tool with `multiple: true`. Always include **Stop** in the list. If the user picks **Stop** alongside other options, treat it as terminating the quiz and discard the other selections.

2. For each map selected (in the order the user listed them), ask:
   - **Map name / identifier** (free text)
   - **Requirement** (only for "Unlock MN map" picks — e.g. `Surf`, `Cut`, `Strength`, `Waterfall`, `Flash`)
   - **Difficulty**: a level range for wild encounters (e.g. `3-5`, `12-14`), or `-` if the map has no wild encounters (cities, or maps with encounters gated behind a move unlocked later). Trainers will use this as a reference but be a bit stronger.

3. Append an entry to `ITINERARY.md` in the following format:

   ```markdown
   ## Step N — <Insert next map | Unlock MN map>

   - **Map**: <name>
   - **Requirement**: <HM/move or `-`>
   - **Difficulty**: <min>-<max> or `-`
   ```

   **Difficulty** may be `-` (no wild encounters). Use this for cities, and for maps whose encounters are gated behind a move that is unlocked in a later step (e.g. a city with surfable water that needs `Surf`). The same map will receive a real range in a later step when the gating move is acquired.

4. Increment the step counter and return to step 1.

## Notes

- The user may rename or re-order steps later; the format above is the canonical shape.
- Difficulty strictly increases across the itinerary. Do not allow a later step to be easier than an earlier one; if the user proposes one, confirm before accepting.
- Trainers are not configured by this quiz — only their reference level range.
