# static_web

The public showcase page for Tricity Property Radar. Plain HTML and CSS, no build
step, no JavaScript, no server. Open `index.html` in a browser and it works.

```
static_web/
├── index.html     the page
├── 404.html       shown for any other address
├── styles.css     all styling; design tokens copied from the app
├── favicon.svg
└── README.md
```

## Hosting it on GitLab Pages

`.gitlab-ci.yml` **at the repository root** (not in this folder) copies `static_web/`
into `public/`, which is the only directory name GitLab Pages serves. That rename is
all the job does.

1. Push the repository to GitLab.
2. In the project, open **Deploy → Pages**. The first pipeline publishes the site.
3. The URL appears on that page, usually `https://<user>.gitlab.io/<project>/`.

Only the default branch publishes, so a work-in-progress branch cannot overwrite the
live page.

### Opening it locally

Any static server will do, or just open the file:

```sh
python3 -m http.server --directory static_web 8080
```

The 404 page links with absolute paths (`/styles.css`), so it looks right when served
from a domain root but unstyled if you double-click the file. That is expected.

## Before this goes public

- [ ] **Remove the `noindex` tag** from `index.html` and `404.html`. It is there on
      purpose: an indexed page would start sending real investors to a product that
      cannot serve them yet. Take it out when you want to be found, not before.
- [ ] **Replace the contact address.** `hello@tricityradar.in` is a placeholder and
      does not exist. It is in the footer of `index.html`.
- [ ] **Check the build-status section** against reality. It is dated October 2026 in
      the copy and will read as stale once it is wrong.
- [ ] Add the real `og:image` if you want link previews to show something.

## Editing it

The palette, radii and fonts at the top of `styles.css` are copied **verbatim** from
`frontend/src/app/globals.css`. Nothing compiles the two together, so if a colour
changes in the app, change it here too — otherwise the site and the product slowly
stop looking like the same thing.

The figures in the hero ledger are illustrative and labelled as such on the page. If
you replace them with real ones, the tier chip beside each has to match how that
figure is actually known. The whole point of the page is that those labels are
honest.

## Fonts

Three faces load from Google Fonts: DM Serif Display (headings), Inter (body) and
DM Mono (numeric values only — never labels, because mono on a label is decoration
and mono on a figure is information).

The fallback stack is Georgia / system-ui / ui-monospace, and the page was checked
with the Google request **blocked** as well as allowed — it still reads correctly
either way, just with different serifs. If you would rather not depend on an external
request at all, download the three `.woff2` files into `static_web/fonts/`, replace the
`<link>` tags with `@font-face` rules in `styles.css`, and nothing else has to change.
