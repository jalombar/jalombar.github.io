# jalombar personal website

Source for Jamie Lombardi's personal academic site, built with
[Jekyll](https://jekyllrb.com/) and hosted on GitHub Pages. GitHub builds the
site automatically on every push to `site-rebuild`; there is nothing to install and no
build step to run.

## How the site is organized

| Path | What it is |
|---|---|
| `_config.yml` | Site title, description, and the `baseurl` setting |
| `_data/navigation.yml` | The navigation tabs |
| `_data/papers.yml` | The paper cards on the Research page |
| `_data/movies.yml` | The simulation movies on the Research page |
| `_data/links.yml` | The Favorite Links page content |
| `_data/outreach.yml` | The Outreach page content |
| `_layouts/default.html` | The shared page frame (header, nav, footer) |
| `assets/css/main.css` | All styling; colors are defined at the top |
| `index.html`, `about.html`, ... | The pages themselves |

Most updates only touch a file in `_data/`.

## Common tasks

### Add or remove a navigation tab

Edit `_data/navigation.yml`. Each tab is a small block; delete a block to
remove its tab, or copy one to add a tab. Entries with `external: true` point
at a full URL and open in a new browser tab. The order in the file is the
order on the page.

### Add a paper to the Research page

1. Pick a figure from the paper and save it (roughly 1200 px wide) into
   `assets/images/papers/`, named like `firstauthor2027.jpg`.
2. Copy the top block of `_data/papers.yml`, paste it above the others, and
   fill in the title, citation, arXiv ID, image path, image description, and a
   one or two sentence plain-English summary.

### Add a simulation movie

1. Convert the movie to web-friendly mp4, for example:
   `ffmpeg -i in.avi -c:v libx264 -crf 23 -pix_fmt yuv420p -movflags +faststart out.mp4`
2. Make a poster frame: `ffmpeg -ss 10 -i out.mp4 -frames:v 1 poster.jpg`
3. Put the movie in `assets/movies/`, the poster in `assets/images/posters/`,
   and copy a block in `_data/movies.yml`. Keep movies under about 50 MB.

### Update Favorite Links or Outreach

Edit `_data/links.yml` or `_data/outreach.yml`. Please check that a URL
actually loads before adding it; the whole point of this site is no dead
links.

## Publishing

The repository is named `jalombar.github.io`, so GitHub Pages serves it at the
root: `https://jalombar.github.io`. Because the repository name matches the
account, `baseurl` in `_config.yml` is empty. Every internal link is written
relative to `baseurl`, so links keep working no matter what `baseurl` is set to.

## Optional local preview

Requires Ruby 3.3 or newer. From the repository root:

```
bundle install
bundle exec jekyll serve --baseurl ""
```

Then open http://localhost:4000. Pushing to GitHub works fine without this;
GitHub performs the same build itself.
