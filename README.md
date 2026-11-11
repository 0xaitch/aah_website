# aah_website

Static site in a single file: `index.html` (~2.8 MB). No framework, no build step, no dependencies.

## File structure

- **HTML:** two views (`#home`, `#collection`) toggled by `show()`, plus a native `<dialog id="dlg">` for the product detail popup.
- **CSS:** inline `<style>`. Colors are CSS variables on `:root`. Dark mode follows `prefers-color-scheme` and can be forced with `data-theme="light"` or `data-theme="dark"` on `<html>`.
- **JS:** inline `<script>`, vanilla, no libraries.

## Data

- `IMG`: array of 19 base64-encoded JPEGs. All images are embedded, which is why the file is large.
- `CAT`: category key to label map (`buddha`, `tier`, `nature`, `modern`).
- `P`: product array. Each entry is `[imageIndex, name, categoryKey, description]`.

## Article codes

Generated at runtime and written to `p[4]`:

```js
const PF={buddha:'BD',tier:'TR',nature:'NT',modern:'CT'},cnt={};
P.forEach(p=>{cnt[p[2]]=(cnt[p[2]]||100)+1;p[4]='AAH-'+PF[p[2]]+'-'+cnt[p[2]]});
```

Numbering starts at 101 per category and follows array order. Append new products to the end of `P` to keep existing codes stable. Product names (`p[1]`) are only used for image `alt` text and the internal `byName()` lookup for featured tiles.

## Rendering

- `tile(p,k)` builds a card: code in `<b>`, category in `<i>`.
- `draw()` renders the category filter chips and the `#grid`.
- `open_(k)` fills and opens the dialog.
- `wa(text)` builds `https://wa.me/918859114786?text=...` links for enquiry buttons.

## External requests

Google Fonts only (Italiana, Jost). Everything else is local to the file.

## Hosting

Works on any static host. For GitHub Pages: Settings → Pages → deploy from `main`, root folder.
