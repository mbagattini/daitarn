# /d3-onboard

One-time bootstrap. Auto-detects greenfield vs brownfield and produces reference/perimeter.md and reference/conventions.md in a single guided session.

## Behavior

1. Announce phase atomicity:

   Onboarding populates perimeter.md and conventions.md through a single conversation. It must be completed in one session. If interrupted, the work is lost and onboarding restarts. Confirm to proceed.

   Wait for confirmation.

2. Detect mode:
   - Look for code files in common roots (src/, lib/, app/, and any path the pilot has already mentioned in CLAUDE.md or the chat).
   - If code is found: brownfield mode.
   - If little or nothing is found: greenfield mode.
   - Announce the detected mode and what was found. The pilot may correct ("ignore vendor/, that's just dependencies").

3. Phase A — perimeter.md.

   Brownfield:
   - Explore the project structure (declaring the lookup).
   - Propose a complete list of paths with mode (r/w, ro, hidden) and a short note where useful. One full proposal, not one path at a time.
   - The pilot corrects in chat.
   - Copy d3-docs/system/templates/perimeter.md, strip HTML comments, write to d3-docs/reference/perimeter.md filled in with the agreed list.

   Greenfield:
   - Ask the pilot: where do you plan to put code? Are there paths to keep ro or hidden from the start?
   - Copy d3-docs/system/templates/perimeter.md, strip HTML comments, write to d3-docs/reference/perimeter.md filled in with the pilot's answers.

4. Phase B — conventions.md.

   Brownfield:
   - Read 3-5 representative code samples (declaring which and why).
   - Extract observed conventions: language, naming style, recurring patterns, file organization.
   - Stay at broad strokes. Do not enumerate minutiae; those emerge per-step.
   - Propose conventions in a list. Where ambiguous, frame as A/B/C with a recommendation and a one-line rationale.
   - The pilot decides.
   - Copy d3-docs/system/templates/conventions.md, strip HTML comments, write to d3-docs/reference/conventions.md filled in.

   Greenfield:
   - Ask the pilot the foundational choices (language, style, frameworks if any).
   - Keep it short. Sufficient to operate the first step without ambiguity.
   - Copy d3-docs/system/templates/conventions.md, strip HTML comments, write to d3-docs/reference/conventions.md filled in.

5. Tell the pilot:

   Onboarding complete. perimeter.md and conventions.md are in d3-docs/reference/. Update or extend them by hand when needed. To start the first step, run /d3-1-brief.

## Notes

- The assistant writes perimeter.md and conventions.md. The pilot corrects in chat during the session, and may freely edit the files afterwards.
- journal.md is not created during onboarding. It will be populated over time via promotions proposed in /d3-5-close.
- Stay at the level of broad strokes. Do not propose exhaustive content; reference/ is alive and grows by targeted accretion.
- Respect Documents and Interactions languages in CLAUDE.md.
- Use the Daitarn root declared in CLAUDE.md.
