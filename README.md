# Embedded Tweet Viewer

Host interactive X (formerly Twitter) posts on your own site with a clean, official-widgets integration.

Paste a post URL or the HTML from **Embed post**, and the viewer renders it with X’s `widgets.js` so media, threading UI, and engagement controls stay in sync with the source post.

## Included files

- `index.html` — single-page gallery UI, styling, first-party cookie persistence, and X widget loader
- `README.md` — project docs

## Getting started

1. Clone or download this repository.
2. Open `index.html` in a modern browser, or deploy the file to any static host (GitHub Pages, Netlify, S3, your own server, etc.).
3. Keep an internet connection available so the page can load `https://platform.twitter.com/widgets.js`.

## Add posts

### In the browser

1. On X, open a post → **Share** → **Copy link**, or **Embed post** and copy the HTML.
2. Paste the URL or embed markup into **Add a post**.
3. Click **Add embed**.

Supported inputs:

- Status URLs such as `https://x.com/user/status/123…`
- Legacy `twitter.com` status URLs
- Bare status IDs
- Official `<blockquote class="twitter-tweet">…</blockquote>` embed snippets

Posts you add are saved in first-party cookies on that browser (no server or account required). Only compact status IDs and URLs are stored so the payload stays lightweight; live embeds are rebuilt with X widgets on each visit.

### Permanently in the page (for public hosting)

Edit the `DEFAULT_TWEETS` array near the bottom of `index.html`:

```js
const DEFAULT_TWEETS = [
  {
    id: "2096694989728440498",
    url: "https://x.com/bjguru24/status/2096694989728440498",
    html: null // optional: paste full embed HTML here
  }
];
```

Deploy the updated `index.html` so every visitor sees those embeds by default.

## How integration works

1. The page parses the status ID from your URL or embed HTML.
2. It loads the official X widgets script once.
3. Each card calls `twttr.widgets.createTweet(...)` (or `widgets.load` when embed HTML is present).
4. X returns the live embed (text, media, timestamp, and link back to the original post).

This keeps compliance with X’s embed path while still letting you curate a gallery on your domain.

## Notes

- Embeds require access to X’s widget endpoints; blocked networks or strict privacy tools may prevent rendering.
- Gallery membership is stored in first-party cookies (`SameSite=Lax`, 1-year expiry) on the visitor’s device. Serve the page over `http://` or `https://` so cookies can persist (opening the file directly as `file://` is unreliable for cookies).
- Removing a card only affects the local gallery, not the original post on X.
- For a multi-author archive, keep adding status URLs; the layout is a responsive card grid.

## Customize

- Theme colors live in the `:root` CSS variables at the top of `index.html`.
- Dark embeds are requested via `theme: "dark"` in the widget options.
- `dnt: true` is enabled so embeds request Do Not Track where supported.
