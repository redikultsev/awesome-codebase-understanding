# Awesome Codebase Understanding [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Understanding code you didn't write, and how much the tools for it are proven to help.

![42 entries](https://img.shields.io/badge/entries-42-0969da?style=flat-square) ![10 measured](https://img.shields.io/badge/measured-10-2da44e?style=flat-square) ![Every entry has an evidence mark](https://img.shields.io/badge/evidence-every%20entry-8250df?style=flat-square) ![Updated November 2026](https://img.shields.io/badge/updated-November%202026-6e7781?style=flat-square)

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/hero-dark.svg">
  <img alt="Six questions. Almost nothing here was measured on people. How does this app fit together: 9 tools, 0 measured on people. Ask the codebase: 5 tools, 0 on people, 1 graded by a model. What did the agent just change: 10 tools, 0 measured on people. What breaks if I change this: 4 tools, 0 on people, 1 on agents. Do I still understand my code: 5 entries, 1 trial on people, about learning. Studies of human review: 6 studies, 0 controlled tests of a tool." src="assets/hero-light.svg">
</picture>

An agent wrote half of the code, and now you have to answer "what happens when a user checks out?" or "is this pull request safe to merge?". This list is sorted by that question. Every entry says what its claim rests on, because most tools here publish no numbers on whether they help a person decide.

<!--lint disable table-pipe-alignment table-cell-padding-->

## Contents

- [Legend](#legend)
- [Start Here](#start-here)
- [What the Evidence Says](#what-the-evidence-says) - You want the numbers, not the tools.
- [How Does This App Fit Together](#how-does-this-app-fit-together) - You inherited a codebase and need the big picture.
- [Ask the Codebase](#ask-the-codebase) - You have a question and no one to ask.
- [What Did the Agent Just Change](#what-did-the-agent-just-change) - An agent opened a pull request.
- [What Breaks If I Change This](#what-breaks-if-i-change-this) - You are about to edit something shared.
- [Do I Still Understand My Code](#do-i-still-understand-my-code) - You merge code you could not explain.
- [Research on Human Review](#research-on-human-review) - What is measured about people reviewing AI-written code.

## Legend

One mark per entry, from strongest to weakest: the strongest thing its claim to help rests on.

| Mark | Meaning |
| --- | --- |
| 🟢 | Measured. A published measurement with a method. The entry says on whom: people or agents. |
| 🟡 | Vendor claim. The maker says it helps and publishes no numbers. |
| ⚪ | Opinion. An argument, a worked example or an experience report. |
| no mark | The entry makes no claim to help. It only does something you can check yourself. |

Open source is noted in the text, not as a mark. Being able to read the code is not evidence that it helps you decide.

## Start Here

Three reads if you have one evening.

- ⚪ [Comprehension debt](https://addyosmani.com/blog/comprehension-debt/) - Addy Osmani. The gap between the code that exists and the code anyone on the team understands, and why review became a throughput problem.
- 🟢 [I ran 3 Claude Code architecture diagram tools on my repo](https://dev.to/yahhi/i-ran-3-claude-code-architecture-diagram-tools-on-my-repo-heres-what-each-one-got-right-110n) - 2026-11. Floorplan, Archify and Understand Anything on one real app, with three known-answer questions, times and costs. An agent reading the code with no map found a security hole all three maps missed. *Limits: one app, one author.*
- ⚪ [Four bets on understanding code your AI wrote](https://medium.com/@martin.jordanovski/archify-vs-graphify-vs-understand-anything-vs-codebase-memory-mcp-four-bets-on-understanding-code-88703e8ad3f5) - 2026-11. Sorts the big map tools by who reads the map, a person or the agent, and by who reads the code, a parser or the model.

## What the Evidence Says

**Nothing measures the main claim.** No published study checks whether a code map, a wiki or a guided pull request tour makes a person decide both faster and more correctly.

**The closest numbers are about pull request descriptions.** AI-written summaries went with reviews 19.3 hours shorter. Descriptions that claimed changes the code didn't make were accepted 28.3% of the time, against 80.0%.

**Scrutiny falls on its own.** As reviewers gained experience, approval of agent pull requests rose from 30.1% to 36.8% and inline comments fell by 22%.

**Maps don't make agents more correct either.** Treat a map as a place to start checking, not as the answer.

## How Does This App Fit Together

Maps of a whole codebase: parts, files, requests and outside services. None of them has been measured on people.

| Tool | Reads the code with | Shows a change | Licence |
| --- | --- | --- | --- |
| Floorplan | model | yes | MIT |
| Understand Anything | model | yes | MIT |
| Graphify | parser | ? | Apache-2.0 |
| Archify | model | yes | Apache-2.0 |
| CodeBoarding | parser and model | ? | MIT |
| Repowise | parser | ? | AGPL-3.0 |

`?` means the project doesn't say.

**For people who don't read code.**

- 🟡 [Floorplan](https://github.com/haydenschmitty/floorplan) - Open source. A zoomable plain-English map of an app, from parts down to endpoints, with frontend requests matched to backend routes across repos. Highlights what the AI just changed and checks for keys in code and open endpoints. *Limits: no measurement of map accuracy; in one test its user flows were wrong in 2 places until re-traced.*
- 🟡 [Understand Anything](https://github.com/Egonex-AI/Understand-Anything) - Open source. A knowledge graph of files, functions and classes with plain-English summaries, a business-domain view, guided tours and diff impact. *Limits: no evaluation; the first analysis cost $13 on a 166-file app in one test.*

**For people who read code.**

- 🟡 [Graphify](https://github.com/Graphify-Labs/graphify) - Open source. A clickable graph of code, docs and PDFs, with a report of the most connected nodes. Code is parsed locally without a model, and each edge is marked extracted, inferred or ambiguous. *Limits: marks how sure it is per edge, but publishes no accuracy numbers.*
- 🟡 [Archify](https://github.com/tt-a1i/archify) - Open source. One validated interactive diagram of a slice of the system, in 10 types, with links back to the source and a before and after view for a change. *Limits: general diagramming, not codebase first; its "measured evidence" means diagram validation, not user outcomes.*
- 🟡 [CodeBoarding](https://github.com/CodeBoarding/CodeBoarding) - Open source. Interactive architecture diagrams: static analysis finds the relationships, a model names and describes the parts. *Limits: no published evaluation.*

<details>
<summary><b>More map tools (4)</b></summary>

- 🟡 [GitDiagram](https://github.com/ahmedkhaleel2004/gitdiagram) - Open source. An interactive architecture diagram of any public GitHub repo and a one-minute explainer video. *Limits: no published evaluation.*
- 🟡 [codeflow](https://github.com/braedonsaunders/codeflow) - Open source. Paste a GitHub URL and get a map of how files connect and what breaks if you change one. *Limits: no published evaluation.*
- 🟡 [GitNexus](https://github.com/abhigyanpatwari/GitNexus) - Source available. A browser graph of symbols, calls and execution flows. *Limits: PolyForm Noncommercial licence.*
- 🟡 [Repowise](https://github.com/repowise-dev/repowise) - Open source. Architecture and C4 views, ownership, hotspots and dead code from a parsed graph. *Limits: its own comparison posts rank it first.*

</details>

## Ask the Codebase

Generated wikis and chat over a repository. The one benchmark here grades documents with a model, not readers.

- 🟡 [DeepWiki](https://docs.devin.ai/work-with-devin/deepwiki) - A wiki per repo with diagrams, summaries, source links and questions you can ask. *Limits: its docs say large repos get partial coverage; maintainers report confident mistakes, such as work-in-progress code described as shipped.*
- 🟡 [Google Code Wiki](https://developers.googleblog.com/introducing-code-wiki-accelerating-your-code-understanding/) - A wiki per repo that regenerates as the code changes, with diagrams and chat. *Limits: claims like "understand new libraries in minutes" come with no data.*
- 🟢 [CodeWiki](https://github.com/FSoft-AI4Code/CodeWiki) - Open source. Repo documentation built from the dependency graph, one page per module, in 11 languages. Measured on documents: 82.23 against DeepWiki's 65.06 on its authors' benchmark. *Limits: graded by a model against a rubric; says nothing about whether a reader decides better.*
- [deepwiki-open](https://github.com/AsyncFuncAI/deepwiki-open) - Open source. A self-hosted DeepWiki: wiki, diagrams and chat for your own repos.
- [OpenWiki](https://github.com/langchain-ai/openwiki) - Open source. A CLI that writes and maintains a Markdown wiki of the repo, written for agents first and readable by people.

## What Did the Agent Just Change

A pull request landed, mostly written by an agent, and you have to decide whether to merge it. None of these tools publishes a number on review time or missed bugs. The only human numbers are about pull request descriptions, in Research on Human Review below.

**Read it in a sensible order.**

- 🟡 [Linear Diffs](https://linear.app/docs/diffs) - Shows a pull request next to its issue, core changes first with the reason for each section, tests and generated files hidden. *Limits: the risk score is a slot an outside provider fills; guides are on a paid tier.*
- 🟡 [CodeRabbit layer-based walkthroughs](https://www.coderabbit.ai/blog/explainable-prs-and-smarter-reviewer-routing) - Reorders the walkthrough into layers, from schema to backend to API to frontend to tests, with a summary per layer. *Limits: no numbers on review time or missed bugs.*
- 🟡 [Devin Review](https://docs.devin.ai/work-with-devin/devin-review) - An overview of the behaviour change, related edits grouped across files, move detection and a bug catcher. *Limits: no accuracy figures for the bug catcher.*
- 🟡 [Plannotator Code Tour](https://docs.plannotator.ai/open-source/workflows/agent-reviews) - Open source. A separate agent narrates the open diff with checkpoints, and saved guides are flagged when the code moves on. *Limits: its docs say the prompt doesn't enforce read-only and its findings are untrusted evidence.*
- ⚪ [GitHub stacked pull requests](https://github.blog/engineering/turn-one-giant-ai-generated-pull-request-to-a-reviewable-stack/) - Splits one large agent pull request into single-purpose ones, read top down and reviewed bottom up. *Limits: a worked example, not a measurement.*

**Read the diff yourself.**

- [hunk](https://github.com/modem-dev/hunk) - Open source. A terminal diff viewer built for reviewing agent-written changes.
- [tuicr](https://github.com/agavra/tuicr) - Open source. A terminal code reviewer that tracks which hunks you have actually seen.

**Check what the agent says it did.**

- ⚪ [Showboat](https://github.com/simonw/showboat) - Open source. The agent writes a demo document of the commands it ran and their output, and `verify` re-runs them. *Limits: its author notes agents edit the document instead of running commands.*
- [Agent Trace](https://agent-trace.dev) - An open spec for recording which lines came from which model and conversation. *Limits: a data format, not a view; quality assessment is an explicit non-goal.*
- 🟡 [accountable-review](https://github.com/wyeworks/accountable-review) - Open source. A Claude Code plugin that turns a pull request into a published HTML review map. *Limits: young project, no evaluation.*

## What Breaks If I Change This

The impact of a change before you make it. The one number here was measured on agents, not on people.

- 🟡 [code-review-graph](https://github.com/tirth8205/code-review-graph) - Open source. The blast radius, affected tests and risk-scored review context for a change. *Limits: built as context for AI tools first.*
- 🟡 [codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp) - Open source. The symbols a diff touches, with risk, and a browser view in beta. *Limits: agent-first.*
- [sem](https://github.com/Ataraxy-Labs/sem) - Open source. Diffs, blame and impact at the level of functions and classes instead of lines, on top of git.
- 🟢 [CodeGraph](https://github.com/colbymchenry/codegraph) - Open source. A symbol and call graph with blast-radius queries. Measured on agents: 53% faster and 88% fewer tool calls on its authors' runs. *Limits: about 80% more retrieved context left in the window; nothing about a person's decision.*

## Do I Still Understand My Code

Keeping your own understanding while an agent writes the code.

- [rederive](https://github.com/EricJujianZou/rederive) - Open source. A Claude Code skill that asks how you would explain code the AI wrote for you, before someone else asks.
- [understanding-map](https://github.com/amit429/understanding-map) - Open source. A Claude Code plugin that finds the code nobody on the team understands any more.
- [mindwalk](https://github.com/cosmtrek/mindwalk) - Open source. Replays a coding-agent session on a 3D map of the codebase, so you can see where it went.
- 🟢 [How AI Impacts Skill Formation](https://arxiv.org/abs/2601.20245) - 2026. Measured on people: in a randomized trial with 52 engineers, those using AI took the same time but scored 17% lower on a comprehension quiz, 50% against 67%. *Limits: about learning with AI, not about maps.*
- ⚪ [Cognitive Debt in the GenAI Era](https://arxiv.org/abs/2610.37888) - 2026. A review of 76 practitioner sources on lost understanding, with suggested practices such as design rationale notes and review-sized changes. *Limits: no effect sizes.*

## Research on Human Review

What is measured about people reviewing AI-written changes. All of it is observational, a survey or interviews: none is a controlled test of a tool.

- 🟢 [Habituation at the Gate](https://arxiv.org/abs/2606.22721) - 2026. Across 11,429 reviews by 400 repeat reviewers, approval of agent pull requests rose from 30.1% to 36.8%, inline comments fell 22% and change requests halved. *Limits: can't separate habituation from agents getting better.*
- 🟢 [Analyzing Message-Code Inconsistency in AI Coding Agent-Authored Pull Requests](https://arxiv.org/abs/2601.04886) - 2026. 1.7% of 23,247 agent pull requests had descriptions that didn't match the code. Those were accepted 28.3% of the time against 80.0% and took 3.5 times longer to merge. *Limits: shows a wrong summary costs time, not that a good one saves it.*
- 🟢 [Generative AI for Pull Request Descriptions](https://dl.acm.org/doi/10.1145/3643773) - 2024. Pull requests with Copilot-written descriptions were reviewed 19.3 hours faster and were 1.57 times likelier to merge. *Limits: early adopters; merging is not correctness.*
- 🟢 [How AI Coding Agents Communicate](https://arxiv.org/abs/2602.17084) - 2026. More structured agent pull request descriptions went with faster responses and completion. *Limits: the authors say simpler changes may explain it.*
- 🟢 [Trust-Calibrated Code Review](https://arxiv.org/abs/2606.01969) - 2026. A three-level review flow from overview to file to snippet; 63% of 43 surveyed developers expected less review effort. *Limits: expectations of a prototype, not measured use.*
- 🟢 [Human oversight of agentic systems in practice](https://arxiv.org/abs/2606.05391) - 2026. Interviews with 17 practitioners describe four ways people oversee agents, from up-front control to review after the fact. *Limits: qualitative, no outcome numbers.*

---

**How entries get in.** A tool helps a person understand a codebase or a change, links to its primary source, and gets the strongest mark its own evidence supports. A study measures how people understand or review code. Every entry names what its evidence doesn't cover.

**What this list doesn't do.** It doesn't test the tools. A mark says what the maker or the authors have shown, not that the tool works on your code.

**Related lists.** [awesome-code-review](https://github.com/joho/awesome-code-review) for code review in general, [awesome-claude-code](https://github.com/jqueryscript/awesome-claude-code) for Claude Code plugins, [Awesome Agents in Production](https://github.com/redikultsev/awesome-agents-in-production) for what breaks when agents run in production.

Contributions welcome: read the [contribution guidelines](contributing.md) first. Licensed [CC BY 4.0](LICENSE).
