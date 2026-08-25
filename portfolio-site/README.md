# Portfolio site

A static site built with Jekyll, which GitHub Pages runs natively — you
push markdown files, GitHub builds the HTML for you. You never need to
write or edit HTML to add content.

## 1. Put this on GitHub Pages

1. Create a new **public** GitHub repo named exactly `yourusername.github.io`
   (replace `yourusername` with your actual GitHub username — this exact
   name is what makes GitHub serve it as a site automatically).
2. Push everything in this folder to that repo's `main` branch.
3. In the repo, go to **Settings → Pages** and confirm the source is
   "Deploy from a branch", branch `main`, folder `/ (root)`.
4. Wait a minute or two, then visit `https://yourusername.github.io`.

If you'd rather use a repo with a different name (e.g. `portfolio`), that
also works — GitHub will serve it at `https://yourusername.github.io/portfolio/`.
In that case, set `baseurl: "/portfolio"` in `_config.yml` first.

## 2. Edit the basics

Open `_config.yml` and fill in your name, email, GitHub/LinkedIn URLs, and
(optionally) a CV PDF path. That's the only file with your identity in it.

## 3. Add a new project

1. Copy `_projects/TEMPLATE.md` to a new file in `_projects/`, e.g.
   `_projects/my-new-project.md`.
2. Fill in the fields at the top (title, summary, tags, repo link).
3. Write the body in plain markdown — headings with `##`, links with
   `[text](url)`, images with `![](/assets/img/filename.png)`.
4. Set `published: true` (or delete that line) when it's ready to appear.
5. Commit and push. It appears automatically on `/projects/` — no HTML to touch.

Delete `_projects/TEMPLATE.md` itself before you go live, or leave
`published: false` in it — either way it won't render.

## 4. Add a new note

Same process, using `_writeups/TEMPLATE.md` in the `_writeups/` folder.
Notes are sorted by the `date:` field, newest first.

## 5. Preview changes locally before pushing (optional)

Requires Ruby installed. From this folder:

```
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`. Not required — you can also just push
and check the live site after GitHub finishes building (usually under a
minute; check the Actions tab on the repo if it doesn't update).

## Structure

```
_config.yml          site name, links, collection settings — edit this
_projects/            one markdown file per project
_writeups/            one markdown file per technical note
_layouts/, _includes/ the HTML templates — you shouldn't need to touch these
assets/css/style.css  all the visual design in one file
index.md              the About/home page text
projects.md, notes.md the listing pages (just front matter, no edits needed)
```
