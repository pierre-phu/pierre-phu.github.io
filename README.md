# pierre-phu.github.io

Source of [pierre-phu.github.io](https://pierre-phu.github.io), my side projects site. GitHub Pages builds it with Jekyll on every push to `main`.

## Layout

| Path | What it holds |
| --- | --- |
| `index.html` | Home page: intro, project cards, contact |
| `_projects/` | One Markdown file per project |
| `_layouts/` | `default` (header, footer) and `project` (project page) |
| `assets/css/main.css` | All styles, with light and dark themes |
| `assets/img/<project>/` | Images, resized to 1600 px max |
| `assets/video/` | Short MP4 clips (use these instead of GIFs) |

## Add a project

Create `_projects/<slug>.md`. It is served at `/projects/<slug>/`.

```yaml
---
title: Project name
description: One sentence, shown under the title and in link previews.
summary: One sentence for the home page card.
year: 2026
context: Where or why it was made
group: ml          # ml = "Machine learning", making = "Built by hand"
order: 5           # position on the home page and in previous/next links
tools: [Python, PyTorch]
facts:             # optional extra rows under the title
  - label: Data
    value: 500 labeled frames
links:             # optional
  - label: Code on GitHub
    url: https://github.com/pierre-phu/...
card: /assets/img/<slug>/card.jpg      # 960×600
image: /assets/img/<slug>/card.jpg     # link preview image
cover: /assets/img/<slug>/cover.jpg    # 1600×900
cover_alt: Describe the cover image
---
```

## Preview locally

With Docker, using the same builder as GitHub Pages:

```sh
docker run --rm -v "$PWD":/src -v "$PWD/_site":/out -e PAGES_REPO_NWO=pierre-phu/pierre-phu.github.io \
  --entrypoint github-pages ghcr.io/actions/jekyll-build-pages:v1.0.13 build --source /src --destination /out
python3 -m http.server -d _site 4000
```

Or with Ruby: `bundle install && bundle exec jekyll serve`.
