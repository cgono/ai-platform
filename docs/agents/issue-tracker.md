# Issue tracker: GitHub

Issues and specs live in GitHub Issues for `cgono/ai-platform`.
Use the `gh` CLI from this clone, or pass `--repo cgono/ai-platform`.

## Operations

- Create: `gh issue create --title "..." --body-file <file>`.
  Use a Markdown file for multiline bodies.
- Read: `gh issue view <number> --json number,title,body,labels,comments`.
- List: `gh issue list --state open --json number,title,body,labels`.
  Add label and state filters as needed.
- Comment: `gh issue comment <number> --body-file <file>`.
- Apply labels: `gh issue edit <number> --add-label "<label>"`.
- Remove labels: `gh issue edit <number> --remove-label "<label>"`.
- Close: `gh issue close <number> --comment "..."`.

When a skill says "publish to the issue tracker", create a GitHub issue.
When it says "fetch the relevant ticket", read the GitHub issue.

## Pull requests as a triage surface

**PRs as a request surface: no.**

## Wayfinding operations

For `/wayfinder`, the map is an issue labelled `wayfinder:map`.
Child tickets use `wayfinder:<type>` labels:
`research`, `prototype`, `grilling`, or `task`.

Link children using GitHub sub-issues. If unavailable, list children
in the map's task list and put `Part of #<map>` in each child's body.

Record blockers with GitHub native issue dependencies. If unavailable,
put `Blocked by: #<number>` at the top of the child's body.

The next ticket is the first open child in map order with no open
blockers and no assignee. Claim with `gh issue edit <number>
--add-assignee @me`. Resolve by commenting, closing, and adding a
summary and link to the map's Decisions-so-far.
