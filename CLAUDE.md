# Stepwise

Step-by-step visual walkthroughs of LeetCode solutions. The whole app is one static file, `index.html` (inline CSS + JS, no build step, no dependencies besides Google Fonts).

## How the code is organized (inside `index.html`)

- **CSS tokens** at the top of `<style>`: every color is a CSS variable on `:root`, redefined for dark mode. Never hard-code a color in a component; use the tokens.
- **Helpers**: `arrayView`, `mapView`, `resView`, `stackView`, `panel`, `row`, `note`, `arrow`, `listView`, `treeView` / `buildTree`, `dpRowView`, `barsView`, `roomsView`. Reuse these before writing a new renderer.
- **Problems**: each one is registered with `def({...})`. The sidebar groups problems by `cat`, in the order they are defined, so a new problem must sit next to the others in its category.
- **Input parsing**: `parseParam` handles the param types `int`, `str`, `ints`, `tree`, `grid`, `matrix`, `rooms`. Extra cross-field checks go in `run()` in the UI section.

## Adding a problem

A problem object has: `id`, `num`, `title`, `diff` (Easy/Medium/Hard), `cat`, `pattern`, `slug` (LeetCode URL slug), `statement`, `idea`, `time`, `space`, `params`, `code` (array of Python lines), and `run(args)`.

`run` returns the steps from `mkSteps()`. Each step is `S.add(line, msg, vars, html)`:
- `line`: 0-based index into `code` to highlight. It must match the line actually executing.
- `msg`: one or two plain-English sentences saying what happened and **why**. Wrap the key value in `<b>`. Escape user input with `esc()`.
- `vars`: the variables worth watching at this step.
- `html`: a full snapshot of the stage, rendered at that moment (render strings, don't store live objects).

Style rules for explanations: the reader is learning, so explain the reason behind every move, not just the move. Use American English. Keep visuals small enough to read (cap input sizes in `params`).

## Before committing

1. Open the page and step through the new problem with its default input and with edge cases (empty, single element, not-found, etc.). Make sure there are no console errors.
2. Check light and dark mode, and a ~400px-wide viewport.
3. Add the problem to the table in `README.md`.

## Git

- Commit and push directly to `main` unless asked otherwise.
- Do not add any AI attribution: no `Co-Authored-By` lines, no "Generated with" footers, no AI names as authors.
