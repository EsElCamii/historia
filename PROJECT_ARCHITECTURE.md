# Architecture

- **Static, no build.** `index.html` (100vh × 100vw globe hero), one HTML file per country (`kenia.html`, scrolls normally), shared `styles.css`. Serve over http (fetch + cross-document view transitions need it): `python3 -m http.server`.
- **Globe = d3-geo orthographic on a 2D canvas**, not three.js. Land is rasterised once into a small equirectangular mask and sampled into ~7k dots; pins are HTML elements positioned by the same projection. Keeps the hero light.
- **Page-to-page motion** uses native `@view-transition { navigation: auto; }`; the globe zooms toward the country before navigating. Browsers without support just navigate.
- **Adding a country:** give its entry in `COUNTRIES` (index.html) an `href`, swap its row from `<button aria-disabled>` to `<a>`, and copy `kenia.html` as the template.
- **Photos** are Wikimedia Commons (CC BY / BY-SA), stored in `assets/`, with attribution in `assets/CREDITS.txt` and the page footer.
