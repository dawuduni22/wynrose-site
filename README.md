# Wynrose Investment Research — site

Plain static HTML. No build step, no dependencies, no framework. Open the
folder in VS Code and edit the files directly. To preview locally, either open
`index.html` in a browser or use the Live Server extension.

## Files

```
index.html        Homepage (nameplate, skyline band, what we publish)
about.html        About + contact
disclaimer.html   Disclaimer
research.html     Research index — BUILT BUT NOT LINKED YET
styles.css        All styling for every page
assets/           Logo, favicon, skyline
notes/            Put the research PDFs here
```

## Turning the research page on

`research.html` exists and works, but it is not linked from the nav and it
carries `<meta name="robots" content="noindex">`. To switch it on:

1. In `index.html`, `about.html` and `disclaimer.html`, find this line
   (it appears twice per file, once in the nav and once in the footer):

   ```html
   <!-- <a href="research.html">Research</a> -->
   ```

   Delete the `<!--` and `-->` around it.

2. In `research.html`, delete the `<meta name="robots" content="noindex">` line.

That is the whole switch. Six uncomments and one deletion.

## Adding a note

In `research.html`, copy one `<article class="note">` block, paste it at the
top of the list, and change:

- the number in `<span class="num">`
- the date in `<span class="date">`
- `data-sector` on the `<article>` (must match a `data-filter` on a button)
- the title and the summary
- the `href` on the View PDF link

Then remove `aria-disabled="true"` from the link so it stops rendering as
inactive, and drop the PDF into `notes/`.

Newest note goes at the top. Numbers count up.

## Palette

Taken straight from the logo file.

| Token      | Hex       | Use                                       |
|------------|-----------|-------------------------------------------|
| `--page`   | `#D9D9D9` | Page background (one step lighter than logo grey) |
| `--band`   | `#CBCBCB` | Skyline strip and footer — exact logo grey |
| `--ink`    | `#000000` | All text                                   |
| `--muted`  | `#565656` | Secondary text                             |
| `--hair`   | `#A8A8A8` | Hairline rules                             |
| `--accent` | `#7A0000` | The dot, one rule, link hover              |

All six live at the top of `styles.css`. Change them there and they change
everywhere.

## Swapping the skyline

`assets/skyline.svg` is a generated placeholder silhouette so you can see the
layout. Replace it with a real photograph:

1. Drop the photo in as `assets/skyline.jpg`. A wide landscape shot with the
   skyline low in the frame crops best. Around 2400px wide is plenty.
2. In `index.html` and `about.html`, change
   `src="assets/skyline.svg"` to `src="assets/skyline.jpg"`.
3. In `styles.css`, find `.skyline img` and adjust `opacity: 0.085`.
   Photographs usually want a touch more, around `0.10`.

The light grey pixel haze sits in `.skyline::after` as two repeating gradients.
To make the grid chunkier, raise the `2px` / `5px` values together (`3px` / `7px`
gives noticeably bigger pixels). To make the haze denser, raise the
`rgba(217,217,217,0.28)` background-colour alpha.

For genuine pixelation rather than a grid overlay, downscale the source photo
before you export it. Something around 300 to 500px wide will visibly blockify,
because `image-rendering: pixelated` is already set on the image.

Make sure you have the rights to whatever photo you use. Unsplash and Pexels
are fine for this.

## Before you push

- Change `contact@wynrose.org` to the real address. It appears in the footer of
  every page and once on `about.html`.
- Set up the email on the domain rather than forwarding to a Gmail address.
- Check the disclaimer wording with someone qualified before the first note
  goes up.

## Deploying

Any static host works. Netlify or Cloudflare Pages will take the folder by drag
and drop, or connect a GitHub repo and push. No configuration needed.
