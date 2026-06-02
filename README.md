# Tutoring Site

A small public companion site for Kramer Gibson's French and Spanish tutoring materials. Plain HTML and CSS, no build step, ready for GitHub Pages.

## Layout

```
tutoring-site/
  index.html            landing page, links to French and Spanish
  french.html           list of French materials (newest first)
  spanish.html          list of Spanish materials (newest first)
  assets/css/site.css   shared styles (warm brand palette)
  files/french/         French PDFs served by the site
  files/spanish/        Spanish PDFs served by the site
  .nojekyll             tells GitHub Pages to serve files as-is
```

## What's on it

Kramer-created French and Spanish tutoring materials from the last six weeks. Student-personalized files, personal language self-tests, and downloaded reference PDFs (copyrighted books, Wikipedia articles) are deliberately left off.

To add a new material later: drop the PDF (or HTML) into `files/french/` or `files/spanish/`, then add one `<a class="file">` block to the matching page, newest at the top, and bump the count on `index.html`.

## Preview locally

```bash
cd "tutoring-site"
python3 -m http.server 8080
# open http://localhost:8080
```

## Publish to GitHub Pages

The repo's gh CLI is already logged in as kramermusician. From this folder:

```bash
cd "tutoring-site"
git init
git add -A
git commit -m "Tutoring site: French and Spanish materials"

# Create a public repo under your account and push (pick a name you like):
gh repo create tutoring-site --public --source=. --remote=origin --push

# Turn on GitHub Pages from the main branch root:
gh api -X POST repos/kramermusician/tutoring-site/pages \
  -f "source[branch]=main" -f "source[path]=/" 2>/dev/null \
  || echo "If that errored, enable Pages in the repo Settings > Pages (Branch: main, Folder: / root)."
```

The live URL will be `https://kramermusician.github.io/tutoring-site/`. It can take a minute or two to go live after the first push.

### Updating later

```bash
git add -A
git commit -m "Add new materials"
git push
```

## Notes

- Total payload is roughly 105 MB. The largest single file is about 33 MB, well under GitHub's 100 MB per-file limit, so no Git LFS is needed.
- All page copy uses Kramer's house style: no em dashes, no team-member names, only Kramer's name on the footer.
