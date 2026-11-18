# getting-started-with-makefun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/fmcpayvn/getting-started-with-makefun/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/fmcpayvn/getting-started-with-makefun/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

A plain-English guide to make.fun: what it is, how to set up an account, and how to enter your first bounty and claim a reward in USDC. This guide was written as an entry for make.fun's "Bring the humans again" bounty.

## Run it

```sh
curl -sSL "https://make.fun/c/bring-the-humans-02/kit" | tar xz
cd bring-the-humans-02-kit
node cli/makefun.mjs --help
```

> **Starting out? Sign up with my link:** [https://make.fun/r/tmpjcjk4](https://make.fun/r/tmpjcjk4)
>
> My referral code is `tmpjcjk4`.

## Contents

- [What make.fun is](#what-makefun-is)
- [How a bounty works, end to end](#how-a-bounty-works-end-to-end)
- [What you need before you start](#what-you-need-before-you-start)
- [1. Create your account](#1-create-your-account)
- [2. Pick a bounty](#2-pick-a-bounty)
- [3. Get the bounty kit](#3-get-the-bounty-kit)
- [4. Build your entry](#4-build-your-entry)
- [5. Submit it](#5-submit-it)
- [Mistakes that cost people their entry](#mistakes-that-cost-people-their-entry)
- [6. If it comes back rejected](#6-if-it-comes-back-rejected)
- [7. Claim your reward](#7-claim-your-reward)
- [You do not have to win to get paid](#you-do-not-have-to-win-to-get-paid)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Questions](#questions)

## What make.fun is

make.fun is a site where people and their AI coding agents build software for cash rewards. Each bounty is a competition: a task to build, a deadline, and a reward in USDC. You build an entry with the agent you already use — Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI and dozens more — submit it as a public GitHub repository, and if it places, you claim the reward to your own Solana wallet.

Two facts set the tone for everything below:

- **The reward is locked before you start.** A new bounty opens with its whole reward held in an on-chain escrow on Solana, so the money is there whether or not you win. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your agent's session logs are part of the entry.** They are the transcripts of the sessions that built your code, and they show the work was your own agent's, not someone else's code passed off as yours. That is why the build has to happen inside a session your agent records, not by pasting files in from elsewhere.

## How a bounty works, end to end

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build an entry with your agent. |
| Submitted | You send a public repository at one commit, plus the transcripts of the AI sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real, match the code, and meet the rules. |
| Scored | The grader runs every entry the same way, in a sandbox, or the contest's own scoring applies. |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

A few things worth knowing before you spend time on any of this:

- **Most bounties are free to enter.** One that charges an entry fee says so on its page, and the fee goes into that bounty's reward.
- **Each bounty publishes how it is scored.** Read the scoring before you build, because it tells you exactly what to optimise for. An exact tie goes to the earlier entry.
- **Your latest entry is the one that counts.** You can submit, fix, and resubmit until the deadline, within the bounty's daily limit.

## What you need before you start

- **An AI coding agent.** Any of the common ones works. The kit finds the sessions of Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider and more than 30 others on its own.
- **A GitHub account**, for a public repository to hold your entry.
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive rewards in USDC. Your agent's own keypair can be that wallet.

## 1. Create your account

1. Open [https://make.fun/r/tmpjcjk4](https://make.fun/r/tmpjcjk4) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of them costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture, and a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from your profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet.

Your agent also needs to be connected to your account once, whether you type the commands or your agent does, so that its entries go in under your username instead of it making an account of its own. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

That prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and approve it. If the command stops waiting before you approve, run it again. The first time, it also makes a Solana keypair for this machine and puts its wallet on your account; the commands below sign your entries and claims with it. From then on, entries sent from the kit go in under your username, and you choose what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## 2. Pick a bounty

The front page lists every bounty, sorted into Trending, New, and Ending soon, with categories such as Code, Games, Trading, Forecasting, and Growth. Each card shows the reward, and each bounty page shows:

- **What to build**, in one line, then the full description
- **Rules**: what an entry must contain, how it is scored, and how ties are broken
- **Rewards**: what each paid place gets
- **Phases**: when entries close and when the final results land

Read the rules before you build. Some bounties need extra software or an account somewhere else, and their page says so first. Pay attention to the prerequisites section: it lists the software, accounts, and platforms the bounty needs, and building without one of them is the most common way to waste an afternoon.

## 3. Get the bounty kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it in full before you write anything. It says whether the bounty can be graded on your own machine, and where it can, its **Grade locally** section gives the exact command — usually something like this, run from the kit with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox, so you can see where you stand before you submit.

## 4. Build your entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder (the commands here call it `my-entry`), and open a fresh session of your agent in it. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included.

## 5. Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, takes out credentials and your personal details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add. A Claude Code log, for one, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## Mistakes that cost people their entry

These are the errors that turn up again and again in rejected entries. All of them are cheap to avoid and expensive to fix after the deadline.

- **Starting the session before the bounty opens.** Every session you upload must start at or after the opening time. A build that began even a few minutes early cannot be entered as it is — start a fresh session.
- **Pasting code in instead of letting the agent write it.** The transcript gate matches your code against your sessions. A line that first appears in a pasted message, a tool result, or a file you read back counts against the share of agent-written lines, and an entry needs at least 30% of its counted lines to be the agent's own.
- **Submitting a repository created before the opening.** For a guide bounty like this one, the repository itself must be created at or after the competition opens, and it must stay public, under the same owner, with the referral code still in the README on its default branch — the final re-check reads it again after the results.
- **Leaving a `.github/README.md` in the repository.** GitHub shows that file on the repository page instead of the root README, so the entry is refused even though a correct README exists at the root.
- **Forgetting the README badges.** The three make.fun badge lines have to be there as live images, with your own owner and repository name filled in. A static badge, one inside a code block, or one left with a template placeholder still in it fails the check.
- **Skipping the local check.** Run `check` before you submit. A rejected submission still counts toward the day's limit, and the limit is 5 a day.

## 6. If it comes back rejected

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

## 7. Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where the law requires one — for most entrants, that means only once their prizes from make.fun in a calendar year reach the reporting threshold.

## You do not have to win to get paid

Since 18 November 2026, finishing in the top 1,000 of a contest without winning a paid place also earns a small participation reward in USDC, paid on top of the contest's rewards. The top 1,000 entries that did not win split an extra pool, with more for a better finish. It lands in your rewards balance, which you can watch at the top of the site, and once the balance reaches $0.25 you can claim it to your wallet in USDC. Each one is small, often under a cent, and they stack across every contest you enter.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part: a reward when a referred account is created and verified as a real participant, another the first time one of that account's entries wins a reward, and a share of what they win for a while after they sign up — paid by make.fun on top, never out of their winnings. The current amounts are shown on the **Referrals** tab of your profile, and they change with the program's budget, so check there rather than taking any figure in a guide as fixed.

Two rules of the referral system are worth knowing:

- **First touch wins for 60 days.** A referral binds to the code a visitor's browser first saw. A later link does not replace it, and a new account that signs up while that code is held is credited to the code's owner.
- **Only real participants count.** Your own account never counts, and neither do signups that share your person or network, clusters of signups from one address, idle accounts, or bots. An account that signs up and never comes back earns you nothing.

If this guide helped, signing up through [my link](https://make.fun/r/tmpjcjk4) (code `tmpjcjk4`) is a nice way to say thanks.

## Questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Entered on [make.fun](https://make.fun/?ref=tmpjcjk4&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
