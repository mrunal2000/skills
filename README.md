# Why it feels good

An agent skill for understanding the craft behind a UI component, interaction, or entire library.

It reads available docs, traces the implementation, and tries the interaction when possible. Then it explains what makes the experience work—and where it falls short—in plain language and technical terms.

## Install

```bash
npx skills add mrunal2000/skills --skill why-it-feels-good
```

Choose your agent when prompted. For manual installation, copy the [`why-it-feels-good`](skills/why-it-feels-good) folder into your agent’s skills directory.

The skill is agent agnostic: one `SKILL.md`, with no scripts, dependencies, or vendor-specific metadata. Your agent needs to support skills or load the instructions directly.

## Use

Give your agent a demo URL, repository, package name, or local component:

```text
Use the why-it-feels-good skill to analyze https://benji.org/liveline
```

```text
Use the why-it-feels-good skill to explain why this button feels good.
Read src/components/button.tsx and try it in the running app.
```

```text
Use the why-it-feels-good skill to analyze this component library.
Look at its shared systems and a few representative components.
```

## What you get

- **Verdict:** the central strength or weakness in one sentence.
- **Why it feels good:** short, plain-language findings.
- **Technical takeaways:** a table of reusable decisions, implementation details, and verified animation values or props, with source links.
- **Where it falls short:** meaningful criticism and tradeoffs, when supported.
- **Checked:** what the agent inspected, tried, and could not verify.

The explanation separates documented intent, code-supported mechanisms, observed behavior, and interpretation. It does not assume every design choice deserves praise.

## Does it need computer use?

No. Browser or computer interaction helps verify timing, gestures, and interruptions, but the skill can still analyze code and docs without it. If enabling an available capability would help, the agent asks and explains what it wants to check. Missing access is disclosed in the result.

## Read or improve the skill

The full instructions are in [`skills/why-it-feels-good/SKILL.md`](skills/why-it-feels-good/SKILL.md). Suggestions and examples of unhelpful output are welcome in [issues](https://github.com/mrunal2000/skills/issues).
