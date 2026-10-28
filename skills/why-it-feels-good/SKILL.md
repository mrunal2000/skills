---
name: why-it-feels-good
description: Deconstruct why a UI component, interaction, or component library feels good or falls short by reading its code, consulting available docs, and trying it when possible. Explain the experience in plain language and connect it to concrete implementation decisions. Use for design craft analysis, not routine implementation or a generic code review.
---

# Why it feels good

Help someone notice, understand, and reuse the decisions behind an interface's feel. Explain both what the person experiences and how the implementation produces it. Treat praise as a hypothesis to investigate, not the assignment's required conclusion. A component and an entire library are both valid subjects.

## Gather evidence

Use three complementary sources: documentation for stated intent, code for mechanisms, and interaction for observable behavior. Do not substitute one for the others or imply you inspected something you did not.

- Read relevant docs when available, including design notes. Treat author claims and source comments as claims to check. Missing docs should not stop analysis.
- Read implementation code. Make a concrete attempt to obtain it from the supplied repository, local project, installed package, published package contents, source maps, or component registry. A registry JSON may embed source and reference shared files. Trace the relevant dependencies instead of stopping at a wrapper, prop table, or README. Prefer a matching package version or revision; disclose a mismatch with the demo when it matters.
- Try the actual interface when tools and a runnable example are available. Prefer an existing demo or local app. If necessary, create a minimal isolated playground without modifying the user's application. Retrieve package contents without executing installation scripts when that is sufficient for reading code. Installing a library, overwriting app files, or installing its companion skill is not automatically necessary because its docs suggest it.
- If a source or runnable interface is inaccessible, state the specific limit and continue with available evidence. Do not describe a docs-only answer as code analysis, or screenshots as evidence of timing, responsiveness, or interruption behavior.

Use available browser or computer interaction tools without an extra confirmation when they materially improve the requested analysis and the actions are already authorized. Computer use is one way to inspect behavior, not a prerequisite for every analysis. If interaction requires the user to enable an available capability, explain the specific behavior you want to verify and ask once whether they want to enable it. Do not invent an enablement option for agents that lack one. Continue independent code-and-docs analysis while waiting; do not treat silence as permission. If interaction is unavailable or declined, complete the analysis with that limitation stated. Static components may need visual inspection more than interaction; gesture-driven controls benefit substantially from hands-on testing.

The sequence can vary. Form an initial observation from the interface when practical, then use docs and code to test it. Do not let the author's vocabulary become the entire explanation.

## Choose the scope

For one component, follow its important state changes and the code that owns them. Include the surrounding system only where it explains the behavior.

For a library, inspect shared foundations and a small, varied sample of components. Choose examples that exercise different behaviors, such as targeting, selection, direct manipulation, and overlays or state transitions. Look for where shared rules are applied and where exceptions occur. Report which components you sampled; do not imply an exhaustive audit. Expand the sample when contradictions would materially change your conclusion.

## Investigate the feel

Follow meaningful moments: approaching a target, pressing, changing a selection, entering or leaving a state, interrupting motion, and recovering from an empty or delayed state. Pick those relevant to the subject rather than running a universal checklist.

For dynamic data, use repeatable inputs when possible: steady change, sudden jumps, reversals, gaps, and bursts. For controls, try rapid reversal or repeated input, and keyboard or touch behavior where relevant and available. Observe what changes, what stays stable, how feedback is sequenced, and whether the visual target matches the actual action.

Read beyond animation constants. Trace state ownership, event handlers, hit testing, layout and measurement, identity across renders, typography, layering, rendering paths, and cancellation where they explain an observed effect. A spring token alone does not prove interruption works; a canvas alone does not prove good performance; an accessible primitive alone does not prove the final component is accessible.

For each strong finding, connect:

**Specific behavior → likely experience → implementation mechanism → consequence if changed.**

Use the last link as a test of whether the detail matters. When a lightweight comparison would resolve uncertainty, change one variable in an isolated reproduction and replay the same input. Otherwise make the counterfactual explicitly hypothetical. Never claim an A/B test or user study you did not perform.

Consider visual hierarchy, spacing, typography, affordances, feedback, stability, motion, and cross-component consistency according to the evidence. Do not reduce all quality to animation. Distinguish essential behavior from decoration that sets a particular tone.

## Exercise judgment

Criticize anything that deserves it. Explain the concrete cost, the context in which it matters, and the evidence behind the concern. Examples include feedback that trails input, movement that obscures information, ambiguous click regions, excessive emphasis, inconsistent component behavior, or reduced-motion handling that leaves distracting movement intact.

