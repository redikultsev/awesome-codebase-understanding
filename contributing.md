# Contribution Guidelines

Thanks for helping. This list is useful only if a reader can tell how much to trust each entry, so every line has to say what it shows and where its evidence stops.

## What fits

- A **tool** that helps a person understand a codebase or a code change: maps, wikis, pull request walkthroughs, impact analysis, provenance.
- A **study or test** that measures how people understand code or review changes, especially code written by AI.
- Not in scope: tools that only feed context to an agent and show nothing to a person, general AI coding assistants, and pages that sell a product without saying how it works.

## How to add an entry

- Link the primary source: the repository, the official docs, the paper. Not a reseller page or a roundup.
- Format: `- 🟡 [Name](link) - Open source. What it shows you. *Limits: what its evidence doesn't cover.*`
- One mark, the strongest the evidence supports: 🟢 a published measurement with a method (say on whom: people or agents), 🟡 the maker's claim with no numbers, ⚪ an argument or experience report, no mark if the entry claims nothing. Write "Open source." in the text instead of a mark.
- Always add *Limits:* unless the entry claims nothing. Name the strongest claim that has no data behind it, or what the measurement doesn't cover.
- One or two plain sentences, ending with a period. Numbers only if they are in the source.
- Put the entry under the decision someone would be making, in the bold sub-group where it fits.
- One pull request per entry, with a title like `Add [Name]`.

## Before you open the pull request

- Run `npx awesome-lint` and fix what it reports.
- Check that the link opens and that the source says what your line says.

If you're not sure whether something fits, open an issue first.
