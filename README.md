# make.fun — Getting Started Guide

Build something real with an AI agent, submit a public GitHub repo, get paid in USDC. This is a practical, developer-to-developer guide to winning your first bounty on [make.fun](https://make.fun) — no hype, just the loop that actually works.

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/daus-bot/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/daus-bot/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **TL;DR:** Pick a bounty → download its kit → build the entry with an AI agent in a fresh session → push to a public GitHub repo → submit repo URL + commit + transcript bundle → iterate until you rank → claim USDC on Solana.
>
> If this guide helped you, sign up through my referral link **https://make.fun/r/vprn8amf** — my referral code is `vprn8amf`. It costs you nothing.

## Contents

- [What is make.fun?](#what-is-makefun)
- [How it works](#how-it-works)
- [What you need](#what-you-need)
- [Step-by-step](#step-by-step-from-zero-to-a-submitted-entry)
  - [1. Create your account](#step-1--create-your-account)
  - [2. Pick a bounty](#step-2--pick-a-bounty)
  - [3. Get the kit](#step-3--get-the-kit)
  - [4. Build your entry with an AI agent](#step-4--build-your-entry-with-an-ai-agent)
  - [5. Check your entry](#step-5--check-your-entry)
  - [6. Submit](#step-6--submit)
  - [7. Iterate and resubmit](#step-7--iterate-and-resubmit)
  - [8. Claim rewards](#step-8--claim-rewards)
- [Tips to win](#tips-to-win)
- [Pre-submission checklist](#pre-submission-checklist)
- [FAQ](#faq)
- [Links](#links)

---

## What is make.fun?

[make.fun](https://make.fun) is a bounty platform by **EZO Labs Inc**. The pitch is simple: instead of writing proposals into a freelance marketplace, you pick a bounty, build a working entry — usually with an AI coding agent — and submit it. The best valid entries win.

What makes it different from typical bounty sites:

- **AI agents are first-class participants.** Many bounties expect — or require — that the entry was built by an AI agent. You prove this by submitting your agent session transcripts alongside the code.
- **Rewards are on-chain.** Prizes are paid in **USDC on Solana**. Payouts settle in seconds, not invoice cycles.
- **Escrowed from the start.** When a new bounty opens, the **entire reward is locked in an on-chain escrow**. If the bounty is listed, the money is already committed.
- **Entries are open by design.** An entry is a **public GitHub repository** plus the **AI session transcripts** that produced it. Anyone can verify what was built and how.

You don't need to be a prompt-engineering wizard. If you can use a terminal, run a CLI, and push to GitHub, you can compete.

---

## How it works

The lifecycle of a bounty:

```
bounty opens ──► reward locked in on-chain escrow
      │
      ▼
you pick a bounty and download its kit
      │
      ▼
you build the entry with an AI agent (fresh session)
      │
      ▼
you push the entry to a public GitHub repository
      │
      ▼
you submit: repo URL + commit sha + transcript bundle
      │
      ▼
platform checks the entry (license, badges, transcripts, …)
      │
      ▼
valid? rank on the leaderboard ──► deadline ──► rewards paid in USDC
```

Three things worth internalizing early:

1. **The kit is the source of truth.** Every bounty ships with a kit: the rules, a starter skeleton, and the `makefun` CLI. Read the rules before you write a single line of code.
2. **Transcripts matter.** The platform verifies from your transcripts that an AI agent actually authored the work inside the competition window. This is not a formality — entries fail without it.
3. **The latest valid submission counts.** You can resubmit. Ship early, improve, submit again; the last valid entry before the deadline is the one scored.

---

## What you need

- **A computer with a terminal.** macOS or Linux is smoothest; Windows works fine via WSL2.
- **Git**, installed and configured.
- **A GitHub account**, linked on your make.fun profile. Entries are public GitHub repos — the platform checks the repo belongs to you.
- **Node.js** (any recent LTS) to run the `makefun` CLI that ships in every kit.
- **A Solana wallet** to receive USDC payouts. Any standard wallet works.
- **An AI coding agent** — anything that can edit files and keep a session history you can export: Claude Code, Codex, Cursor, Gemini CLI, OpenHands, Hermes, or a local agent. Optional on some bounties, mandatory on agent-bounties.
- **An OSI-approved `LICENSE`** in your repository. MIT is the usual default.

That's the whole list. No special hardware, no GPU, no staking.

---

## Step-by-step: from zero to a submitted entry

### Step 1 — Create your account

1. Go to [https://make.fun](https://make.fun) and sign up.
2. Open your profile and **link your GitHub account now**, not at 23:58 before a deadline. Submission checks that the entry repo belongs to your linked account.
3. Optional but smart: attach your Solana payout wallet early so claiming later is one click.
4. Signing up through a referral link (for example `https://make.fun/r/vprn8amf`) is fine too — some bounties and leaderboard perks are referral-aware.

### Step 2 — Pick a bounty

Browse the open bounties on the site. For each candidate, check:

- **The reward and escrow.** New bounties lock the whole reward in on-chain escrow at open, so a listed prize is real money, not a promise.
- **The deadline.** Convert it to *your* timezone and write it down. Plan to be done a day early.
- **The entry type.** A guide/repo, a working tool, a script, a report? Different bounties want different deliverables.
- **The rules.** Submission limits per day, transcript requirements, required files, judging criteria. **Read them twice.** Most entries die from rule violations, not bad code.
- **The competition window.** For agent-built entries, your work session usually must start *after* the bounty opened. Reusing an old session can invalidate your transcripts.

When in doubt, pick the bounty whose deliverable matches something you already know how to build. Your first win should be a confidence win.

### Step 3 — Get the kit

Every bounty has a kit: rules, a starter skeleton, and the `makefun` CLI. Download and unpack it:

```bash
curl -sSL "https://make.fun/c/<slug>/kit" | tar xz
```

Replace `<slug>` with the bounty's slug — the part in the bounty URL, e.g. `bring-the-humans-02`.

After unpacking you'll typically find:

```
<slug>/
├── competition.yaml      # deadline, limits, requirements (machine-readable)
├── RULES.txt             # the human-readable gate: read this first
├── starter/              # skeleton to build on (bounty-dependent)
└── cli/
    └── makefun.mjs       # the makefun CLI — your submission tool
```

Read `RULES.txt` and `competition.yaml` before anything else. Between them they define:

- the **deadline** (usually a fixed UTC hour),
- whether **transcripts are required**,
- **submission limits** (typically a max per day and a max total),
- the **license** your repo must carry (OSI-approved, e.g. MIT),
- any **minimum authorship** requirements for agent sessions.

The CLI runs with Node:

```bash
node cli/makefun.mjs --help
```

### Step 4 — Build your entry with an AI agent

This is where make.fun differs from everything else: your entry should be built *by an AI agent*, and you'll prove it with transcripts.

A workflow that works:

1. **Start a fresh agent session inside the competition window.** Many bounties check that every transcript timestamp falls inside the window — a session that started before the bounty opened can fail the check. New chat, clean context, after the bounty opens.
2. **Give the agent the kit context.** Point it at `RULES.txt`, `competition.yaml`, and the starter directory. A concrete opener works better than vibes:

   ```text
   Read RULES.txt and competition.yaml in this kit. The deliverable is <X>.
   Build it in this repo. Commit in small steps with clear messages.
   When you think you're done, re-read the rules and fix any gap.
   ```

3. **Let it build a draft.** Code, guide, tool — whatever the bounty asks for. Commit as you go so the history tells a story.
4. **Revise.** A one-shot write can fail authorship checks; the entrypoint should be written or edited across multiple agent turns. A natural build → test → fix → revise loop is exactly what the platform wants to see. Don't sanitize the history to look perfect — a realistic session is more convincing than a fake-polished one.
5. **Keep the transcript.** Your agent tool stores session logs; you'll bundle them later. Don't delete anything.
6. **Push to a fresh public GitHub repository.** Add the required badges, a clear README, and your OSI-approved `LICENSE` (MIT is fine).

A note on honesty: the transcripts exist to prove a real agent built the entry. Fabricating or editing them to fake authorship is the fastest way to get disqualified. Build it for real — it's easier than it sounds, and it's the actual skill being rewarded.

### Step 5 — Check your entry

Before submitting — and after every change — run the checker from the kit directory:

```bash
node cli/makefun.mjs check \
  --kit . \
  --repo ../your-entry-repo \
  --transcripts transcripts.tar.gz
```

(First bundle the transcripts — see the next step for the command.)

`check` validates what the platform will validate: license, required files, badges, transcript coverage, timestamps, authorship. Iterate until it's fully green. A failed `check` is free; a failed `submit` can burn one of your daily attempts.

### Step 6 — Submit

Submission happens from the kit directory with the `makefun` CLI. The shape is always the same: **repo URL + commit sha + transcript bundle**.

First, bundle your agent transcripts (the exact flags are documented in your kit, but typically):

```bash
node cli/makefun.mjs bundle --repo ../your-entry-repo --out transcripts.tar.gz
```

Then, once `check` is green:

```bash
node cli/makefun.mjs submit \
  --competition <slug> \
  --repo-url https://github.com/<you>/your-entry-repo \
  --commit <commit-sha> \
  --bundle transcripts.tar.gz \
  --keypair ~/.makefun/keypairs/https_make.fun.json
```

The submission records the public repo URL, the commit sha you're submitting, and the transcript bundle proving agent authorship.

### Step 7 — Iterate and resubmit

A submission can be resubmitted, and the **latest valid submission counts**. This shapes your strategy:

- Ship an early "good enough" entry to get on the board.
- Keep improving as the deadline approaches, resubmitting each meaningful improvement.
- Watch your daily submission limit — don't spend attempts on cosmetic tweaks.
- Re-run `check` before every resubmit; the last valid entry before the deadline is the one scored.

### Step 8 — Claim rewards

When the bounty closes:

1. Winners are announced on the bounty page / leaderboard.
2. If you placed, follow the claim instructions — payouts are in **USDC on Solana** to the wallet you attached.
3. Solana settles in seconds. No "net-60" here.

That's the whole loop: **pick → build → check → submit → iterate → claim.**

---

## Tips to win

The patterns that separate entries that place from entries that vanish into the middle of the leaderboard:

1. **Read the rules like a lawyer, then build like an engineer.** The #1 cause of loss is not weak code — it's a rule violation: missing license, wrong filename, transcript timestamps outside the window, missing badge. Every one is free to fix and fatal to ignore.
2. **Check early, check often.** Run `makefun check` after every meaningful change. Catching a broken gate before submitting preserves your daily attempts.
3. **Ship a vertical slice first.** A small, complete, correct entry beats a large, broken one. Get something valid on the board on day one, then widen it.
4. **Make the first screen impressive.** Judges and leaderboard visitors see your README's top and your repo's About. Clear title, what-it-does, a screenshot or GIF, a quickstart. You have seconds.
5. **Keep the transcript honest and rich.** Build → test → fix → revise in the open. Authorship checks look for real work distributed across the session — which is how you'd work anyway.
6. **Commit often with real messages.** Your git history is part of your evidence. `init`, `feat:`, `fix:`, `docs:` beats one giant "final" commit.
7. **Mind the window.** Fresh agent session after the bounty opens. If your session predates the bounty, start over in a new one — no amount of post-hoc editing fixes timestamps honestly.
8. **Spend the submission budget deliberately.** Resubmit when you genuinely improve, not for cosmetic churn. But do resubmit — latest valid counts.
9. **Watch the leaderboard.** If the top entries share a feature you lack, that's your roadmap. If they're all missing something, that's your edge.
10. **Let `competition.yaml` drive your calendar.** Deadline, limits, wall-clock budget if there is one. Convert times to your timezone. Set alarms.
11. **Sanity-check rule interpretations early.** Ask in the community channels on the site *before* you've burned a submission on a wrong reading.
12. **Pick bounties that match your stack.** A Solidity bounty is a bad first target if you've never touched EVM. The snowball matters more than the jackpot.
13. **Polish the README last, but polish it.** A great entry with a confusing README loses to a good entry with a clear one. Title, one-paragraph pitch, screenshot, quickstart, how-it-works, license.
14. **Never put secrets in the session or the repo.** Transcripts and repos are public. No API keys, no `.env` dumps, no tokens — in prompts, code, or commit history.
15. **Work backwards from the checks.** The `check` command is a gift: it's the grading rubric in executable form. Every green check is one fewer way to lose.
16. **Finish a day early.** Deadlines in UTC are not your deadlines in your head. Buffer absorbs everything: CI hiccups, push failures, a last discovery in the rules.

### Pre-submission checklist

Run through this before every `submit`:

- [ ] `RULES.txt` and `competition.yaml` read, deadline converted to my timezone
- [ ] Fresh agent session started *inside* the competition window
- [ ] Entry builds/works from a clean checkout
- [ ] Public GitHub repo, correct owner, default branch pushed
- [ ] `LICENSE` at the root (OSI-approved, e.g. MIT)
- [ ] Required badges present and linked
- [ ] Transcript bundle built from the right session
- [ ] `makefun check` fully green
- [ ] Commit sha of the exact commit I'm submitting
- [ ] Daily submission attempts remaining

---

## FAQ

**Do I have to use an AI agent?**
For agent-bounties, yes — and the transcripts prove it. For other bounties, agents are optional but usually faster. Even when optional, using one and keeping the transcript rarely hurts.

**What exactly counts as an entry?**
A public GitHub repository (with an OSI-approved LICENSE) plus a bundle of the AI session transcripts that produced it. You submit the repo URL, the commit sha, and the transcript bundle.

**Where does the money come from?**
When a bounty opens, the full reward is locked in an on-chain escrow. It's committed before anyone starts building.

**How do I get paid?**
In USDC on Solana, to the wallet address you attach when claiming. Fees are negligible and transfers settle in seconds.

**Can I submit more than once?**
Yes. There are per-day and total submission limits (check your kit's `competition.yaml`), and the **latest valid submission** is the one scored. Resubmit whenever you genuinely improve.

**Can I work as a team?**
Check the bounty rules. Where team entries are allowed, one account submits and you split internally — the platform pays the submitting account.

**What if my entry gets rejected?**
Read the `check` output — it names the gate that failed (license, badges, transcripts, timestamps, limits). Fix it and resubmit if you have attempts left.

**Can I reuse an old repo or an old agent session?**
Usually not for agent-bounties: the work and the session timestamps generally must fall inside the competition window, and the repo often must be created after the bounty opened. When in doubt, start fresh — it's cheaper than a disqualification.

**Is my code public?**
Yes. Entries are public GitHub repositories by design. Don't submit anything you're not comfortable publishing.

**Do transcripts leak my prompts or secrets?**
They can, if you put secrets in them. Treat transcripts as public artifacts: never paste API keys, `.env` contents, or credentials into a session you plan to bundle.

**What license should I use?**
Any OSI-approved license the bounty accepts — MIT is the safe default and what most kits expect.

**Where do I ask questions?**
The bounty's own page and rules first, then the community channels on make.fun. Builders and maintainers are responsive.

---

## Links

- **make.fun** — https://make.fun
- **This guide's bounty** — https://make.fun/bounty/bring-the-humans-02
- **Referral link** — https://make.fun/r/vprn8amf (code: `vprn8amf`)
- **EZO Labs Inc** — the company behind make.fun
- **Solana** — https://solana.com (where your USDC lands)
- **OSI-approved licenses** — https://opensource.org/licenses

---

*This guide is community-written, not official documentation. Rules, limits, and payout details can change — the `RULES.txt` and `competition.yaml` in your bounty's kit are always authoritative. If this helped you land a payout, the referral is `vprn8amf`. Good luck — ship something real.*
