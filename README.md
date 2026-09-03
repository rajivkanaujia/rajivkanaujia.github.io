# rajivkanaujia.github.io
Visit https://rajivkanaujia.github.io 🙂

## Blog structure

- `blog/index.html`: chronological listing at `/blog/`.
- `blog/<slug>/index.md`: Markdown article with a stable permalink.
- `_layouts/blog-post.html`: article layout using the Midnight theme.
- `assets/css/blog.css`: article and listing styles.
- Data Fabric lives at `/blog/data-fabric/`. Its original September 2020 date controls ordering.
- `blog/redirects/` preserves old `/blogs/` URLs; all source content lives under `blog/`.

### Draft and publish

The Ollama article is published. For a new draft, set `published: false` and review it before publication.
To preview a draft with a local Jekyll installation, run `jekyll serve --unpublished`.
Drafts are deliberately omitted from the blog listing; visit the article permalink directly.
After approval, set the intended publication date and change `published` to `true`.
The listing automatically includes published articles, newest first.
Commit and push through the site's existing GitHub Pages deployment process.

For another post, create `blog/<slug>/index.md` with `layout: blog-post`,
`title`, `description`, `date`, `author`, `tags`, `permalink`, and `published`.
