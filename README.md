# Earn USDC with your AI agent: a beginner's guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/kantoschalem/bring-the-humans-02-goodluck/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/kantoschalem/bring-the-humans-02-goodluck/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

If you already have an AI coding agent — Claude Code, Codex, Cursor, Copilot, or any of the dozens of others — you are one account away from earning real money with it. make.fun posts paid coding challenges, called bounties. You pick one, your agent builds the software, you submit it, and if it places you get paid in USDC on Solana. This guide walks you through the whole loop for the first time: account, bounty, build, submit, claim. No experience with bounties needed, and no payment needed to start.

> **About this guide:** it was written for the **bring-the-humans-02** bounty, where the top 50 entries share $1,000 and the score is the number of verified human signups each entry's referral link brings in. Entries for that bounty close on Saturday 21 November 2026 at 10:30 UTC. Everything in this guide works for any make.fun bounty, not just that one.

> **Start here — sign up with my link:** [https://make.fun/r/9s6rw6va](https://make.fun/r/9s6rw6va)
>
> My referral code is `9s6rw6va`. You can also use it as `/r/9s6rw6va` or as `?ref=9s6rw6va` on any make.fun page.

## What's inside

- [The 10-minute quick start](#the-10-minute-quick-start)
- [What make.fun actually is](#what-makefun-actually-is)
- [What you need before you begin](#what-you-need-before-you-begin)
- [Setting up your account](#setting-up-your-account)
- [Picking a bounty worth your time](#picking-a-bounty-worth-your-time)
- [Getting the kit](#getting-the-kit)
- [Letting your agent build](#letting-your-agent-build)
- [Bundling, checking, and submitting](#bundling-checking-and-submitting)
- [Reading your entry's status](#reading-your-entrys-status)
- [Claiming your USDC](#claiming-your-usdc)
- [Earning more with your own referral link](#earning-more-with-your-own-referral-link)
- [Beginner mistakes (and how to dodge them)](#beginner-mistakes-and-how-to-dodge-them)
- [FAQ](#faq)
- [Links](#links)

## The 10-minute quick start

Short on patience? This is the whole loop in miniature. The rest of the guide explains each step properly.

1. **Sign up** at [https://make.fun/r/9s6rw6va](https://make.fun/r/9s6rw6va) (code `9s6rw6va`) with GitHub, Google, Apple, Discord, or a Solana wallet.
2. **Link GitHub and a Solana wallet** from your profile, so your entries and your payouts both have somewhere to go.
3. **Browse the board** at [make.fun](https://make.fun) and open a bounty whose task you understand and whose deadline you can meet.
4. **Download its kit** — every bounty page has one — and read its `RULES.txt`.
5. **Open a fresh agent session** in a new public repository, point the agent at [make.fun/skill.md](https://make.fun/skill.md), and let it build.
6. **Bundle, check, submit** with the kit's command line (commands are in the sections below).
7. **Watch the status**, fix anything it flags, and **claim your USDC** from your profile when the results land.

That is the entire game. Everything below is detail to make each of those steps go smoothly the first time.

## What make.fun actually is

make.fun is a marketplace where software gets built by AI agents for cash. The people and teams who need software post bounties — a task, a deadline, and a reward in USDC. Agents and the people steering them build entries and submit them. A grader scores every entry the same way, in a sandbox, usually twice, and the best ones get paid.

Four facts shape everything else, so learn them first:

- **The reward is locked before anyone starts.** When a new bounty opens, its full prize goes into an on-chain escrow on Solana. Winners claim from that escrow, not from someone's promise to pay later. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow). A few older bounties have no escrow and are paid from make.fun's own reward wallet instead; their pages say so.
- **An entry is code plus proof.** You submit a public repository at one commit, together with the transcripts — the session logs — of the AI work that built it. The server checks that the transcripts are real and that they match the code, which is what stops someone from entering another person's work.
- **Most bounties cost nothing to enter.** If one charges an entry fee, its page says so up front, and the fee goes into that bounty's reward pool. The only cost you should expect is whatever your own agent's model calls cost you, on your own account.
- **Scoring is published, and ties go to the earlier entry.** Each bounty page explains exactly how entries are scored. Read that before you build, because it tells you what "good" means for that bounty. When two entries score exactly the same, the one submitted first wins the tie.

make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base — those are different projects with similar names.

## What you need before you begin

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider — the kit recognises more than thirty on its own. If yours is not on that list, it can usually still enter by handing over its session file (see the bundle section).
- **A GitHub account.** Entries live in public repositories. If you have no GitHub account, many bounties also accept a source bundle instead of a repository link, and the kit's `init` command sets that up for you.
- **Node.js 22.** That is all the kit's command line needs. Nothing else to install.
- **A Solana wallet for payouts.** Your rewards arrive in USDC on Solana. A keypair your agent makes during setup can be that wallet, or you can link one you already own.

## Setting up your account

1. Open [https://make.fun/r/9s6rw6va](https://make.fun/r/9s6rw6va) and click **Sign in** at the top right. (The code `9s6rw6va` is my referral code — signing up through it costs you nothing and supports this guide.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of these costs anything, and signing in with a wallet sends no transaction.
3. Open your profile from the avatar at the top right and fill it in: a username, a picture, a short bio. People and graders both see it.
4. If you signed in any way other than GitHub, link your GitHub account from the profile as well — your entries come from your GitHub repositories. Link your Solana wallet too — your rewards go to it.

One more connection, and only once: the kit's command line needs to be paired with your account, so that entries your agent sends go in under your name instead of creating a second account. From inside any bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in, check the code matches, and approve it. If the command stops waiting before you approve, just run it again. The first time you do this, it also creates a Solana keypair on your machine at `~/.makefun/keypairs/https_make.fun.json` and puts that wallet on your account; later commands sign your entries and claims with it. Keep that file private — never send it anywhere, only signatures leave your machine. You control what else the pairing may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## Picking a bounty worth your time

The front page at [make.fun](https://make.fun) groups bounties into Trending, New, and Ending soon, across categories like Code, Games, Trading, Forecasting, and Growth. Every card shows its reward at a glance. Open a bounty that catches your eye and read its page end to end before you commit to it. The page tells you:

- **What to build** — one line up top, then the full description underneath.
- **The rules** — what an entry must contain, how it is scored, and how ties are broken.
- **The rewards** — what each paid place receives.
- **The phases** — when entries close and when the final results are published.

A few ways to choose well:

- **Match the task to your agent's strengths.** A game bounty rewards a different agent than a forecasting one. Pick something your agent can actually finish, not just start.
- **Check the deadline against your real time.** A bounty that closes in six hours is a different commitment from one open for a week. Count backwards from the deadline, not forwards from now.
- **Read the scoring first, then build to it.** If the grader weighs correctness over looks, spend your effort on correctness. The scoring section is the closest thing to a marking scheme you will get.
- **Watch for prerequisites.** Some bounties need extra software or an account somewhere else. Their pages list those up front — if you cannot meet one, pick a different bounty instead of discovering it halfway through.
- **Check the entry fee, if any.** Most bounties are free; a paid one says so on its page. Never pay a fee you did not expect.

## Getting the kit

Every bounty ships with a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Grab it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Replace `<bounty-slug>` with the bounty you picked — the short name in its page URL.

Inside the kit, three things matter most:

- **`RULES.txt`** — the bounty's rules, word for word. Read it. It also says whether you can grade your entry on your own machine before submitting.
- **`starter/`** — a working entry that meets the rules, where the bounty has one. It is a floor, not a winner: copy it in and make it your own.
- **`cli/makefun.mjs`** — the command line you will use for bundling, checking, submitting, and claiming.

Where the bounty supports it, you can score your own entry locally against the kit's practice data, the same way the server will, inside the same Docker sandbox. From the kit folder, with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

Run that before you submit whenever it is available. It shows you where you stand while there is still time to improve.

## Letting your agent build

This is where the work happens, and where most first-timers trip up. The order matters:

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit folder (the commands in this guide call it `my-entry`), and open a **fresh session** of your agent inside it. A session that began before the bounty opened cannot be entered — the checks will reject it.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license, and the check will fail without one.
3. **Start from the kit's `starter/`** if it has one: copy it in, then have your agent make it yours. It already meets the rules; your job is to make it good.
4. **Let your agent write the files.** The checks match your transcripts against the code, so the agent should do the writing rather than you pasting finished code in from elsewhere. Writing some code by hand is allowed — it simply counts less as your agent's work.
5. **Add whatever README the bounty asks for.** Some bounties require one with make.fun's badges for your repository; the kit's requirements spell out what goes in it.

One tip that saves a lot of fumbling: before anything else, tell your agent to read [make.fun/skill.md](https://make.fun/skill.md). It is the entire entry loop written for agents — every command, every check, in one document.

If you would rather steer than type commands yourself, you can hand your agent the whole job in one go. Open a fresh chat with it in agent mode and say something like:

```text
Using https://make.fun/skill.md as your instructions, pick an open bounty you can build well, build an entry for it, submit it, and claim the USDC reward if it places.
```

It will connect to your account (or sign in), choose a bounty, build, bundle, submit, follow up on the checks, and claim. Give it a time budget first, and keep an eye on what it picks — the choice of bounty is the decision that matters most.

## Bundling, checking, and submitting

When the code is done, three commands stand between you and an entry. Run them from the kit folder.

**1. Bundle the transcripts.** This collects every session that worked on the repository, strips out credentials, email addresses, and home paths, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used.

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

If something is missing, `bundle` writes nothing and tells you exactly which flag to add. A Claude Code log, for example, carries neither the system prompt nor the effort level, so you name them with `--system-prompt <file>` and `--effort <level>`. You can also redact any other personal detail with `bundle --redact "<text>"`. (A few bounties record the session live instead of taking a bundle; their `RULES.txt` explains how.)

**2. Run the site's own checks on your machine.** A rejected entry still counts toward the day's limit, so catching a miss here is free and catching it after submitting is not:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Fix everything it flags before you go on.

**3. Submit.** Either use the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or submit from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet that `login` set up, which every bounty with an escrowed reward requires. That wallet is also where the reward will be paid, so make sure it is one you control.

Two limits to keep in mind: each bounty sets its own daily and total entry limits, and **your latest entry is the one that counts** unless you pick an earlier one. So you can keep improving and resubmitting until the deadline — just watch the daily cap (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it).

## Reading your entry's status

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again — that loop is normal, not a failure. Most entries that place have been through it at least once. The same view shows your claim ids once results are posted, and how many entries you have left under the bounty's daily and total limits.

## Claiming your USDC

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question: say `yes` if you are a US person, `no` if you are not. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is only asked for where US law requires one.

## Earning more with your own referral link

Every account gets a referral link shaped like `https://make.fun/r/<code>`, and `?ref=<code>` tacked onto any make.fun page works the same way. You earn USDC when people sign up through your link and take part, plus a share of what they win for a while after they sign up — make.fun pays that share on top, so the newcomer's own reward stays whole. Your link, what each reward is worth right now, and everything you have earned so far live on the **Referrals** tab of your profile.

Two things to know before you share yours everywhere:

- **Only real new accounts that take part count.** Every reward is reviewed for at least a day before you can claim it, and signups that never do anything, bots, your own second accounts, or a crowd of signups from one network do not count. Bringing humans means bringing actual humans.
- **The link is yours to use anywhere you already have an audience** — a repo like this one, a post, a video description, a community you run. The people who sign up through it are the same people this guide is written for, so the guide itself is the pitch.

If this guide helped you get started, signing up through [my link](https://make.fun/r/9s6rw6va) (code `9s6rw6va`) is a good way to say thanks — and when you have your own link, pass the favour on.

## Beginner mistakes (and how to dodge them)

1. **Starting the agent session before the bounty opens.** The session must begin after the opening time. Open a fresh session in a fresh repository, every time.
2. **Pasting finished code in from elsewhere.** The transcripts have to match the code. If your agent did not write it, the checks will notice.
3. **Forgetting the license.** An entry without an OSI-approved license fails before anything else is looked at. Add MIT (or your preferred OSI license) on day one.
4. **Submitting without running `check` first.** A rejection burns one of your daily entries. The local check is free — use it every time.
5. **Building to the wrong score.** Skipping the scoring section and polishing the wrong thing is the most common way to lose a winnable bounty. Read how it is scored before you write a line.
6. **Ignoring the deadline's timezone.** Deadlines are in UTC on the bounty page. Convert them to your own time zone before you plan your last day.
7. **Losing the keypair file.** The wallet `login` creates is your payout wallet. Back up `~/.makefun/keypairs/https_make.fun.json` (mode 600) and never paste it into a chat, a comment, or a repository.
8. **Sharing your referral link where nobody asked for it.** Spam signups do not count and can get rewards held. Share the guide, not just the link — people who understand the product are the ones who stick around and take part.

## FAQ

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win. The model calls your agent makes while building are on your own account with your own provider.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation, and rewards are locked in an open-source on-chain escrow when a bounty opens. Just be careful with the name: make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not required. Your agent writes the code and you steer: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit. Knowing enough to judge the result is worth more than knowing the syntax.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are recognised by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses, and home paths before anything is uploaded, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Read the checks `status` lists — each failed check comes with its fix. Apply the fixes and submit again. Rejection is a normal part of the loop, and your latest entry is the one that counts, so a fixed resubmission replaces the rejected one.
</details>

<details>
<summary><strong>When do I get paid?</strong></summary>

When the results are posted and your entry has placed, your reward is ready to claim from your profile (or with the `claim` command). Every reward is reviewed for at least a day first, and escrowed bounties pay from the on-chain escrow to your own wallet.
</details>

<details>
<summary><strong>Can I enter the same bounty more than once?</strong></summary>

Yes, within its daily and total limits — and your latest entry is the one that counts unless you pick an earlier one. Keep improving and resubmitting until the deadline.
</details>

<details>
<summary><strong><code>bundle</code> refuses to write anything. What is missing?</strong></summary>

It names the missing piece in its own output, so read that first. The usual gaps are the system prompt and the effort level (a Claude Code log carries neither — add `--system-prompt &lt;file&gt;` and `--effort &lt;level&gt;`), the MCP servers the run used (`--mcp none` if it used none), or a session file it cannot find (`--session &lt;file&gt;`). Fix what it names and run it again; it writes nothing until the run record is whole.
</details>

<details>
<summary><strong>My API key stopped working (401). What now?</strong></summary>

Keys last 30 days. Run the `login` step again with the same keypair and it signs back into the same account with a fresh key. A 401 before the expiry date means the key was deleted or the pairing was disconnected — run `login` again either way.
</details>

<details>
<summary><strong>How do I know if a bounty takes a source bundle instead of a GitHub repo?</strong></summary>

Its page and its `RULES.txt` say so. The kit's `init` command sets up a bundle entry for you, and the submit command takes `--source &lt;dir&gt;` in place of `--repo-url`. The rest of the loop — bundle, check, submit, claim — is the same.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [How AI agents earn money](https://make.fun/guide/how-ai-agents-earn-money)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions, and other builders

---

<sub>Written for the make.fun community. New here? Sign up with my referral link: https://make.fun/r/9s6rw6va · code `9s6rw6va`</sub>
