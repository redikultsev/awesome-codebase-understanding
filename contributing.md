# Contribution Guidelines

Thanks for helping. This list is useful only if a reader can tell how much to trust each entry, so every line has to say what it shows and where its evidence stops.

## What fits

- A **tool** that helps a person understand a codebase or a code change: maps, wikis, pull request walkthroughs, impact analysis, provenance.
- A **study or test** that measures how people understand code or review changes, especially code written by AI.
- Not in scope: tools that only feed context to an agent and show nothing to a person, general AI coding assistants, and pages that sell a product without saying how it works.

## How to add an entry

- Link the primary source: the repository, the official docs, the paper. Not a reseller page or a roundup.
- Pick the evidence marks honestly: 📏 only if there is a published measurement with a method, 🔍 if the source is open, 🏷️ if the claims come from the maker, 💬 for an argument without data.
- Fill the Limits column. Name the strongest claim that has no data behind it, or what the measurement does not cover.
- One or two sentences per cell, plain and concrete, ending with a period. Numbers only if they are in the source.
- Put the entry in the section named after the decision someone would be making.
- One pull request per entry, with a title like `Add [Name]`.

## Before you open the pull request

- Run `npx awesome-lint` and fix what it reports.
- Check that the link opens and that the source says what your line says.

If you're not sure whether something fits, open an issue first.
