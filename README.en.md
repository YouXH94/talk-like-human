# talk like human

English · [简体中文](README.md)

A Codex writing skill for **Chinese reports, progress updates, and technical explanations**. It turns stiff, overly compressed wording into clear, connected Chinese while preserving facts, numbers, conditions, and uncertainty.

For example, when the source supports that meaning, it can explain “concurrency scenarios are not covered” as “we have not yet tested what happens when several people use it at the same time.”

## What it helps with

A report can contain all the right terminology and still leave readers unsure what happened, what was checked, or what the findings mean. This skill makes those relationships easier to follow.

- **Explain abstract labels through concrete actions.** Identify the relevant people, objects, and behavior when the source provides them.
- **Preserve facts and confidence.** “Not tested” stays different from “failed,” and a possible cause does not become a confirmed cause. Keep numbers, units, conditions, exceptions, and sources.
- **Use a structure that fits the content.** Prefer connected paragraphs for explanations, and use lists for steps, parallel items, or comparisons. Do not force every response into a template.
- **Keep the appropriate register.** Formal reports stay formal, technical terms remain accurate, and natural writing does not require jokes, invented experiences, or emotional embellishment.

Use it to revise an existing draft or write from supplied notes. It does not verify the underlying facts or fill missing information with invented details. Results depend on the input and the model.

## Before and after

These are **fictional, illustrative rewrites**, not records of real projects or a model benchmark. The English passages below translate Chinese examples to explain the changes; the skill itself targets Chinese writing. In examples 1 and 2, the report author is the person who performed the checks. Without that context, a rewrite must not invent an “I checked” claim.

### 1. Explain a confirmed problem concretely

**Before**

> After a reservation is cancelled, the page does not restore availability. Investigation found that the availability query does not exclude cancelled records, so the time slot is still treated as occupied. Improve the query conditions and verify that the slot can be booked again after cancellation.

**After**

> The reservation has been cancelled, but the page still shows that the time slot cannot be booked. I checked the query logic and found that the system still counts cancelled reservations when calculating free time.
>
> The query should exclude those cancelled records. After the change, cancel a reservation and try booking the same slot again to confirm that the problem is resolved.

**What changed:** The rewrite explains the behavior behind the query issue and connects the proposed change to a concrete verification step.

### 2. Separate completed checks from open questions

**Before**

> A user reports that an already open document page remains viewable after access is removed. Only the frontend permission configuration has been checked; cache handling and server-side authorization have not been checked, so the cause remains unclear. Investigate those areas and test access after refreshing and signing in again.

**After**

> A user says they can still view a document in a page that was already open after their access was removed.
>
> So far, I have only checked the frontend permission configuration. I have not checked how the cache and server handle the permission change. I suggest checking both, then testing whether the document still opens after a refresh and after signing in again, to identify where the problem occurs.

**What changed:** The cause remains unresolved, and suggested checks are not presented as work already completed.

### 3. Keep a performance result tied to its test conditions

**Before**

> On the same server with 50,000 product records and a warmed cache, 20 queries were run before and 20 after optimization. Average search time fell from 2.4 seconds to 0.9 seconds. The result applies only to those conditions; cold-cache and concurrent-user scenarios have not been tested. Complete those tests before assessing release readiness.

**After**

> In this test, average product search time fell from 2.4 seconds to 0.9 seconds. Both runs used the same server and the same 50,000 product records, with 20 queries before the change and 20 after it. The cache was already warmed up.
>
> We have not yet tested how fast searches are with a cold cache or whether searches slow down when several people use the system at once. I suggest testing both before deciding whether it is ready to go live.

**What changed:** All numbers and conditions remain visible. A limited test does not turn into a claim that the system is ready for release.

[See all six original Chinese examples](references/examples.md), including product rules, schedule risks, and suggestions for reducing duplicate work.

## Install in Codex

This standalone skill contains instructions and examples only. It needs no additional API key, MCP service, or executable script. You still need your existing Codex environment and model access.

### Option 1: Ask Codex to install it

```text
Use $skill-installer to install the talk-like-human skill from https://github.com/YouXH94/talk-like-human.
```

### Option 2: Install a pinned version manually

Run these commands in a macOS or Linux terminal to install `v1.0.0` in the user skill directory:

```bash
mkdir -p "$HOME/.agents/skills"
git clone --depth 1 --branch v1.0.0 https://github.com/YouXH94/talk-like-human.git "$HOME/.agents/skills/talk-like-human"
```

Alternatively, download `talk-like-human-v1.0.0.zip` from [Releases](https://github.com/YouXH94/talk-like-human/releases), extract it, and place the `talk-like-human` folder in `~/.agents/skills/`. For use in one project only, place it in that project's `.agents/skills/` directory.

If a skill with the same name is already installed, review its contents and location first to avoid duplicate installations. Try invoking the skill after installation; if it does not appear in the skill list, restart Codex.

See the [official OpenAI skills documentation](https://learn.chatgpt.com/docs/build-skills) for discovery locations. Other tools that support `SKILL.md` may be able to use these instructions, but their installation procedures and compatibility have not been verified here.

## Usage

**Revise an existing Chinese report**

```text
Use $talk-like-human to revise the Chinese report below for colleagues familiar with the subject.
Preserve facts, numbers, sources, test conditions, and uncertainty.
Return only the revised Chinese text.

[Paste the source text]
```

**Write a progress update from notes**

```text
Use $talk-like-human to write a formal Chinese progress update from these notes.
Distinguish completed work, unfinished work, and suggestions.
Do not invent checks, causes, or conclusions.

[Paste the notes]
```

**Request a comparison**

```text
Use $talk-like-human to revise the Chinese text below.
Show a before-and-after comparison and explain the key changes.
Keep its level of formality, quotations, commands, and code intact.

[Paste the source text]
```

Automatic selection is enabled, and you can invoke the skill explicitly with `$talk-like-human`. By default it returns the finished text. Ask for comparisons, explanations, or a particular format when needed. Your requested genre, terminology, tone, and length take precedence.

## Scope and privacy

The skill primarily targets explanatory writing in Chinese. An English README does not imply optimization for English writing. It is not a fact-checking tool and makes no promise about passing AI-text detectors. Code, exact quotations, and machine-readable content must follow the task's preservation requirements.

The package contains no telemetry, networking code, or external service dependency. Text you provide is still processed by your chosen AI product. This skill neither changes that product's data practices nor automatically anonymizes your input. Redact sensitive information before sharing it.

## Repository contents

```text
talk-like-human/
├── SKILL.md                 Core instructions in Chinese
├── agents/openai.yaml        Codex UI metadata and invocation policy
├── references/examples.md    Six fictional Chinese examples
├── README.md                 Chinese guide and comparisons
├── README.en.md              English guide and translated examples
├── CHANGELOG.md              Release history
└── LICENSE                   MIT license
```

## License

[MIT](LICENSE). You may use, modify, and redistribute the skill while retaining the copyright and permission notice.
