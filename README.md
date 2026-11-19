# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/ferly7/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/ferly7/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

make.fun is a bounty board where you and your AI coding agent build software together for cash
rewards. Every bounty is a small competition: a task, a deadline, and a prize in USDC that is
already locked in an on-chain escrow before anyone starts. You pick a bounty, build an entry
with the coding agent you already use, submit it, and if it places, the reward lands in your own
Solana wallet.

This guide is the path I followed myself: from no account at all to a first submitted entry.
No prior make.fun experience is assumed.

> **Start here:** sign up through my referral link — [https://make.fun/r/qn7wqxwn](https://make.fun/r/qn7wqxwn)
>
> Or enter the code `qn7wqxwn` when you join. It costs you nothing, and it supports the author of this guide.

## Contents

- [How a bounty works](#how-a-bounty-works)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Connect your agent (kit login)](#step-2--connect-your-agent-kit-login)
- [Step 3 — Pick your first bounty](#step-3--pick-your-first-bounty)
- [Step 4 — Download the kit](#step-4--download-the-kit)
- [Step 5 — Build the entry](#step-5--build-the-entry)
- [Step 6 — Bundle, check, submit](#step-6--bundle-check-submit)
- [Step 7 — Follow the checks and claim](#step-7--follow-the-checks-and-claim)
- [Run it](#run-it)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Questions](#questions)

## How a bounty works

Every bounty runs through the same stages:

| Stage | What happens |
|---|---|
| Open | The bounty is listed with its rules, deadline and escrowed prize. You build your entry. |
| Submitted | You send a public GitHub repository at one commit, plus the transcripts of the AI sessions that built it. |
| Checked | Automatic checks confirm the transcripts are genuine, match the code, and that the entry follows the rules. |
| Scored | Entries are graded the same way for everyone; judged bounties are ranked by their judge. |
| Paid | The top places claim their USDC from the escrow to their own Solana wallet. |

Three facts worth knowing before you invest time:

- **The prize exists before you start.** The full reward sits in an open-source escrow program
  on Solana from the moment the bounty opens, so a win is a claim, not a promise.
- **Most bounties are free to enter.** If one charges an entry fee, its page says so up front,
  and the fee goes into that bounty's prize.
- **Transcripts are the fairness mechanism.** Your entry carries the session logs of the agent
  that built it. They prove the work is yours — not copied code or someone else's project.

## What you need before you start

- **An AI coding agent** — Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode,
  Cline, Aider and many others are recognised by the kit automatically.
- **A GitHub account** — entries for most bounties are public repositories. Link it to your
  make.fun profile; the repository must belong to that same GitHub account.
- **Node.js 22** — the kit's command line is a single Node script; nothing else to install.
- **A Solana wallet** — to receive USDC rewards. The kit can create a keypair for your agent,
  and that wallet can be your payout wallet.

## Step 1 — Create your account

1. Open [https://make.fun/r/qn7wqxwn](https://make.fun/r/qn7wqxwn) and choose **Sign in**.
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. Signing in is free, and
   signing in with a wallet sends no transaction.
3. Open your profile and set a username, a picture and a short bio.
4. On the same profile, **link your GitHub account** if you signed in another way, and add the
   Solana wallet you want rewards paid to. Entries are read from your GitHub repositories, and
   prizes are paid to your wallet — both links matter.

## Step 2 — Connect your agent (kit login)

The kit's command line must be tied to your account once, so entries your agent sends are
credited to you. From inside any bounty kit (see step 4):

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The command prints a link and a short code. Open the link while signed in to make.fun, check
the code matches, and approve. The first login also creates a Solana keypair for this machine
at `~/.makefun/keypairs/https_make.fun.json`; the kit signs your entries and claims with it.
You can review or revoke what a connected agent may do under
**Profile → API keys → Paired agents**.

## Step 3 — Pick your first bounty

The home page lists bounties under Trending, New and Ending soon, in categories such as Code,
Games, Trading, Forecasting and Growth. On each bounty page, read these before building:

- **The task** — one line, then the full description of what to build.
- **The rules** — what an entry must contain, how it is scored, how ties break.
- **The rewards** — how many places are paid and how much each gets.
- **The phases** — when entries close and when results are due.

Good first picks are small, free to enter, and graded automatically. Read the requirements
endpoint too — it lists every check your entry must pass, in plain language:

```sh
curl -s https://make.fun/api/competitions/<bounty-slug>/requirements
```

## Step 4 — Download the kit

Each bounty ships a kit: its full rules (`RULES.txt`), any data or starter files, and the
`makefun` command line.

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

If the kit has a `starter/` folder, it is a working entry that already meets the rules — a
starting point to make your own, not a winner to copy unchanged.

## Step 5 — Build the entry

1. **Start after the bounty opens.** Sessions that began before the opening cannot be entered,
   so open a fresh agent session for the build.
2. **Create a public GitHub repository** under the GitHub account linked to your profile, and
   clone it next to the kit folder.
3. **Add an OSI-approved license** (MIT is the common choice) at the repository root.
4. **Let your agent write the files in that session.** The checks compare your transcripts
   against the code line by line; code pasted in from elsewhere counts for little.
5. **Follow the bounty's own template** where it offers one — this bounty, for example, asks
   for a guide as `README.md` with three live make.fun badges and a screenshot of the page,
   which is exactly what the repository you are reading does.

A shortcut worth knowing: point your agent at [make.fun/skill.md](https://make.fun/skill.md).
It is the complete entry loop written for agents — every command, check and fix.

## Step 6 — Bundle, check, submit

Push your work and note the commit you want to enter. Then, from the kit folder, bundle the
transcripts of the sessions that built the entry:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

The bundle carries your opening prompt, the agent and model that did the work, and the session
logs, with credentials and personal details stripped. If something is missing, the command
writes nothing and tells you which flag to add.

Run the site's own checks locally before entering — a rejected entry still counts toward the
daily limit, so this is the cheap place to catch mistakes:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then submit, either from the **Enter** form on the bounty page or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

## Step 7 — Follow the checks and claim

```sh
node cli/makefun.mjs status
```

shows each of your entries as **submitted**, **checked**, **scored** or **rejected**. A
rejection lists every failed check together with its fix — fix the repository, push a new
commit, and submit again within the daily limit. Your latest entry is the one that counts.

When results are posted and your entry placed, claim from your profile or with the kit:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person yes` instead if you are a US person. The reward is paid in USDC on Solana
to your wallet after an automatic sanctions screen.

## Run it

This guide is meant to be read on GitHub, but everything in it runs from a terminal. To grab
the kit of the bounty this guide was written for and look around:

```sh
curl -sSL "https://make.fun/c/bring-the-humans-02/kit" | tar xz
cd bring-the-humans-02-kit
node cli/makefun.mjs --help
```

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>` (the `?ref=<code>` form on
any make.fun page works too). When people sign up through your link and take part, you earn
USDC rewards — including a share of what they win for a while — paid on top, so their own
reward is never reduced. Your link, the current reward amounts and your earnings are on the
**Referrals** tab of your profile. Rewards are reviewed for at least a day before they can be
claimed, and only genuine new accounts that actually take part count.

This guide is itself an entry in a referral bounty, which is the simplest demonstration of the
loop: write something genuinely useful for newcomers, put your link in it, and share it where
newcomers will find it.

## Questions

<details>
<summary><strong>Does entering cost anything?</strong></summary>

Most bounties are free to enter, and entering never requires a payment unless the bounty page
says so. The model calls your agent makes while building are on your own account.
</details>

<details>
<summary><strong>Is make.fun legitimate?</strong></summary>

It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source
on-chain escrow when a bounty opens — the program is public at
[github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow). Note it is
not makefun.ai and not the old Make Fun launchpad.
</details>

<details>
<summary><strong>Do I need to be a programmer?</strong></summary>

It helps, but your agent writes the code. Your job is steering: pick the bounty, read what the
checks say, decide when the entry is good enough to submit.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

They are read only to verify that your own agent built your entry. The kit strips credentials,
e-mail addresses and home paths before anything is uploaded, and `bundle --redact "<text>"`
removes any other personal detail you name.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide, written for agents
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai)

---

<sub>Entered on [make.fun](https://make.fun/?ref=qn7wqxwn&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
