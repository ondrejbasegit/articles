---
nazev: How to get an AI to work your way
typ: clanek
druh: HOW-TO
popis: The most useful instructions I have written for an AI have nothing to do with code.
---

No website is complete these days without a guide to writing your CLAUDE.md. I am going to try a slightly different one (which everyone says as well, I know). Instead of a file to copy and paste, I will describe how I go about it and what to watch out for. The most useful instructions I have have nothing to do with code or anything technical.

First a bit of theory, from the ground up, none of the advanced parts (custom agents, skills, MCP — another time).

Once you give an AI agent access to your computer, and it does not matter which agent (Codex, Cursor, Copilot, Gemini, Claude Code…), there are usually two places it takes its “permanent knowledge” from, meaning its instructions:

- **Global** — in the home directory of the current user, e.g. `~/.claude/`
- **Per project** — in the folder of the project the AI is currently open in,
  e.g. `~/projects/invoicing/.claude/`

The agent will usually create both by itself and keep whatever it sees fit in them. What we care about is one file in each folder. It goes by different names, and its content is stuck in front of every prompt you type:

| tool | file |
|---|---|
| anyone | `AGENTS.md` |
| Claude Code | `CLAUDE.md` |
| GitHub Copilot | `.github/copilot-instructions.md` |
| Cursor | `.cursor/rules/*.mdc` (formerly `.cursorrules`) |
| Gemini CLI | `GEMINI.md` |

Keep in mind that the agent loads the file from your home directory every single time, and the one from the project folder only while it works on that project.

That split also tells you which kind of instruction belongs where.

**Global, in your home directory** (`~/.claude/CLAUDE.md`) — applies to every session, whatever folder or project I am in. Only what is true all the time goes here. Mine holds, among other things:

- who I am and how to talk to me — language, tone, how much to riff (“*I like brainstorming, throw ideas at me often and do not be brief about it*”)
- more detail about my machine — hardware, PowerShell, WSL2, my home server
- that it should look things up on the web on its own, without asking, and **not invent them**, “*the model's knowledge is out of date and most questions need something current from the web*” (worth reminding an AI about)
- what belongs where on disk
- what it must never do: delete or overwrite without confirmation, post anything in public, touch a few “off limits” folders
- lessons from mistakes and how to avoid them next time — writing down what to do better, regularly, on its own and without being asked (this one matters)

**Per project, in the project folder** — everything else, everything specific to the project the AI is working on. Paths, conventions, states, decisions, reasons. None of that belongs in the global file, because it will not be true in any other project.

The file will grow as more of this piles up, so past a certain point it works best as a **signpost** to the rest of your documentation. It should still carry a general description of the project and the rules that cannot be broken.

One project from my own computer, deliberately not a technical one:

## A file about a camera

My first real camera after years of shooting on an iPhone. Into the `CLAUDE.md` of my `foto` project I wrote instructions that have nothing to do with code:

> **I am a complete beginner.** I do not know the genre terms or the acronyms.
>
> **Explain the terms.** Whenever you use a technical term or an acronym,
> ALWAYS explain it simply, right there. Do not assume I know anything.
>
> **Correct me directly.** When I have something wrong, say so. Do not agree
> with me when I am not right.
>
> **No “it depends”.** When the answer really does depend on the situation,
> say what it depends on and give me **a rule to decide by**, not a list of
> options.

Below that is my gear down to the last detail — body, lens, focal length, how close it focuses — and then a section called **“What I already understand”**. It says that exposure is aperture, shutter speed and ISO, that ISO is a consequence rather than a creative choice, and that I follow one rule: *use the longest shutter speed that keeps everything sharp*. Not so the model knows. So it stops explaining it to me.

And at the end, a mandatory order of work: **the manual in the repository first** — all 452 pages cut into markdown, plus an image of every page in case the text is not enough — **the web only after that**. *Never invent a menu path or a setting.*

## A rule without a scar is just decoration

Having gone through all my instruction files, almost every sentence that ever prevented something was written after it happened. First mistakes are usually impossible to avoid. The really serious ones are what the home directory file and hard limits on commands are for, but that is not what this article is about.

The rest you deal with differently: the agent should keep a running record of what worked and of the mistakes the project fell into. It tends to do that by itself, but it is worth stating outright in the main instruction file as a safety net.

