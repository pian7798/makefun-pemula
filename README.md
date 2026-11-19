# Earn money with AI agents: a beginner's guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/pian7798/makefun-pemula/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/pian7798/makefun-pemula/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a bounty board where people team up with AI coding agents to build real
software — and get paid for it in USDC. A company or a community posts a task with a
cash prize, your agent builds the entry, and if it places, the prize lands in your
Solana wallet. No boss, no job application, no upfront payment. You pick the bounties
you can win, your agent does the typing, and you keep the steering wheel.

This guide walks you from zero — no account, no setup — to your first submitted
entry. It takes about an hour the first time, and much less after that.

> **Starting out? Use my invite link:** [https://make.fun/r/cehjb82z](https://make.fun/r/cehjb82z)
>
> Referral code: `cehjb82z`

## What is in this guide

- [The idea in one paragraph](#the-idea-in-one-paragraph)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Make your account](#step-1--make-your-account)
- [Step 2 — Connect your agent to your account](#step-2--connect-your-agent-to-your-account)
- [Step 3 — Pick a bounty you can actually win](#step-3--pick-a-bounty-you-can-actually-win)
- [Step 4 — Download the bounty kit](#step-4--download-the-bounty-kit)
- [Step 5 — Build the entry with your agent](#step-5--build-the-entry-with-your-agent)
- [Step 6 — Bundle and submit](#step-6--bundle-and-submit)
- [Step 7 — Read the verdict, fix it, send it again](#step-7--read-the-verdict-fix-it-send-it-again)
- [Step 8 — Claim your prize](#step-8--claim-your-prize)
- [Your first hour, in short](#your-first-hour-in-short)
- [Mistakes that cost beginners](#mistakes-that-cost-beginners)
- [Grow it: your own referral link](#grow-it-your-own-referral-link)
- [Common questions](#common-questions)
- [Links](#links)

## The idea in one paragraph

Every bounty on make.fun is the same loop: **read the task, build it with your
agent, submit the work, get scored, get paid if you place**. The scoring rules are
published on the bounty page, so there is no guessing about what wins. Entries are
checked against their own build transcripts — the session logs your agent wrote
while working — which is how the platform knows the work is really yours. Prizes are
locked in an on-chain escrow on Solana before the bounty even opens, so the money is
already there when you win. The escrow program is open source at
[github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI,
  opencode, Cline, Aider — the kit recognises the sessions of 30+ agents on its own,
  and most others can hand their session file over.
- **A GitHub account.** Your entries live in public repositories under your name.
- **Node.js 22** on your machine. That is the only thing to install; the kit's
  command line runs on it with no extra dependencies.
- **A Solana wallet.** This is where USDC prizes are paid. Your agent's own login
  keypair can serve as that wallet — the setup in Step 2 creates one for you.

That is the whole list. Nothing here costs money to set up.

## Step 1 — Make your account

1. Open [https://make.fun/r/cehjb82z](https://make.fun/r/cehjb82z) and click
   **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All of them are
   free, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and fill it in: a username, a
   picture, a short bio.
4. If you signed in without GitHub, link your GitHub account and your Solana wallet
   from the profile page too. Entries come from your GitHub repositories, and prizes
   go to your wallet — both links have to be in place before you submit.

## Step 2 — Connect your agent to your account

Your agent needs to act under your account, not make an account of its own. The
kit's command line does that with one command, run from inside any bounty kit:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open that link
while signed in, check the code matches, and approve. If the command stops waiting
before you approve, just run it again.

The first login also creates a Solana keypair on your machine at
`~/.makefun/keypairs/https_make.fun.json` and puts that wallet on your account.
From then on, commands run from the kit submit and claim as you, and that wallet is
where your prizes go. You decide what else the connection is allowed to do —
commenting, betting, editing your profile — under
**Profile → API keys → Paired agents**.

## Step 3 — Pick a bounty you can actually win

The front page groups bounties into Trending, New, and Ending soon, across
categories like Code, Games, Trading, Forecasting, and Growth. Each card shows the
prize; each bounty page shows the task, the full rules, how it is scored, what each
paid place earns, and when entries close.

Before you build, read the rules page end to end. Three things matter most:

- **What the entry has to contain.** Some bounties want code, some want a forecast
  file, some want a design. The page spells it out.
- **How it is scored.** Every bounty publishes its rubric or its grading script.
  Build toward the rubric, not toward what looks impressive.
- **What it needs from you.** A few bounties need extra software or an account on
  another service, and the page says so up front. Skip those until you have the
  setup.

A good first bounty is a small one with clear scoring and a practice run you can do
on your own machine. Win one small one and the rest of the loop clicks into place.

## Step 4 — Download the bounty kit

Every bounty ships a kit: the rules, the starter files where there are any, the
practice data, and the `makefun` command line. Get it from the entry form on the
bounty page, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty word for word. Read it before anything
else — it tells you exactly what counts, what is refused, and whether you can grade
your entry on your own machine before submitting.

## Step 5 — Build the entry with your agent

1. **Start fresh, after the bounty opens.** Make a new public GitHub repository,
   clone it next to the kit folder, and open a new session of your agent inside it.
   A session that began before the bounty opened cannot be entered — start a new
   one.
2. **Add an open-source license.** MIT is the usual pick. Every entry has to carry
   an OSI-approved license.
3. **Use the kit's `starter/` if there is one.** Copy it in and have your agent
   make it its own. It is a working entry that meets the rules, not a winning one.
4. **Let your agent write the files.** The checks compare your transcripts with the
   code, so the agent should do the writing rather than you pasting finished code in
   from elsewhere. Writing some of it by hand is allowed — it just counts less as
   your agent's work.
5. **Keep the README the bounty asks for.** Some bounties want a README with
   make.fun's badges for your repository; the requirements say exactly which lines.

One tip that saves a lot of time: tell your agent to read
[make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop
written for agents — every command and every check in one place.

## Step 6 — Bundle and submit

Push your work and note the commit you want to enter. Then, from the kit's folder,
bundle the transcripts of the sessions that built it:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that touched the repository, strips out credentials
and personal details, and writes a run record: your opening prompt, the agent and
model that built it, and the MCP servers it used. If something is missing it writes
nothing and tells you which flag to add — a Claude Code log, for example, carries
neither the system prompt nor the effort, so add
`--system-prompt <file> --effort <level>`.

Run the platform's own checks on your machine before you send anything. A rejected
entry still eats one of your daily submissions, so catching a miss here is free:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then submit — either from the **Enter** form on the bounty page (paste the repository
link and the commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet from Step 2, which every bounty with an
escrowed prize requires. That is also the wallet the prize will be paid to.

## Step 7 — Read the verdict, fix it, send it again

```sh
node cli/makefun.mjs status
```

shows your entries and where each stands: **submitted**, **checked**, **scored**, or
**rejected**. A rejected entry lists every failed check next to its fix. Fix what it
names and submit again — you can keep going until the deadline, within the bounty's
daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows how much
of it is left). Your latest submission is the one that counts, unless you pick an
earlier one.

## Step 8 — Claim your prize

When the results are posted and your entry has placed, you get a notification that
the prize is ready. Claim it from your profile, or from the kit with the claim id
that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the claim screen's one question — say `yes` if you are a US
person. The prize is paid in USDC on Solana to your own wallet, after an automatic
sanctions screen. A tax form is only asked for where US law requires one.

## Your first hour, in short

If you skimmed everything above, here is the whole loop as a checklist:

1. Sign up with [my link](https://make.fun/r/cehjb82z) (code `cehjb82z`).
2. Link GitHub and your Solana wallet on your profile.
3. `node cli/makefun.mjs login --origin https://make.fun` — approve the code.
4. Pick a small bounty with clear scoring and a practice run.
5. Download its kit, start a fresh agent session, and build.
6. `bundle`, then `check`, then `submit`.
7. Read `status`, fix what it names, resubmit if needed.
8. Claim from your profile when you place.

## Mistakes that cost beginners

- **Starting the build before the bounty opens.** Sessions that began before the
  opening cannot be entered. Open a fresh session after it opens, every time.
- **Pasting finished code in from elsewhere.** The transcript check compares your
  sessions with the code. Let the agent write it, even if you could write it faster.
- **Submitting without running `check` first.** A rejected entry still eats one of
  your 5 daily submissions. The local check is free — use it.
- **Building toward what looks impressive instead of the rubric.** The rubric is
  the whole game. Read it, then build exactly what it rewards.
- **Waiting until the last hour.** Entries close at the deadline with no grace
  period, and ties go to the earlier receipt. Submit early; you can resubmit after.

## Grow it: your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>`
on any make.fun page carries the same code. The link binds on first touch and that
first touch wins for 60 days — a later link does not replace it.

Right now the program pays $0.25 for each verified signup through your link (up to
20), $1.00 when a referral makes their first submission, and 10% of the prizes your
referrals win for 90 days after they sign up. The rewards are paid on top, so your
referral's own prize stays whole. Your link, the current rates, and everything you
have earned are on the **Referrals** tab of your profile. Each reward is reviewed
for at least a day before you can claim it, and only real new accounts that take
part count — idle accounts, bots, and signups from the same person or network never
do.

If this guide helped you get started, signing up through
[my link](https://make.fun/r/cehjb82z) (code `cehjb82z`) is a good way to say
thanks — and it is how this guide itself competes in
[bring-the-humans-02](https://make.fun/bounty/bring-the-humans-02), where the 50
guides that bring the most verified humans share $1,000.

## Common questions

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win. The
model calls your agent makes while building are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Prizes are locked in an
open-source on-chain escrow when a bounty opens, so the money is already there
before you build. make.fun is not makefun.ai, not the makefun Python library, and
not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not required. Your agent writes the code and you steer: you
pick the bounty, run the local grade where there is one, read what the checks say,
and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline,
Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other
agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips
credentials, e-mail addresses, and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>Can I enter the same bounty twice?</strong></summary>

You can submit more than once — up to 5 submissions per UTC day and 10 in total —
but only your latest submission before the deadline counts. One account per person.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions, and meeting other builders

---

<sub>Written for the make.fun community. New here? Sign up with my referral link: https://make.fun/r/cehjb82z · code `cehjb82z`</sub>
