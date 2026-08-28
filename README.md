# CatalogVisualizer

Web application to visualize course catalogs for various years in the UTK EECS department, and to lay out prerequisite/corequisite chains between classes as a connected graph.

Originally built with [Joshua Mandzak](https://github.com/jmandzak/CatalogVisualizer); this copy is maintained independently so it can keep getting doc/bugfix updates.

## How to run it

1. Install dependencies and build the bundle:

   ```
   npm install
   npm run build
   ```

   (`npm run build-watch` instead if you're editing `index.js` and want it to rebuild on save.)

2. This app pulls in a local script (`node_modules/leader-line/leader-line.min.js`) via a plain `<script src>` tag, so it has to be served over HTTP — **opening `index.html` directly from disk (double-clicking it, or a `file://` URL) will silently fail to draw the prerequisite lines.** Serve it locally instead:

   ```
   npx http-server
   ```

   Then open whichever `http://localhost:...` link it prints.

## Known issue

The 2019 catalogs (`cs-2019`, `ce-2019`, `ee-2019`) load and show classes fine, but no prerequisite/corequisite lines get drawn for them. This isn't missing data — it's a formatting mismatch: the app finds course codes in prereq/coreq text with the pattern `SUBJECT NUMBER` (e.g. `MATH 130`), but UTK's 2019 catalog page listed prerequisites without repeating the subject prefix (e.g. just `130`, or spelling out `Mathematics 141` instead of `MATH 141`), so the pattern never matches anything for that year. Every later year (2020+) is formatted consistently and works as expected. Fixing this would mean special-casing the 2019 prereq text in the scraper output, not re-scraping.
