---
name: screenshot-critique
description: Use one unprimed subagent as a second set of eyes at a visual-wave boundary or final integration. Mandatory before accepting an integrated visual wave, before declaring a user-reported visual bug fixed, and once more on the final integrated visual state; do not run a fresh critique for every contributing slice.
---

# Screenshot Critique

Use one unprimed subagent as a second set of eyes after related visual slices
have been integrated into a coherent wave. This is for visual defects, not
pixel metrics; pair it with `compare-screenshots` when you also need numbers.

## Workflow

1. Fix the review scope: one integrated visual wave, or the final integrated
   visual state. Capture or locate its current PNGs/GIF frames; include the
   reporter's framing when the wave answers a user-reported bug.
2. Create tight 2x-4x crops for every key feature changed in the wave, plus the
   full screenshot for context. Crop selected units, city/town stacks,
   flags/poles, shadows, selection rings, labels/icons, roads, terrain
   features, water, and any artifact-prone area. If the complaint is about
   "too faint", "wrong order", or "not in perspective", the crop is mandatory.
3. Spawn one fresh explorer with `fork_context: false`; pass only the full
   images, the crops, and a short neutral task. Do not include the main thread
   history, implementation details, or expected answer.
4. Ask for concrete visible defects with confidence levels. Name likely risk
   categories: unit/prop depth ordering, layering, shadows, selection-marker
   contrast, ground-plane perspective, flag/pole attachment, label style and
   icon readability, blur, scale, lighting, artifacts, missing models, terrain
   feature readability, roads, water, and overall scan readability.
5. Compare the sub-agent's critique against your own inspection. Treat overlap
   as high-priority evidence. Treat novel high-confidence findings as bugs to
   inspect, not as taste notes to dismiss.
6. Record actionable findings against the owning wave in the spec, visual
   report, or next task plan before accepting it.

## Sub-Agent Prompt

Use this shape, replacing the bracketed surface and attaching local images:

```text
Fresh visual critique task. You have no project backstory and should only
inspect the supplied screenshots and crops. First inspect the full screenshot
for context, then inspect each crop at zoomed scale. Look for concrete
visual/layout defects in [surface], especially unit/prop depth ordering,
layering, shadows, selection-marker contrast, ground-plane perspective,
flag/pole attachment, label style/icons, blur, scale, lighting, artifacts,
missing models, terrain feature readability, roads, water, and scan
readability. Do not assume these are correct. Return a concise list of issues
you can see, with confidence and whether the issue is visible in the full image,
the crop, or both.
```

Spawn config:

- `agent_type`: `explorer`
- `fork_context`: `false`
- attach screenshots as `local_image` items
- omit model overrides unless the user explicitly requests one

## Rules

- **One per wave, one at final integration.** Contributing slices collect
  honest shots and focused comparison evidence; they do not each spawn a fresh
  critic. Run this skill after the coherent visual wave is integrated, then
  once more over the feature's final visual state. The final-integration
  critique is a distinct feature-wide pass even when the last visual wave just
  closed.
- **Mandatory before "fixed":** never declare a user-reported visual bug fixed
  on the implementer's inspection. Include it in the next wave-boundary
  critique; “mild residue” the primed implementer is tempted to waive is
  exactly what fresh eyes catch.
- **Reproduce the reporter's framing.** When the user supplied a screenshot,
  the critique must include a capture at that framing (same camera/zoom/spot,
  or as close as reproducible) — a defect that lives at their framing can be
  invisible at yours. Your chosen probe framing is a supplement, never the
  substitute.
- **Prove the change is real before critiquing it.** Byte/pixel-diff the
  candidate against the pre-change baseline first: a critique of an unchanged
  image "verifies" a no-op. (Recorded failure: a palette pass that never
  reached the production render path — before/after were byte-identical and
  only the diff caught it.)
- Never tell the sub-agent the defect you expect it to find.
- Use the current candidate screenshot, not a stale report or baseline image.
- Do not rely on full-page report scale for small visual features. Attach
  crops around the exact features a player would read: selected army/city,
  label/icon clusters, flags, shadows, ring edges, road crossings, terrain
  feature patches, water labels, and suspicious debug/artifact regions.
- If the sub-agent says a crop reveals an issue that is weak or invisible in
  the full shot, treat it as a real usability defect when the player can zoom
  to that scale in-game.
- For animation, attach a short set of deterministic still frames first; GIFs
  are useful for human review, but still frames make specific defects easier to
  name.
- A passing sub-agent critique does not replace direct inspection by the main
  agent or screenshot regression gates.
- If the sub-agent catches an issue the main agent missed, add that failure mode
  to the relevant wave evidence or feature plan immediately.