Separate a verified defect from a tradeoff, personal preference, or untested concern. There is no quota for praise or criticism. Do not invent weaknesses for balance, or call something universally good because it is expressive. Consider repeated use and the task's stakes as well as first-impression delight. Avoid performance and accessibility verdicts unsupported by inspection or testing.

When docs and code disagree, explain the discrepancy and base implementation claims on the inspected version. Code comments about calibration or measured performance are not measurements you have reproduced. Interpret psychological effects as reasoned judgments unless supported by relevant evidence from people.

## Write the explanation

Make the answer easy to scan. Investigate deeply, but summarize selectively. Default to roughly 250–450 words, fewer for a simple component. Expand only when the user asks for depth or a material finding needs it. For a library, synthesize the strongest shared patterns instead of giving every sampled component its own report.

Use this compact format, keeping qualitative and technical findings in separate sections:

1. **Verdict:** One sentence naming the central quality or weakness of this particular example. Avoid generic praise.
2. **Why it feels good:** Usually 2–4 short bullets in everyday language. Give each a brief, concrete label and one or two sentences describing a recognizable moment and its likely effect. No function names, CSS properties, spring constants, or implementation digressions here. Adapt the heading when the experience is mixed or poor.
3. **Technical takeaways:** Turn the implementation into explicit, reusable lessons. Present a Markdown table with exactly three columns: **Takeaway**, **How it works**, and **Values / props**. Use one row per reusable lesson. The Takeaway cell names a concrete design or engineering decision that makes sense on its own, such as “Animate the surface independently of the label.” The How it works cell briefly explains the mechanism and its practical consequence, with a source link. Keep cells concise; do not put paragraph-length explanations or nested lists inside them. Keep the order aligned with the qualitative findings where useful, but do not reuse their emotional labels. Link to the relevant source. Include the exact animation values and props behind each technical finding when available: durations and delays with units, easing curves, spring configuration, animated properties and their start/end values, transforms, distances, opacity, and interaction or motion props that enable or tune the behavior. Name the actual identifiers using inline code. Put these in the Values / props cell, separated with semicolons and labeled by state where needed. Use “Not applicable” when the mechanism has no relevant animation values or props; use “Not verified” for unknown values rather than inventing them. Explain what the important values control. Distinguish defaults from demo overrides, entry from exit, and configured duration from measured settling time. If a value comes from a shared token, resolve it to its definition and include both the token name and value. Report only values verified in code or clearly attributed to docs; say when a value could not be determined instead of guessing. Include relevant animation values even when they are not the main lesson, but do not dump unrelated API props.
4. **Where it falls short:** Include only meaningful criticism, usually 1–2 concise bullets. Identify the concrete cost and context, distinguishing observed defects from tradeoffs or untested concerns. Omit this section if there is nothing substantiated to add; do not manufacture balance.
5. **Checked:** One compact evidence line stating what you read and tried, the sampled components for a library, and any material limitation. Do not bury a limitation that undermines the verdict; mention that earlier too.

The qualitative section explains the experience; the technical section teaches the decisions that produce it. A reader scanning only the Takeaway column should learn something they could apply elsewhere. Keep each technical row focused on one lesson: do not bury unrelated spacing, timing, or documentation discrepancies inside a hover finding. Select the strongest lessons instead of cataloging every implementation detail. Preserve conditions and exceptions so a context-specific technique does not become a universal rule. Use descriptive source links within the How it works cells rather than a separate bibliography. Explain unfamiliar technical terms briefly. Do not add scores, exhaustive inventories, a recap, an implementation plan, or a repeated closing lesson by default.

Example format, using illustrative values that must be verified for the actual subject:

**Why it feels good**

- **A deliberate press.** The surface responds immediately while the label and click target stay steady.

**Technical takeaways**

| Takeaway | How it works | Values / props |
|---|---|---|
| **Animate the surface independently of the content.** | Contract a separate background layer while keeping text and the hit area fixed. [Source](verified-source-link) | Animated property: `box-shadow`; contraction: `1px` per edge |
| **Press quickly, release gently.** | Separate timings give immediate feedback and a softer return. [Source](verified-source-link) | Press: `80ms`; release: `180ms` |

Avoid a Takeaway cell such as “A small, deliberate press” followed by a dense inventory of implementation details. Name the reusable technical decision instead. Keep distinct lessons in separate rows. These example mechanisms and values are not rules to impose on every component.

Use plain language that distinguishes interpretation from observation without repeating a disclaimer after every bullet. Replace adjectives such as polished, delightful, intuitive, or smooth with what actually happens. The output should explain the experience, not merely list features.

Before responding, check that you actually read code, attempted interaction when feasible, and kept documented intent, inspected mechanics, observed behavior, and your interpretation distinct. If one is missing, disclose it plainly. Do not claim to know why every user will feel the same way.
