<p align="center">
  <img src="assets/hero.png" alt="Anti-Defensive Writing: an open book grows into a tree rooted in evidence. Develop the idea. Keep the evidence." width="100%">
</p>

<h1 align="center">Anti-Defensive Writing</h1>

<p align="center"><strong>Give worthwhile ideas the explanation, evidence, and voice they deserve.</strong></p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-23453B" alt="MIT license"></a>
  <a href="skill/anti-defensive-writing/SKILL.md"><img src="https://img.shields.io/badge/format-SKILL.md-16324F" alt="SKILL.md format"></a>
  <a href="README.zh-CN.md"><img src="https://img.shields.io/badge/docs-English%20%2F%20中文-A4472D" alt="English and Chinese documentation"></a>
</p>

<p align="center"><strong>English</strong> · <a href="README.zh-CN.md">简体中文</a></p>
<p align="center"><a href="#quick-start">Quick start</a> · <a href="#examples">See the difference</a> · <a href="#how-it-works">The method</a> · <a href="#usage">Prompts</a> · <a href="#provenance">Origins</a></p>

A portable writing skill for AI agents. It helps an author develop a promising idea, explain a relationship, and revise a draft with confidence calibrated to the evidence. It addresses premature retreat, repetitive caveats, unsupported narrowing, and revisions that leave prose smoother but thinner.

The guiding question is simple: **What should this passage help the reader understand or experience, and has it actually done that?**

This repository is **git-zyyang's adaptation** of [Kiterlin/anti-defensive-writing](https://github.com/Kiterlin/anti-defensive-writing). It carries forward the upstream treatment of claims and qualifications, with additional guidance for idea development, substantive review, theoretical depth, and preservation of authorial voice. [Read the provenance](skill/anti-defensive-writing/references/upstream.md).

## Contents

