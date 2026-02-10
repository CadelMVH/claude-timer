<!-- Generated: concise, actionable guidance for AI code assistants working on this repo -->
# Repository-specific Copilot Instructions

Purpose: Help AI coding agents quickly make safe, correct edits to this small static web project.

- Big picture: This is a single-page, client-side clock with optional weather visuals. The published app lives in `docs/index.html` (served by GitHub Pages). `archive/timer.html` is a simpler development copy. There is no build system, bundler, or package manifest.

- Key files:
  - `docs/index.html`: primary application (HTML, CSS and JS all inline). Main functions to know: `updateTime()`, `searchCities()`, `selectCity(...)`, `geocodeCity()`, `fetchWeatherForCity()`, and `renderWeatherVisuals()`.
  - `archive/timer.html`: local dev copy; mostly the original clock implementation without weather features.
  - `CLAUDE.md`: project notes and quick-start instructions.

- Runtime & developer workflow:
  - To run locally: open `docs/index.html` (or `archive/timer.html`) in a browser. No build steps.
  - Use browser DevTools console + Network tab when debugging API calls (geocoding / weather).

- Integration points & external APIs:
  - Geocoding: https://geocoding-api.open-meteo.com/v1/search (used by `searchCities()` and `geocodeCity()`). Returned fields used: `name`, `latitude`, `longitude`, `timezone`, `country`, `admin1`.
  - Weather: https://api.open-meteo.com/v1/forecast (current `weather_code` and `is_day` are consumed by `fetchWeatherForCity()`). Weather codes map to descriptive strings via `getWeatherDescription()`.
  - Time formatting uses `Intl.DateTimeFormat` with the `timeZone` option to render a city's time.

- Project-specific patterns and conventions:
  - All styles and scripts are inline in `docs/index.html` — when editing, preserve structure and avoid introducing bundlers.
  - DOM element ids and classes are relied on across scripts: `#time`, `#date`, `#greeting`, `#cityName`, `#citySearch`, `#searchResults`, `#weatherContainer`. Keep these stable unless updating all references.
  - Time is updated with `setInterval(updateTime, 1000)` and `updateTime()` expects `currentTimezone` (nullable). Use `Intl.DateTimeFormat(..., {timeZone})` to compute parts.
  - Weather visuals: `renderWeatherVisuals(weatherType)` populates `#weatherContainer` with elements (sun, moon, clouds, raindrops, snowflakes, lightning). Visual creation functions (`createRaindrops`, `createSnowflakes`) append DOM nodes dynamically.

- Editing guidance & safe change patterns:
  - When changing time logic, update `updateTime()` and keep `Intl.DateTimeFormat` usage for cross-timezone correctness.
  - When changing search or geocoding behavior, preserve the API URL parameters (`count`, `language`) and the expected fields (`latitude`, `longitude`, `timezone`) used elsewhere.
  - If you rename an element id or class, update every usage across `docs/index.html` (search the file for the identifier). There is no build-time checker, so runtime testing in browser is required.
  - Avoid introducing node/npm tooling unless you also add a minimal README section and a `package.json` — the repo intentionally lacks tooling.

- Examples (useful call signatures seen in code):
  - `searchCities(query)` → populates `#searchResults` from geocoding API (up to 10 results).
  - `selectCity(cityName, timezone, latitude, longitude)` → sets `currentTimezone`, `currentCityName`, updates the clock and invokes `fetchWeatherForCity(latitude, longitude)`.
  - `fetchWeatherForCity(lat, lon)` → calls Open-Meteo and uses `data.current.weather_code` and `data.current.is_day`.

- Testing & validation:
  - Open `docs/index.html` in Chrome/Firefox and verify:
    - Searching for a city returns results and selecting one updates the time, city label, background and visuals.
    - Network requests to the geocoding and weather endpoints succeed (check Network tab, response fields).
  - Console errors indicate missing ids or JS syntax issues because everything is inline.

If any part of this file looks incorrect or you'd like more detail (examples of code edits, small refactors, or tests), tell me which area to expand.
