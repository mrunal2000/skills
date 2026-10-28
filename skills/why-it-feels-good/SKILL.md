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

Use available interaction tools within the authorized analysis without asking again. Computer use is helpful, not required: static components may need visual inspection more than interaction. If enabling an available capability would help, explain what you want to verify and ask once. Continue independent code-and-docs work while waiting; silence is not permission. Do not invent an enablement option. If interaction is unavailable or declined, finish with that limit stated.

The sequence can vary. Form an initial observation from the interface when practical, then use docs and code to test it. Do not let the author's vocabulary become the entire explanation.

For behavior attributed to code, trace the active path from call-site props through shared tokens and relevant CSS overrides, platform branches, and motion preferences. A default constant may not describe the demonstrated setup. If the active setup cannot be established, label the analyzed defaults or configuration as such; do not imply they were observed.

For code-only analysis, introduce the verdict as an interpretation of the implementation. Reserve “I observed” and “I tried” for actual interaction. State a material limitation once near the affected conclusion, then use natural language rather than repeating a disclaimer in every finding.

## Choose the scope

For one component, follow its important state changes and the code that owns them. Include the surrounding system only where it explains the behavior.

For a library, inspect shared foundations and a small, varied sample of components. Choose examples that exercise different behaviors, such as targeting, selection, direct manipulation, and overlays or state transitions. Look for where shared rules are applied and where exceptions occur. Report which components you sampled; do not imply an exhaustive audit.

Stop when the selected findings have enough evidence to explain the behavior, mechanism, and meaningful limits. Expand investigation or sampling only to resolve a contradiction or uncertainty that could change the conclusion. Do not keep collecting components, props, or animation tokens merely because they exist.

## Investigate the feel

Follow meaningful moments: approaching a target, pressing, changing a selection, entering or leaving a state, interrupting motion, and recovering from an empty or delayed state. Pick those relevant to the subject rather than running a universal checklist.

For dynamic data, use repeatable inputs when possible: steady change, sudden jumps, reversals, gaps, and bursts. For controls, try rapid reversal or repeated input, and keyboard or touch behavior where relevant and available. Observe what changes, what stays stable, how feedback is sequenced, and whether the visual target matches the actual action.

Trace the state, events, targeting, layout, typography, rendering, or cancellation that explain the effect. A spring token alone does not prove interruption works; a canvas does not prove performance; an accessible primitive does not prove the final component is accessible.

For each strong finding, connect:

**Specific behavior → likely experience → implementation mechanism → consequence if changed.**

Use the last link as a test of whether the detail matters. When a lightweight comparison would resolve uncertainty, change one variable in an isolated reproduction and replay the same input. Otherwise make the counterfactual explicitly hypothetical. Never claim an A/B test or user study you did not perform.

Consider visual hierarchy, spacing, typography, affordances, feedback, stability, motion, and cross-component consistency according to the evidence. Do not reduce all quality to animation. Distinguish essential behavior from decoration that sets a particular tone.

## Exercise judgment

Criticize anything that deserves it. Explain the cost, context, and evidence: for example, lagging feedback, obscured information, ambiguous targets, excessive emphasis, inconsistent behavior, or distracting movement under reduced-motion settings.

Distinguish verified defects, tradeoffs, personal preferences, and untested concerns. Do not invent weaknesses for balance or equate expressiveness with universal quality. Consider repeated use and task stakes alongside first impressions. Support performance and accessibility verdicts with inspection or testing.

When docs and code disagree, explain the discrepancy and base implementation claims on the inspected version. Code comments about calibration or measured performance are not measurements you have reproduced. Interpret psychological effects as reasoned judgments unless supported by relevant evidence from people.

## Write the explanation

Investigate deeply, but summarize selectively. Default to roughly 250–450 words, fewer for a simple component. Expand when the user requests depth or a material finding needs it. For a library, synthesize shared patterns rather than giving every sampled component its own report.

Keep qualitative and technical findings separate:

1. **Verdict:** One sentence naming the central quality or weakness. Frame it as an interpretation when runtime behavior has not been observed.
2. **Why it feels good:** Usually 2–4 short bullets in everyday language. Describe a recognizable moment and its likely effect, without function names or animation constants. Adapt the heading for mixed or poor experiences.
3. **Technical takeaways:** A Markdown table with exactly **Takeaway**, **How it works**, and **Values / props**. Default to 3–5 strong lessons, fewer for simple components. Follow the table rules below.
4. **Where it falls short:** Only meaningful criticism, usually 1–2 concise bullets. Explain the concrete cost and context; distinguish observed defects from tradeoffs or untested concerns. Omit if there is nothing substantiated to add.
5. **Checked:** One compact line naming the evidence, sampled components for a library, analyzed configuration, and material limits. A limitation that undermines the verdict also belongs near that verdict.

### Technical table

- **Takeaway:** Name one reusable design or engineering decision that makes sense on its own. “Animate the surface independently of the label” teaches more than “A deliberate press.” Keep roughly the same order as the qualitative findings, without repeating their wording.
- **How it works:** Briefly explain the actual mechanism and consequence, with a descriptive source link. Preserve relevant conditions so a local technique does not become a universal rule. Explain unfamiliar terms briefly.
- **Values / props:** Give the verified settings behind that lesson: relevant animated properties and endpoints, durations and delays with units, easing or spring parameters, distances, opacity, and controlling props. Use actual identifiers in inline code, short state labels, and semicolons. Static findings may instead include spacing, type, layout, or other relevant settings; do not force an animation explanation.
- Analyze the **active configuration** shown or specified. With no demo or known active setup, report clearly labeled defaults. Include another size, theme, or variant only when it materially changes the explanation or the user asks for comparison. Do not enumerate every variant by default.
- Resolve shared tokens and report both the token name and values **actually consumed by this behavior**. Check call-site overrides before quoting defaults. Exclude unused transitions or token fields, such as an exit preset that the component never applies.
- Distinguish entry from exit, configured duration from measured settling time, and values verified in code from values only documented. Use “Not verified” for an unknown value and “Not applicable” when the lesson has no relevant values or props. Do not guess.
- Keep each row focused on one lesson and each cell compact. Include exact relevant values for the selected mechanism, but avoid an inventory of incidental coordinates or unrelated props. If a mechanism has a long state map, show the states needed to understand it and link to the full definition. Do not squeeze all findings into the table or repeat the same configuration across rows.

Example format, with illustrative values that must be verified for the actual subject:

**Why it feels good**

- **A deliberate press.** The surface responds immediately while the label and click target stay steady.

**Technical takeaways**

| Takeaway | How it works | Values / props |
|---|---|---|
| **Animate the surface independently of the content.** | Contract a separate background layer, leaving text and the hit area fixed. [Source](verified-source-link) | `box-shadow`; contraction: `1px` per edge |
| **Press quickly, release gently.** | Separate timings give prompt feedback and a softer return. [Source](verified-source-link) | Press: `80ms`; release: `180ms` |

These example mechanisms and values are not rules to impose on other components. Replace vague praise such as polished, delightful, intuitive, or smooth with what actually happens. Do not add scores, exhaustive inventories, a recap, an implementation plan, or a repeated closing lesson by default.

Before responding, verify that you read relevant code **or describe the concrete attempt and why access failed**; attempted interaction when feasible; traced reported values to the analyzed configuration; and kept documented intent, inspected mechanics, observed behavior, and interpretation distinct. Do not claim to know why every user will feel the same way.