Three examples from the `AGENTS.md` of my `galerie` project:

> **Never decide from a description.** Whether an image is a clean reproduction
> is decided by looking at it. Auction blurbs, blog captions and artists' own
> modest wording (“just a study”) say nothing reliable.

> **Check the role, not just the name.** Museum APIs return works where the
> artist is the *sitter*, not the maker. Filter on the creator role or you will
> file someone else's painting under your artist.

> **Empty is not the same as none.** Several of these APIs return an empty
> result instead of an error when they are being rate limited. Repeat before
> believing it. Trusting a single empty answer has silently emptied a
> catalogue before.

The last one is the most valuable of the lot, and not because of what it orders, but because of its last sentence. Without it, it is general advice. With it, it is a fact about my project.

## Agree on the pace before you start

At the beginning of a project it pays to settle how the two of you are going to work together. The agent will happily propose it itself, but approve it first and then write it down, so its behaviour does not drift from session to session. What the AI is allowed to do follows from that.

Examples from my own instructions:

> - Commit the backup script yourself. **Push only once I have said so.**
> - On the website, run git entirely on your own — commit and push, no asking.
>   Nowhere else.
> - My original repositories are off limits. A public copy is a new repository;
>   a change never travels back into the project, **even when it belongs there**.
> - At the end of every step, report what you found and what you are about to
>   do, then wait for me.
> - Never offer to write anything in public for me — Reddit, GitHub issues,
>   forums. I write in my own voice.
> - Ask before anything irreversible.

## Writing with an AI

I would not let an AI write longer texts, other than drafts or strictly technical descriptions such as a README. There are still a few ways to strip some of the usual AI habits out of a text.

In the instructions for this website I have it like this:

> **Out go the phrases where the text rates itself:** “being honest about
> this”, “and I am not going to pretend otherwise”, “worth knowing before you
> spend an evening on it”. State the fact, not the impression.
>
> Calling yourself honest is the strongest sign of a text written by an AI —
> a person who tells you something does not usually mention their own honesty.

A list of words to run the text through before it goes out: `honest`, `pretend`, `worth knowing`, `to be fair`, `admittedly`, `frankly`.

## Split the instructions by what may leave your computer

You do not have to deal with this while a project stays yours. The moment you want to release it publicly you hit a wall: the instructions hold a server address, paths to data, container names and decisions that mean nothing to anyone else.

In `galerie` I cut it into three files by a single question — **may this go out?**

- `AGENTS.md` is about the project: how it works, what must not break, how to
  add another source. It ships unchanged.
- `docs/ops.md` is about this one machine: server, deployment, my curatorial
  decisions. It never ships.
- `CLAUDE.md` is left as a signpost to those two.

Checking that it holds is then easy. Between the public copy and my private one there is a single line of difference, and it is a container name.

This is not a security measure, it is an organisational one. Keys and passwords have no place in instructions to begin with — they belong in `.env`, outside the repository — and the project gets scanned by a tool before it goes public.

## What instructions cannot do

**A written rule is not a rule that gets followed.**

My instructions said that the AI pushes to a remote repository only once I approve. The model broke it — it took permission that applied to one repository and carried it over to another. An instruction file lowers the risk, it does not remove it.

When you need certainty, instructions are not enough and you have to reach for limits that cannot be talked around. They look different in every agent, but the principle is the same: a config file can restrict which commands it may run at all. And then there is approving every single action, which tends to be on by default.

**Instructions go stale faster than code.**

On a long-running project you maintain more than its contents — you maintain the file that describes it. At the end of a working session, get the agent to review the instructions as well as write down where the project stands. It should catch newer orders contradicting older ones, and parts of the documentation that no longer hold.

Every once in a while, ask for a full analysis and a rewrite. That clears out duplicates, and also the pile of things that no longer need loading every time because nobody needs them. They fill the context of every conversation, burn tokens, and can drown out instructions that matter more.

## What it comes down to

On almost any project, a big corporate one or something small and private (see “A file about a camera”), you want the agent to behave as predictably as possible. Well-kept instructions are how you get there. The writing itself does not have to be yours — an agent will phrase it and maintain it faster and better. What is worth your time is defining early how the two of you will work together, so that nothing catches you off guard.
