# Awesome Codebase Understanding [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Tools and evidence for understanding a codebase or a code change you didn't write, and deciding faster.

The code works, an agent wrote half of it, and the question is "what happens when a user checks out?" or "is this pull request safe to merge?". This list is sorted by the decision you are making. Every entry says how strong the evidence behind it is, because most tools here publish no numbers on whether they help a person decide, and the few studies that exist measure something narrower than their headlines.

Evidence: 📏 measured, a published measurement with a method · 🔍 open source, you can read how it works · 🏷️ vendor claim · 💬 opinion

<!--lint disable table-pipe-alignment table-cell-padding-->

## Contents

- [Start Here](#start-here)
- [What the Evidence Says](#what-the-evidence-says)
- [How Does This App Fit Together](#how-does-this-app-fit-together)
- [Ask the Codebase](#ask-the-codebase)
- [What Did the Agent Just Change](#what-did-the-agent-just-change)
- [What Breaks If I Change This](#what-breaks-if-i-change-this)
- [Do I Still Understand My Code](#do-i-still-understand-my-code)
- [Research on Human Review](#research-on-human-review)

## Start Here

Three reads if you have one evening.

- [Comprehension debt](https://addyosmani.com/blog/comprehension-debt/) - Addy Osmani. The gap between the code that exists and the code anyone on the team understands, and why review became a throughput problem.
- [I ran 3 Claude Code architecture diagram tools on my repo](https://dev.to/yahhi/i-ran-3-claude-code-architecture-diagram-tools-on-my-repo-heres-what-each-one-got-right-110n) - 2026-11. The only hands-on test found: Floorplan, Archify and Understand Anything on one real app, with three known-answer questions, times and costs. An agent reading the code with no map found a security hole all three maps missed.
- [Four bets on understanding code your AI wrote](https://medium.com/@martin.jordanovski/archify-vs-graphify-vs-understand-anything-vs-codebase-memory-mcp-four-bets-on-understanding-code-88703e8ad3f5) - 2026-11. Sorts the big map tools by who reads the map, a person or the agent, and by who reads the code, a parser or the model.

## What the Evidence Says

- No published study measures whether a code map, a wiki or a guided pull request tour makes a person decide both faster and more correctly. The tools below report setup time, star counts or agent speed, not human outcomes.
- The closest human numbers come from pull request descriptions. AI-written summaries went with reviews 19.3 hours shorter, in an observational study of early adopters. Descriptions that claimed changes the code didn't make were accepted 28.3% of the time against 80.0%.
- Human scrutiny falls without any tool: approval of agent pull requests rose from 30.1% to 36.8% as reviewers gained experience, while inline comments fell by 22%.
- For agents, maps and context files do not reliably raise correctness. Treat a map as a starting point you check, not as an answer.

## How Does This App Fit Together

Maps of a whole codebase: parts, files, requests and outside services.

| | Tool | What it shows you | Limits |
| --- | --- | --- | --- |
| 🔍 🏷️ | [Floorplan](https://github.com/haydenschmitty/floorplan) | A zoomable plain-English map of an app, from parts down to endpoints, with frontend requests matched to backend routes across repos. Highlights what the AI just changed and runs a health check for keys in code and open endpoints. | Made for people who don't read code. No measurement of map accuracy; in one test its user flows were wrong in 2 places until re-traced. |
| 🔍 🏷️ | [Understand Anything](https://github.com/Egonex-AI/Understand-Anything) | A knowledge graph of files, functions and classes with plain-English summaries, a business-domain view, guided tours and diff impact. | No evaluation. The first analysis can cost many tokens: $13 on a 166-file app in one test. |
| 🔍 🏷️ | [Graphify](https://github.com/Graphify-Labs/graphify) | A clickable graph of code, docs and PDFs with a report of the most connected nodes; each edge is marked extracted, inferred or ambiguous. | Marks how sure it is per edge, but publishes no accuracy numbers. |
| 🔍 🏷️ | [Archify](https://github.com/tt-a1i/archify) | One validated interactive diagram of a slice of the system, in 10 types, with links back to the source, plus a before and after view for a change. | General diagramming, not codebase first. Its "measured evidence" means diagram validation, not user outcomes. |
| 🔍 🏷️ | [GitDiagram](https://github.com/ahmedkhaleel2004/gitdiagram) | An interactive architecture diagram of any public GitHub repo and a one-minute explainer video. | No published evaluation. |
| 🔍 🏷️ | [CodeBoarding](https://github.com/CodeBoarding/CodeBoarding) | Interactive architecture diagrams: static analysis finds the relationships, a model names and describes the parts. | No published evaluation. |
| 🔍 🏷️ | [codeflow](https://github.com/braedonsaunders/codeflow) | Paste a GitHub URL and get a map of how files connect and what breaks if you change one. | No published evaluation. |
| 🔍 🏷️ | [GitNexus](https://github.com/abhigyanpatwari/GitNexus) | A browser graph of symbols, calls and execution flows. | Non-commercial licence. |
| 🔍 🏷️ | [Repowise](https://github.com/repowise-dev/repowise) | Architecture and C4 views, ownership, hotspots and dead code from a parsed graph. | AGPL-3.0. Its own comparison posts rank it first. |

## Ask the Codebase

Generated wikis and chat over a repository.

| | Tool | What it shows you | Limits |
| --- | --- | --- | --- |
| 🏷️ | [DeepWiki](https://docs.devin.ai/work-with-devin/deepwiki) | A wiki per repo with diagrams, summaries, source links and questions you can ask. | Its docs say large repos get partial coverage. Maintainers report confident mistakes, such as work-in-progress code described as shipped. |
| 🏷️ | [Google Code Wiki](https://developers.googleblog.com/introducing-code-wiki-accelerating-your-code-understanding/) | A wiki per repo that regenerates as the code changes, with diagrams and chat. | Claims like "understand new libraries in minutes" come with no data. |
| 📏 🔍 | [CodeWiki](https://github.com/FSoft-AI4Code/CodeWiki) | Repo documentation built from the dependency graph, one page per module, in 11 languages. | Scored 82.23 against DeepWiki's 65.06 on its authors' own benchmark, graded by a model against a rubric. Says nothing about whether a reader decides better. |
| 🔍 | [deepwiki-open](https://github.com/AsyncFuncAI/deepwiki-open) | A self-hosted DeepWiki: wiki, diagrams and chat for your own repos. | No published evaluation. |
| 🔍 | [OpenWiki](https://github.com/langchain-ai/openwiki) | A CLI that writes and maintains a Markdown wiki of the repo. | Written for agents first; readable by people. |

## What Did the Agent Just Change

Making one pull request readable: walkthroughs, ordering and provenance.

| | Tool | What it shows you | Limits |
| --- | --- | --- | --- |
| 🏷️ | [CodeRabbit layer-based walkthroughs](https://www.coderabbit.ai/blog/explainable-prs-and-smarter-reviewer-routing) | Reorders a pull request walkthrough into layers, from schema to backend to API to frontend to tests, with a summary per layer. | No numbers on review time or missed bugs. |
| 🏷️ | [Linear Diffs](https://linear.app/docs/diffs) | Shows a pull request next to its issue, core changes first with the reason for each section, tests and generated files hidden. | The risk score is a slot an outside provider fills; Linear doesn't compute it. Guides are on a paid tier. |
| 🏷️ | [Devin Review](https://docs.devin.ai/work-with-devin/devin-review) | An overview of the behaviour change, related edits grouped across files, move detection and a bug catcher. | No accuracy figures for the bug catcher. |
| 🔍 🏷️ | [Plannotator Code Tour](https://docs.plannotator.ai/open-source/workflows/agent-reviews) | A separate agent narrates the open diff with checkpoints; saved guides are flagged when the code moves on. | Its docs say the prompt doesn't enforce read-only and its findings are untrusted evidence. |
| 🏷️ | [GitHub stacked pull requests](https://github.blog/engineering/turn-one-giant-ai-generated-pull-request-to-a-reviewable-stack/) | Splits one large agent pull request into a stack of single-purpose ones, read top down and reviewed bottom up. | A worked example, no measurement that stacks speed up or improve review. |
| 🔍 🏷️ | [accountable-review](https://github.com/wyeworks/accountable-review) | A Claude Code plugin that turns a pull request into a published HTML review map. | Young project, no evaluation. |
| 🔍 | [hunk](https://github.com/modem-dev/hunk) | A terminal diff viewer built for reviewing agent-written changes. | A viewer; it does not explain the change. |
| 🔍 | [tuicr](https://github.com/agavra/tuicr) | A terminal code reviewer that tracks which hunks you have actually seen. | Keyboard-first, terminal only. |
| 🔍 💬 | [Showboat](https://github.com/simonw/showboat) | The agent writes a demo document of commands it ran and their output, which `verify` can re-run. | Its author notes agents cheat by editing the document instead of running commands. |
| 🔍 | [Agent Trace](https://agent-trace.dev) | An open spec for recording which lines came from which model and conversation. | A data format, not a view. Quality assessment is an explicit non-goal. |

## What Breaks If I Change This

Impact of a change before you make it.

| | Tool | What it shows you | Limits |
| --- | --- | --- | --- |
| 🔍 🏷️ | [code-review-graph](https://github.com/tirth8205/code-review-graph) | The blast radius, affected tests and risk-scored review context for a change. | Built as context for AI tools first. |
| 🔍 🏷️ | [codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp) | The symbols a diff touches, with risk, and a browser view in beta. | Agent-first. |
| 🔍 | [sem](https://github.com/Ataraxy-Labs/sem) | Diffs, blame and impact at the level of functions and classes instead of lines, on top of git. | No published evaluation. |
| 📏 🔍 | [CodeGraph](https://github.com/colbymchenry/codegraph) | A symbol and call graph with blast-radius queries. | Its numbers are for the agent: 53% faster and 88% fewer tool calls on its authors' runs, but about 80% more retrieved context left in the window. Nothing about a person's decision. |

## Do I Still Understand My Code

Tools and research on keeping your own understanding.

- 🔍 [rederive](https://github.com/EricJujianZou/rederive) - A Claude Code skill that asks how you would explain code the AI wrote for you, before someone else asks.
- 🔍 [understanding-map](https://github.com/amit429/understanding-map) - A Claude Code plugin that finds the code nobody on the team understands any more.
- 🔍 [mindwalk](https://github.com/cosmtrek/mindwalk) - Replays a coding-agent session on a 3D map of the codebase, so you can see where it went.
- 📏 [How AI Impacts Skill Formation](https://arxiv.org/abs/2601.20245) - 2026. In a randomized trial with 52 engineers, those using AI took the same time but scored 17% lower on a comprehension quiz, 50% against 67%. About learning with AI, not about maps.
- 💬 [Cognitive Debt in the GenAI Era](https://arxiv.org/abs/2610.37888) - 2026. A review of 76 practitioner sources on lost understanding, with suggested practices such as design rationale notes and review-sized changes. No effect sizes.

## Research on Human Review

| | When | Study | Finding | Limits |
| --- | --- | --- | --- | --- |
| 📏 | 2026 | [Habituation at the Gate](https://arxiv.org/abs/2606.22721) | Across 11,429 reviews by 400 repeat reviewers, approval of agent pull requests rose from 30.1% to 36.8%, inline comments fell 22% and change requests halved. | Observational. Can't separate habituation from agents getting better. |
| 📏 | 2026 | [Message-code inconsistency in agent pull requests](https://arxiv.org/abs/2601.04886) | 1.7% of 23,247 agent pull requests had descriptions that didn't match the code. Those were accepted 28.3% of the time against 80.0%, and took 3.5 times longer to merge. | Shows a wrong summary costs time, not that a good one saves it. |
| 📏 | 2024 | [Generative AI for Pull Request Descriptions](https://dl.acm.org/doi/10.1145/3643773) | Pull requests with Copilot-written descriptions were reviewed 19.3 hours faster and were 1.57 times likelier to merge. | Observational, early adopters. Merge is not correctness. |
| 📏 | 2026 | [How AI Coding Agents Communicate](https://arxiv.org/abs/2602.17084) | More structured agent pull request descriptions went with faster responses and completion. | The authors say simpler changes may explain it. |
| 📏 | 2026 | [Trust-Calibrated Code Review](https://arxiv.org/abs/2606.01969) | A three-level review flow from overview to file to snippet. 63% of 43 surveyed developers expected less review effort. | Expectations of a prototype, not measured use. |
| 📏 | 2026 | [Human oversight of agentic systems in practice](https://arxiv.org/abs/2606.05391) | Interviews with 17 practitioners describe four ways people oversee agents, from up-front control to review after the fact. | Qualitative, no outcome numbers. |

## Related Lists

- [awesome-code-review](https://github.com/joho/awesome-code-review) - Articles, papers and tools on code review in general.
- [awesome-claude-code](https://github.com/jqueryscript/awesome-claude-code) - Plugins and tools for Claude Code, including several map tools.
- [Awesome Agents in Production](https://github.com/redikultsev/awesome-agents-in-production) - Incidents where agents in production broke, and the controls that would have held.
