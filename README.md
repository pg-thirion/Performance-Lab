# Performance Lab

A dependency-free, responsive, privacy-first gaming benchmark workspace. Open index.html through a local HTTP server or deploy the repository to Vercel. Vercel's fixed upstream rewrite exposes the benchmark data without a general-purpose server-side URL proxy.

## Data

Open GPU Benchmarks: https://opengpubenchmarks.com (CC BY 4.0: https://creativecommons.org/licenses/by/4.0/). The dashboard adapts its published, non-synthetic game records and preserves available provenance. Its upstream source was inspected on 2026-11-26. Coverage depends on the upstream dataset. Missing measurements are blank. Reciprocal mean frame time is explicitly marked approximate when no frame-time measurement is provided. Imported measurements are not independently verified.

## Features

- Automatic measured online feed, manual refresh, timestamp, cached fallback, import errors, source attribution, source links, proof-level labelling.
- Search, game/GPU/CPU/resolution/preset/upscaling/frame generation/OS/form factor/vendor/source/API filters, FPS target, minimum 1% low, maximum GPU temperature, verified-only and favourite-only filters, reset, persistent filters.
- Match counts, maximum FPS, maximum 1% low, target attainment, ranking charts with 13 metrics, sorting, pagination, configurable page size, record details.
- Four-way comparisons, baseline selection, FPS percentage change, differences warning, saved named sets, comparison print report.
- Settings optimiser based on matching tested hardware/OS, frame-time budget, target attainment, individual settings breakdown.
- CSV, JSON, online direct URL, manual entry, generic frame-time CSV and JSON arrays, basic CapFrameX-style capture JSON where CaptureData.MsBetweenPresents is an array; validation, duplicate ID suppression, CSV template, source metadata.
- Calculated FPS, slowest-1% reciprocal FPS, P99, min/max FPS, stutter percentage (>50 ms), downsampled frame-time trace, FPS/watt, low-to-average ratio.
- Personal library, result deletion, favourites, JSON backup and restore, filtered CSV/JSON export, CSV formula-injection mitigation.
- FPS/frame-time conversion, refresh interval, performance uplift, FPS/watt, cost/FPS, frame-time headroom, energy use.
- Responsive layout, light/dark theme, keyboard-accessible controls, CSP, clickjacking protection, restricted device permissions, bounded downloads, fixed upstream proxy.

## Import format

Use the CSV template in the app. Structured JSON can be an array or an object with records. Frame capture JSON can use {"frametimes":[16,17,15]} with metadata entered in the form; capture CSV can use a MsBetweenPresents or frametime_ms column. These are supported formats, not a guarantee of compatibility with every capture tool/version. File and URL imports are limited to 10 MB, 100,000 raw rows and 5,000 benchmark records. Online URL imports require CORS and run directly in the browser; only the fixed public benchmark feed is proxied.

## Storage and deployment

No accounts, database, paid API, server-side telemetry or background jobs. Personal data and the cached feed live in localStorage; back up regularly. Quota/browser clearing can cause loss. Do not treat published results across different systems as controlled tests. Hosting is Vercel static hosting. Run a local server, e.g. python -m http.server 8080, and use the direct upstream fallback during local development.

### Expanded sources (2026-11-26)

All sources are adapted under CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/). Each online feed refreshes independently; when a feed fails its last successfully cached results remain available.

- SteamFPS — SteamOS Playability Dataset (https://steamfps.com/state-of-steamos), https://github.com/xpressmike/steamos-playability-dataset, with upstream measurement credit to https://deck-verified.games. Import only rows with deck_provenance=community and positive deck_fps. These are representative community FPS values rather than controlled averages, and no unknown settings or frame-time metrics are inferred. The settings optimiser excludes these rows.
- TechFuelHQ — ASUS ROG Astral RTX 5080 OC First-Party Bench Dataset (https://techfuelhq.com/data/gpu/rog-astral-rtx-5080-oc-2026-06-09/). Import measured 4K gaming and frame generation configurations. The independently logged June 28 GPU sensor time series is a separate thermal-only record with temperature, board power, utilisation and clock traces. No FPS or FPS/watt is attributed to that unrelated sensor session.
- PCGameBenchmarks (https://pcgamebenchmarks.com, https://github.com/emilioagustin83/pc-game-fps-dataset). Dedicated searchable FPS estimates tab, 1080p High across 12 reference GPUs. The data is loaded lazily and is not part of the benchmark ranking or comparison engine. The source methodology (https://pcgamebenchmarks.com/methodology) describes typical error of around 30%, or 40% for integrated graphics. Model values are not measurements.

Fixed Vercel rewrites are read-only and do not accept arbitrary upstream URLs. CSV sources are bounded by the existing 10 MB request limit. Upstream schema changes may require adapter updates. Unknown data stays null.
