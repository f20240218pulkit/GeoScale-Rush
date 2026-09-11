# GeoScale Rush — local source

This package contains all the game source and the complete bundled map dataset.
The game files are identical to the original implementation. No npm install,
framework, API key, external map service, or build step is required.

## Folder structure

- geoscale-rush/
  - README.md
  - dist/
    - index.html — page structure and dialogs
    - style.css — appearance and responsive layout
    - game.js — game logic, city coordinates, map rendering, controls and scoring
    - world.json — complete Natural Earth country-boundary dataset
    - icon.svg — browser-tab icon

The original hosted project also has .openai/hosting.json and Git metadata.
Those are hosting-specific and are not needed or included for local use.

## Run on Windows

1. Extract the ZIP. Open the extracted geoscale-rush folder in VS Code.
2. Open Terminal > New Terminal. Check that the terminal is in the folder
   containing README.md and dist.
3. With Python 3 installed, run:

   py -m http.server 8000 --bind 127.0.0.1 --directory dist

4. Open http://localhost:8000 in your browser.
5. Leave the terminal running while you play. Press Ctrl+C to stop the server.

If the py command is unavailable but Python is installed, try:

   python -m http.server 8000 --bind 127.0.0.1 --directory dist

On macOS or Linux, use:

   python3 -m http.server 8000 --bind 127.0.0.1 --directory dist

If you already use the VS Code Live Server extension, you can instead
right-click dist/index.html and choose Open with Live Server.

Do not simply double-click index.html: the game loads world.json using fetch,
which needs this folder to be served over HTTP. Keep world.json in dist beside
index.html and game.js. If manually creating files, preserve their extensions;
for example, game.js must not be saved as game.js.txt.

## Editing

Edit index.html for the interface, style.css for styling, and game.js for
logic. The cities array in game.js contains [city, country, latitude, longitude].
Refresh the browser after saving. world.json is data, not executable code.

## Behavior and validation

The game has five randomized city pairs, Haversine distances using R = 6371 km,
a 100–20,000 km estimate slider in 50 km steps, relative-error accuracy,
city reveals, and a round-by-round summary. Displayed mean accuracy is rounded
to a whole percentage.

The political map supports drag, pinch, wheel zoom, plus/minus/reset buttons,
and keyboard controls when the map is focused: arrow keys pan, + and - zoom,
and 0 resets. Great-circle routes unwrap longitude across the date line.

JavaScript syntax, local asset presence, known distance and scoring cases,
and all 946 possible city-pair routes were checked. Browser-based end-to-end
or visual testing has not been performed.

## Map data

Natural Earth, public domain, 1:110m administrative countries (177 features).
Source: https://github.com/nvkelso/natural-earth-vector/blob/master/geojson/ne_110m_admin_0_countries.geojson
The boundaries are shown as supplied.
