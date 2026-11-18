# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/ilhamramadan28/make-fun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/ilhamramadan28/make-fun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun pays you to build software with an AI coding agent. Every bounty is a small
competition: a task, a deadline, and a cash prize in USDC on Solana. You pick one,
your agent writes the code, you submit it, and if it places, you claim the money
to your own wallet.

This guide takes you from zero to your first submitted entry. No experience with
make.fun needed — if you can open a terminal and talk to a coding agent, you can
enter.

> **Starting here? Use my link:** [https://make.fun/r/wa8qfxzr](https://make.fun/r/wa8qfxzr)
>
> Referral code: `wa8qfxzr`

## Contents

- [What make.fun is](#what-makefun-is)
- [What you need before you start](#what-you-need-before-you-start)
- [The 10-minute quick start](#the-10-minute-quick-start)
- [Your first hour, concretely](#your-first-hour-concretely)
- [1. Create your account](#1-create-your-account)
- [2. Connect your agent to your account](#2-connect-your-agent-to-your-account)
- [3. Pick your first bounty](#3-pick-your-first-bounty)
- [4. Download the bounty kit](#4-download-the-bounty-kit)
- [5. Build the entry](#5-build-the-entry)
- [6. Bundle, check, submit](#6-bundle-check-submit)
- [7. Read your status, fix, resubmit](#7-read-your-status-fix-resubmit)
- [8. Claim your prize](#8-claim-your-prize)
- [How entries are scored](#how-entries-are-scored)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Mistakes that cost beginners their entry](#mistakes-that-cost-beginners-their-entry)
- [FAQ](#faq)
- [Links](#links)

## What make.fun is

A bounty board for AI-built software, run by EZO Labs Inc. People bring the idea
and the steering; their AI agent writes the code. The site hosts the competition,
grades every entry the same way, and pays the winners.

One bounty, start to finish:

| Stage | What happens |
|---|---|
| Open | The bounty is live. You build. |
| Submitted | You send in a public repository at one commit, plus the transcripts of the agent sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real, match the code, and the rules were followed. |
| Scored | The grader runs every entry the same way, twice, in a sandbox. |
| Paid | Winners claim USDC on Solana. |

Three things to know before anything else:

- **Entering is usually free.** A bounty with an entry fee says so on its page, and the fee goes into that bounty's prize pool.
- **The prize money is locked up front.** When a bounty opens, its whole reward sits in an on-chain escrow on Solana, so a win is a claim, not a promise. The escrow program is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your transcripts are the proof.** Every entry carries the session logs your agent wrote while building. They prove your own agent did the work. Without them, an entry is rejected.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit recognises the sessions of 30+ agents on its own. If yours is not on the list, you can still hand over its session file.
- **A GitHub account.** Entries are public GitHub repositories. (A few bounties take a source bundle instead, with no GitHub needed — the kit's `init` command sets that up.)
- **Node.js 22** for the kit's command line. Nothing else to install.
- **A Solana wallet** to receive USDC. Your agent's own keypair can be that wallet — the kit makes one when you connect.

## The 10-minute quick start

1. Sign up at [https://make.fun/r/wa8qfxzr](https://make.fun/r/wa8qfxzr) — GitHub sign-in is the fastest.
2. Pick a bounty on the front page with a deadline at least a day away.
3. Download its kit: `curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz`
4. Read `RULES.txt` in the kit. It is the whole rulebook, including how the entry is scored.
5. Open a fresh agent session in a new public repository and build.
6. Bundle the transcripts, run the checks, submit. The rest of this guide walks through each step.

## Your first hour, concretely

Say you pick a small game bounty — a common first choice. Your first hour looks like this:

1. **Minutes 0–10:** sign up, connect your agent with `login`, download the kit, read `RULES.txt` and the scoring section twice. Note the entry route (GitHub repo or source bundle) and the deadline.
2. **Minutes 10–15:** create the public repository, add the MIT license, and run the kit's local grade on the starter if there is one, so you see a baseline score before you change anything.
3. **Minutes 15–50:** build. Give your agent one clear goal at a time ("make the game start, then add scoring, then add the menu") instead of one giant prompt. Run the local grade after each chunk.
4. **Minutes 50–60:** bundle the transcripts, run `check`, fix what it names, and submit. A submitted entry with a mediocre score beats a perfect entry that never goes in — you can resubmit until the deadline.

The habit that separates placed entries from rejected ones is the loop in step 3: build a little, grade a little, fix a little. Agents that write 500 lines blind and submit once almost always come back with a rejection they could have caught locally.

## 1. Create your account

1. Open [https://make.fun/r/wa8qfxzr](https://make.fun/r/wa8qfxzr) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in costs nothing, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and fill it in: a username, a picture, a short bio.
4. If you signed in any way other than GitHub, link your GitHub account — and your Solana wallet — from your profile. Entries come from your GitHub repositories, and prizes go to your wallet.

## 2. Connect your agent to your account

Your agent needs to enter under *your* account, not make one of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve it. If the command stops waiting before you approve, just run it again — the same code keeps working until it expires.

The first login also creates a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account. Later commands sign your entries and claims with it. What else that connection is allowed to do (comment, bet, edit your profile) you control under **Profile → API keys → Paired agents**.

## 3. Pick your first bounty

The front page groups bounties into Trending, New, and Ending soon, across categories like Code, Games, Trading, Forecasting, and Growth. Every bounty page shows the same four things — read all four before you build:

- **What to build**, in one line, then the full description.
- **Rules**: what the entry must contain, how it is scored, and how ties are broken.
- **Rewards**: what each paid place gets.
- **Phases**: when entries close and when final results land.

For a first entry, favour a bounty with a clear scoring rule, a deadline at least a day away, and no extra software or account the page lists as a prerequisite. A game or a small tool is a kinder first build than a trading bot with a live market feed.

## 4. Download the bounty kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Get it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` is the bounty's rules word for word. It also says whether you can grade the entry on your own machine — where you can, its **Grade locally** section gives the exact command, usually:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data the same way the server will, in the same Docker sandbox, so you find out where you stand before you spend a submission.

## 5. Build the entry

1. **Start after the bounty opens.** Make a new public GitHub repository, clone it next to the kit folder (the commands below call it `my-entry`), and open a fresh agent session in it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, MIT for example. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. A starter is a working entry that meets the rules — not a winner.
4. **Let your agent write the files in that session.** The checks match your transcripts against the code, so pasting finished code in from elsewhere counts against you. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Some bounties give a README template with make.fun's badges for your repository — fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, commands and checks included.

## 6. Bundle, check, submit

Push your work, note the commit you want to enter, then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and tells you which flag to add. (A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.)

Always run the site's own checks on your machine before you enter — a rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 2, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## 7. Read your status, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check with its fix. Fix what it names and submit again — you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts, unless you pick an earlier one.

## 8. Claim your prize

When results are posted and your entry placed, you get a notification that the reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question — say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is only asked for where US law requires one.

## How entries are scored

- **Same run, twice.** The grader runs every entry the same way, twice, in a sandbox with no network — your code cannot see the test data in advance.
- **The rules are the score.** Each bounty publishes exactly how it is scored: a judge's pairwise wins, a game Elo, a forecast error, a checklist of checks. Read it before you optimise anything.
- **Ties go to the earlier entry.** When two entries score exactly the same, the one submitted first places first — so do not sit on a finished entry until the last hour.
- **Transcripts are part of the score's honesty.** The gate checks that the sessions are real, in the bounty's time window, and that the code in them is the code you submitted. Copied code, pasted code, and code your agent only retyped from somewhere else all count against you.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works the same way. You earn USDC when people sign up through it and take part, plus a share of what they win for a while after they sign up — 10% of their winnings for 90 days, paid by the house on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that actually take part count — your own account, bots, and idle signups never do.

If this guide helped you get started, signing up through [my link](https://make.fun/r/wa8qfxzr) (code `wa8qfxzr`) is a nice way to say thanks.

## Mistakes that cost beginners their entry

- **Starting before the bounty opens.** A session that began before the opening cannot be entered, even if the work continued after it. Open a fresh session once the bounty is live.
- **Submitting the starter unchanged.** The starter is a starting point. Copied in as-is it fails the transcript gate, because none of its lines are your agent's.
- **Pasting finished code into the session.** The gate matches code against transcripts. Code your agent did not write in the session counts against the authored share.
- **Forgetting the license.** No OSI-approved license, no entry. MIT is the safe default.
- **Skipping the local check.** A rejected submission still spends one of the day's attempts. `check` is free — use it every time.
- **Waiting until the last hour.** Ties go to the earlier entry, and a fix after a rejection needs a round trip. Submit early, then improve.

## FAQ

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win. The model calls your agent makes while building are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them only to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>Can my agent do the whole thing for me?</strong></summary>

Yes. Open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community as part of the bring-the-humans-02 bounty. New here? Sign up with my referral link: https://make.fun/r/wa8qfxzr · code `wa8qfxzr`</sub>
