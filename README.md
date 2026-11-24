# nedbday.github.io

Landing page for **North East Database Day (NEDB Day)**, served at <https://nedbday.github.io>.
It is a single `index.html` that links to each year's event site.

Since 2025, each year lives in its own repo in the `nedbday` org. A repo named `<year>` is served by GitHub Pages at `https://nedbday.github.io/<year>/`.

## Creating a site for a new year

This example creates 2027 from the 2026 site:

1. **Create the new repo from 2026.** Pick one of these options:
   - **Template** (starts with a fresh history). First mark `nedbday/2026` as a template, either in its Settings → "Template repository" or by running `gh repo edit nedbday/2026 --template`. Then:
     ```bash
     gh repo create nedbday/2027 --public --template nedbday/2026 --clone
     ```
   - **Copy** (keeps the git history):
     ```bash
     git clone https://github.com/nedbday/2026.git 2027 && cd 2027
     git remote remove origin
     gh repo create nedbday/2027 --public --source=. --remote=origin --push
     ```
2. **Turn on GitHub Pages** (from `main`, root folder). You can do this in the repo's Settings → Pages, or run:
   ```bash
   gh api -X POST repos/nedbday/2027/pages -f 'source[branch]=main' -f 'source[path]=/'
   ```
3. **Update the content.** Change every `2026` to `2027`, including the absolute `nedbday.github.io/2026` URLs in `index.html`'s meta tags, `site.xml` and `README.md`. To find them all, run `grep -rn 2026 .`. Then update the dates, venue, host, program and banners. Commit and push. The site goes live at `https://nedbday.github.io/2027/` within a few minutes.

## Updating the main page

Edit `index.html` in this repo. Add the new year at the top, using the same format:

```html
<a href="https://nedbday.github.io/2027/">North East Database Day 2027</a> (Host University)
<br>
```

Commit and push to `main`. GitHub Pages republishes <https://nedbday.github.io> automatically.