- [Why this skill exists](#why-this-skill-exists)
- [Quick start](#quick-start)
- [Examples](#examples)
- [How it works](#how-it-works)
- [Where it helps](#where-it-helps)
- [Usage](#usage)
- [Default integration](#default-integration)
- [Installation, updates, and removal](#installation-updates-and-removal)
- [Files and validation](#files-and-validation)
- [FAQ](#faq)
- [Provenance](#provenance)
- [Contributing and license](#contributing-and-license)

## Why this skill exists

AI-assisted writing can lose its central idea while trying to anticipate every objection. A paragraph spends its best sentences listing what it cannot establish. A research direction gets narrowed before its actual relationship to previous work is examined. A revision removes the caveats, then also removes the evidence and explanatory development that gave the passage substance.

This skill treats those as decisions about thinking and writing. It asks the agent to develop the supported argument, identify what each qualification contributes, and check what an edit has lost.

| When you see… | The skill asks the agent to… |
|---|---|
| A promising idea dismissed because a similar topic exists | Compare the actual question, explanation, method, and contribution. |
| A claim followed by generic self-undermining reminders | Identify a concrete reader need; develop the argument where the material supports it. |
| Repeated “may,” “only,” or “does not imply” | Read the passage and judge the function of each qualification. |
| Theory reduced to a list of practical measures | Restore the relationship that explains why the measures matter. |
| A polished revision that loses sources, voice, or a scene | Compare the actual passages and recover the lost value. |
| A cautious review treated as automatically correct | Evaluate its evidence and implications before revising. |

<p align="center">
  <img src="assets/principles.png" alt="Three principles: develop ideas, ground claims in evidence, preserve the author's voice." width="100%">
</p>

## Quick start

The skill consists of Markdown instructions and references. **It requires no API key, package installation, or executable service of its own.** Your chosen AI host supplies the model and any tools used for the writing task.

### Codex · macOS / Linux

Run this from the directory where you want to keep the repository:

~~~bash
git clone https://github.com/git-zyyang/anti-defensive-writing.git
cd anti-defensive-writing

# A same-named installation is left untouched.
if [ -e "$HOME/.agents/skills/anti-defensive-writing" ] || [ -L "$HOME/.agents/skills/anti-defensive-writing" ]; then
  echo "An installation already exists. Compare or back it up before replacing it."
else
  mkdir -p "$HOME/.agents/skills"
  cp -R skill/anti-defensive-writing "$HOME/.agents/skills/anti-defensive-writing"
fi
~~~

Then invoke it in Codex:

~~~text
$anti-defensive-writing

Revise the passage below for a research audience. Develop the central explanation
using the supplied material. Preserve the citations, findings, and conditions
that affect interpretation. Return the revised passage and brief notes on
substantive changes.

[paste your passage and relevant evidence]
~~~

Codex's documented user-level discovery directory is `~/.agents/skills`; project-level skills live in `.agents/skills`. Check the skill selector after installation and restart the host if it has not refreshed. See [Codex's local skill documentation](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills).

### Claude Code and other hosts

For Claude Code, copy the **entire** `skill/anti-defensive-writing` folder into `~/.claude/skills/` or your project's `.claude/skills/`, then use `/anti-defensive-writing`. See [Claude Code's skill documentation](https://code.claude.com/docs/en/skills#choose-where-skills-load).

For another host, use its documented skill directory. If it can read files but does not discover skills, ask it to read `SKILL.md` and the linked expression guide explicitly. Copy the references with the entrypoint.

These are format and documented-path integrations. [Validation status](docs/validation.md) distinguishes packaging checks from live host and model evaluation.

## Examples

The examples below are **constructed teaching material**, with stated premises. They illustrate editorial choices; they are not measured model outputs or claims about real research.

### 1. Develop the relationship

**Premise:** A shared glossary gives two teams the same definitions and reduces clarification exchanges.

**Before**

> This small change may be helpful, although it cannot solve every coordination problem.

**After**

> The shared glossary gives both teams the same definitions, reducing the back-and-forth needed to clarify terms.

The revision explains what changes and why. It does not add an unsupported claim about final delivery speed.

### 2. Keep the strength of the evidence

**Premise:** An observational analysis finds a positive association, without causal identification.

**Before**

> This may possibly suggest that X could be positively associated with Y.

**After**

> In this observational analysis, X is positively associated with Y.

The scope remains visible and the statement remains associational. If the direction or estimate is itself uncertain, that uncertainty still belongs in the account.

### 3. Preserve a necessary qualification

> The sample covers three pilot cities and cannot support a national prevalence estimate.

**Keep it** when readers might otherwise interpret the finding as a national estimate. An independently read abstract may need the condition even if the methods section already states it.

### 4. Preserve a character's voice

> “I'm not asking you to stay.” He left the porch light on.

In a fictional scene, the contrast between speech and action can carry feeling. Replacing it with a summary of “emotional conflict” would lose the scene's effect.

More examples cover [plans versus achievements, adverse results, real distinctions, responsibility, research scope, and read-only requests](skill/anti-defensive-writing/references/examples.md).

## How it works

### Develop the worthwhile content

Establish what the passage should explain, accomplish, or make felt. Use the material to develop that purpose. During ideation, examine what previous work enables and what the current question could add.

### Judge qualifications by function

For a caveat, ask:

1. What specific claim or possible misunderstanding does it address?
2. Has the current reading unit already done that work?
3. What would the reader lose if it disappeared?
4. Does it belong in the finished text or in an editing note?

A real scope condition, counterargument, apology, conceptual distinction, or narrative hesitation can be essential. A word list cannot decide.

### Repair the substantive problem

A factual error calls for correction. Repetition may call for deletion. A generic but accurate paragraph may need a more developed explanation. Rich material without a center may need reorganization. Effective prose deserves to remain.

### Inspect the actual result

Read the revised text without the editing notes, then compare it with the source. Check explanation, evidence, interpretive conditions, theory, voice, rhythm, and scenes. Carry changed definitions or claims through dependent passages.

These are decisions within the current task, not mandatory separate calls or approval stages. The full method lives in the [Skill entry](skill/anti-defensive-writing/SKILL.md) and [expression guide](skill/anti-defensive-writing/references/writing-expression.md).

## Where it helps

| Writing task | Useful focus |
|---|---|
| Research ideation and literature discussion | Compare questions and contributions before narrowing the project. |
| Academic papers and books | Develop explanations; retain citations, theoretical depth, and supported judgments. |
| Empirical reporting | Explain verified findings at the strength the design supports. |
| Proposals and policy reports | Connect the problem, actors, relationships, and proposed investigation or action. |
| Technical and business communication | State what changed, how it works, and what the reader should do. |
| Slides and teaching | Distribute explanation across the visible material and speaker notes. |
| Fiction and personal essays | Preserve desire, choices, felt experience, voice, and pacing. |
| Everyday messages | Communicate directly while retaining courtesy and responsibility. |

The language of the output follows your request. The portable instructions are in English; documentation and teaching examples are bilingual.

## Usage

### Develop a research idea

~~~text
Use anti-defensive-writing to help develop this research idea.
Compare it with the supplied literature at the level of questions and explanations.
Identify a worthwhile contribution and the evidence needed to investigate it.

Idea:
Sources:
Constraints:
~~~

### Strengthen an existing draft

~~~text
Use anti-defensive-writing to revise this section.
Explain the relationships that the supplied material supports.
Preserve citations, necessary conditions, and the author's register.
Point out specific missing evidence in a short editing note.
~~~

### Review without editing

~~~text
Use anti-defensive-writing for a read-only review.
Locate repetitive caveats, unsupported narrowing, and places where an earlier
revision may have lost substance. Explain each issue and its consequence.
Do not rewrite the passage or edit files.
~~~

### Refine creative prose

~~~text
Use anti-defensive-writing while revising this scene.
Keep the character's voice and meaningful hesitation.
Develop the experience through the available actions, perceptions, and choices.
Preserve the established events and point of view.
~~~

For best results, supply the audience, genre, source material, and any protected passages. A skill can use supplied evidence; a research workflow must obtain evidence that is still missing.

## Default integration

Installation makes a skill discoverable. To request it consistently during writing, add a short instruction to the host's instruction file, such as `AGENTS.md` or `CLAUDE.md`:

~~~markdown
For natural-language drafting and substantive review, load anti-defensive-writing
once per task and apply its checks within the current workflow. Develop the
supported explanation and preserve evidence, necessary conditions, and voice.
Respect read-only, formatting-only, quoted, and locked-text scopes.
~~~

This is an optional configuration choice. The repository does not edit your instructions or install hooks. Your host still controls discovery and invocation. Reuse the loaded method within the task rather than adding a visible ritual to every short reply.

## Installation, updates, and removal

### Project installation

Copy `skill/anti-defensive-writing` to your project's `.agents/skills/` for Codex, or `.claude/skills/` for Claude Code. Keep the `references/` directory and bundled `LICENSE` with it. Inspect any existing same-named skill before replacing it.

### Windows

Download the repository ZIP from GitHub's **Code → Download ZIP**, extract it, and copy the skill folder into the corresponding directory under your user profile, such as `%USERPROFILE%\.agents\skills\`. The installed folder should contain `SKILL.md`, `LICENSE`, and `references`.

### Updating

Run `git pull --ff-only` in your repository checkout, inspect the changes, and back up any local modifications before replacing the installed folder. A copied installation does not update when the checkout changes. Preserve the author's customized rules when merging an update.

### Removal

Remove the installed `anti-defensive-writing` folder and any default-integration instruction you added. Keep a copy first if you customized it. The project has no background process or package dependencies to uninstall.

### Name collisions

This adaptation retains the upstream skill name. If you already use Kiterlin's version, choose which installation your host should load and resolve the existing copy explicitly. Do not install two identically named versions and assume the host merges them.

## Files and validation

~~~text
anti-defensive-writing/
├── README.md                         English guide
├── README.zh-CN.md                   中文说明
├── LICENSE                          Upstream MIT notice
├── CONTRIBUTING.md                  Bilingual contribution guide
├── assets/
│   ├── hero.png                     README cover
│   ├── principles.png               Ideas / evidence / voice illustration
│   └── prompts.md                   Image prompts and generation notes
├── docs/
│   ├── provenance.md                Packaging and documentation references
│   └── validation.md                What checks can establish
└── skill/anti-defensive-writing/
    ├── SKILL.md                     Portable entrypoint
    ├── LICENSE                      License travels with the installed skill
    └── references/
        ├── writing-expression.md    Shared expression method
        ├── examples.md              Bilingual teaching examples
        └── upstream.md              Source and adaptation history
~~~

The installable folder is self-contained. The illustrations belong to the README and are not required at runtime.

Packaging checks cover frontmatter, relative links, required files, image readability, and accidental local/private material. There is no published comparative benchmark of writing quality in this release. See [validation guidance](docs/validation.md) for evaluating actual outputs.

## FAQ

**Will this make claims too strong?**<br>
The method preserves evidence strength. It distinguishes association from causation, plans from results, and candidate explanations from verified findings. Unsupported certainty is a defect to repair.

**Should every caveat be removed?**<br>
Keep caveats that change interpretation or action. The decision depends on the passage's function, including whether an abstract or caption will be read independently.

**Does it force short writing?**<br>
Length follows the task. A thin explanation may need expansion; a repetitive paragraph may need cutting. Long arguments and scenes can be valuable.

**Can it be used with another writing or research skill?**<br>
Yes. This skill supplies expression judgments within that workflow. Research design, source verification, document formatting, and delivery remain with the relevant task.

**Why are there no quality scores or claimed percentage improvements?**<br>
A score does not show whether an argument became more explanatory or a voice survived revision. This release supplies explicit decisions and examples; behavioral claims require recorded evaluations.

## Provenance

[Kiterlin/anti-defensive-writing](https://github.com/Kiterlin/anti-defensive-writing) provides the upstream foundation. This adaptation adds an integrated treatment of ideation, drafting, review decisions, cross-genre expression, and value preservation. The portable package contains newly written teaching examples and removes dependencies on the maintainer's private workspace.

The scope of the adaptation and the recorded baseline fingerprint are documented in [upstream.md](skill/anti-defensive-writing/references/upstream.md). README organization draws on the clear onboarding and navigable documentation of [Superpowers](https://github.com/obra/superpowers), [Anthropic Skills](https://github.com/anthropics/skills), and [Best-README-Template](https://github.com/othneildrew/Best-README-Template). [Documentation and asset notes](docs/provenance.md) distinguish these references from the skill's sources.

## Contributing and license

Share a concrete case, a preservation failure, or a better explanation through [Issues](https://github.com/git-zyyang/anti-defensive-writing/issues) or a pull request. See the bilingual [contribution guide](CONTRIBUTING.md).

Distributed under the [MIT License](LICENSE), retaining Kiterlin's copyright notice. The adaptation is maintained by [git-zyyang](https://github.com/git-zyyang).
