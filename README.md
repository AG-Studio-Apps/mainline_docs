# Mainline Docs

Documentation site for [Mainline](https://mainline.agnticstudio.com/), built with Jekyll and hosted on GitHub Pages with a custom domain.

## Preview locally

```bash
bundle install
bundle exec jekyll serve
```

Then open http://localhost:4000/ in your browser.

## Deploy

Push to `main`. GitHub Pages builds and deploys automatically (no Actions config required). The `CNAME` file at the repo root points the GitHub Pages site at `mainline.agnticstudio.com`.
