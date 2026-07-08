# scottmiller.io

Personal site for Scott Miller. Hand-written, static, no build step.

## Stack

- Plain HTML
- [Tailwind CSS](https://tailwindcss.com/) via CDN
- Vanilla JavaScript (no frameworks, no bundler)
- A `topo.png` background image

Hosted as a static site on DigitalOcean App Platform.

## Layout

```
index.html         # Home page
topo.png           # Background image
blog/
  index.html       # Blog index: lists posts from posts.json
  posts.json       # Post manifest (the only file to edit when adding a post)
  <slug>/
    index.html     # Individual post (one folder per post, pretty URL)
```

The home page and blog pages share the same visual language: mono font, topo
background, Tailwind utility classes, the GitHub/LinkedIn footer with inline
SVGs.

## Local development

No build step. To preview locally:

```sh
python3 -m http.server 8000
# then open http://localhost:8000/
```

Any static file server works (`npx serve`, `caddy file-server`, etc.).

## Adding a blog post

1. Create a new folder under `blog/` whose name is the post's URL slug
   (lowercase, hyphens, no spaces). Example: `blog/my-new-post/`.
2. Inside that folder, create `index.html`. Use
   `blog/hello-world/index.html` as a template — same `<head>`, same
   `background-image:url('../../topo.png')`, same `font-mono` body, same
   `max-w-prose` content card.
3. Add an entry to `blog/posts.json` with the slug, title, ISO date
   (`YYYY-MM-DD`), and a one-sentence description. Newest first.
4. Update the visible date and description in the post's `<header>` to match
   the values you put in `posts.json` (the post page is static, so the
   header doesn't read from the manifest).
5. Commit and push (or upload the new folder + updated `posts.json` to
   DigitalOcean App Platform).

## Editing the home page

`index.html` at the repo root. The home page is a single centered card with a
short bio and links to projects. Edit and commit.

## Blog post format (quick reference)

A complete post template you can copy and adapt. Everything is self-contained
in one file — no partials, no includes.

Note the relative paths: from `blog/<slug>/index.html`, `../` lands in `blog/`
and `../../` lands at the site root.

```html
<html lang="en">
  <head>
    <title>Your Post Title - Scott Miller</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.tailwindcss.com"></script>
  </head>

  <body class="font-mono" style="background-image:url('../../topo.png');">
    <div class="max-w-3xl mx-auto px-4 py-10 md:py-16">
      <header class="mb-8">
        <a href="../" class="text-sm hover:underline">&larr; back to blog</a>
        <h1 class="text-2xl font-bold mt-4 mb-1">Your Post Title</h1>
        <div class="text-sm text-neutral-700">Month D, YYYY</div>
        <p class="mt-2 text-neutral-800">One-sentence description.</p>
      </header>

      <article class="bg-white/90 shadow rounded-lg p-6 md:p-8 space-y-4 max-w-prose mx-auto">
        <p>First paragraph...</p>
        <p>More paragraphs...</p>
      </article>

      <section class="mt-10 bg-white/90 shadow rounded-lg p-6 md:p-8 max-w-prose mx-auto">
        <h2 class="text-sm font-bold text-neutral-700 mb-3">More posts</h2>
        <ul id="more-posts" class="space-y-2 text-sm"></ul>
      </section>

      <footer class="mt-10 flex items-center justify-center space-x-6 text-xs text-neutral-700">
        <a href="https://github.com/scott" class="flex items-center space-x-1 hover:underline">
          <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" fill="currentColor" viewBox="0 0 16 16" aria-hidden="true" focusable="false">
            <path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.012 8.012 0 0 0 16 8c0-4.42-3.58-8-8-8z" />
          </svg>
          <span>GitHub</span>
        </a>
        <a href="https://linkedin.com/in/optimizeit" class="flex items-center space-x-1 hover:underline">
          <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" fill="currentColor" viewBox="0 0 16 16" aria-hidden="true" focusable="false">
            <path d="M0 1.146C0 .513.526 0 1.175 0h13.65C15.474 0 16 .513 16 1.146v13.708c0 .633-.526 1.146-1.175 1.146H1.175C.526 16 0 15.487 0 14.854V1.146zm4.943 12.248V6.169H2.542v7.225h2.401zm-1.2-8.212c.837 0 1.358-.554 1.358-1.248-.015-.709-.52-1.248-1.342-1.248-.822 0-1.359.54-1.359 1.248 0 .694.521 1.248 1.327 1.248h.016zm4.908 8.212V9.359c0-.216.016-.432.08-.586.173-.431.568-.878 1.232-.878.869 0 1.216.662 1.216 1.634v3.865h2.401V9.25c0-2.22-1.184-3.252-2.764-3.252-1.274 0-1.845.7-2.165 1.193v.025h-.016a5.54 5.54 0 0 1 .016-.025V6.169h-2.4c.03.678 0 7.225 0 7.225h2.4z" />
          </svg>
          <span>LinkedIn</span>
        </a>
      </footer>
    </div>

    <script>
      (function () {
        var list = document.getElementById('more-posts');
        if (!list) return;

        var parts = window.location.pathname.split('/').filter(function (p) { return p.length > 0; });
        var last = parts[parts.length - 1];
        var currentSlug = (last === 'index.html' ? parts[parts.length - 2] : last) || '';

        fetch('../posts.json')
          .then(function (r) { return r.json(); })
          .then(function (posts) {
            var others = posts.filter(function (p) { return p.slug !== currentSlug; }).slice(0, 5);
            if (others.length === 0) {
              list.parentElement.style.display = 'none';
              return;
            }
            list.innerHTML = others.map(function (post) {
              var date = new Date(post.date + 'T00:00:00').toLocaleDateString('en-US', {
                year: 'numeric', month: 'long', day: 'numeric'
              });
              return (
                '<li class="flex items-baseline space-x-2">' +
                  '<a href="../' + post.slug + '/" class="hover:underline">' + post.title + '</a>' +
                  '<span class="text-neutral-600">&middot;</span>' +
                  '<span class="text-neutral-600">' + date + '</span>' +
                '</li>'
              );
            }).join('');
          })
          .catch(function () { list.parentElement.style.display = 'none'; });
      })();
    </script>
  </body>
</html>
```

## Conventions

- Mono font everywhere (no serif headlines).
- Post content cards use `bg-white/90` for readability against the topo
  background; the rest of the page shows topo.
- Pretty URLs: one folder per post, each with its own `index.html`. No
  rewrites needed — works on any static host.
- The post list and "More posts" section are rendered client-side from
  `posts.json` by a small inline `<script>`. `<noscript>` fallbacks are
  included on the blog index for SEO and no-JS visitors.
- Dates are stored as ISO `YYYY-MM-DD` and rendered as e.g. "July 8, 2026"
  via `toLocaleDateString` (with a `T00:00:00` suffix to avoid timezone
  off-by-one).

## Deployment

Push to the branch DigitalOcean App Platform watches (typically `main`). No
build command, no output directory override — it serves the repo as-is.

## Future additions (not implemented yet)

- RSS / Atom feed at `blog/feed.xml`
- Tags or categories
- Syntax highlighting for code blocks (Prism via CDN)
- Sitemap and favicon
