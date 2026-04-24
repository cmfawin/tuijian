# Repository Guidelines

## Project Structure & Module Organization

This repository is a static dashboard project for recommendation-performance analysis.

- `千人千面数据看板.html`: main single-page dashboard. Contains layout, Vue state, and ECharts rendering.
- `data.js`: monthly metric source consumed by the dashboard. Keep only `全站` plus recommendation modules; exclude `搜索结果` and `推荐加权`.
- `events.js`: timeline/event source for module trend charts.
- `26.3数据.xlsx`, `推荐事件表.xlsx`: latest raw Excel inputs.
- `推荐模块事件表说明.md`, `千人千面数据看板.md`: reference docs for field meaning and display rules.
- `backup.html`: fallback snapshot before major edits.

## Build, Test, and Development Commands

There is no build pipeline or package manager in this repo. Work directly on the static files.

- `python3 -m http.server 8000`
  Serve the directory locally for browser testing.
- `node --check events.js`
  Validate `events.js` syntax after edits.
- `python3 - <<'PY' ... PY`
  Use short pandas scripts to inspect `.xlsx` inputs before updating `data.js` or `events.js`.

## Coding Style & Naming Conventions

- Use 4-space indentation in HTML, CSS, and JavaScript.
- Preserve the current plain-browser stack: Vue 3 CDN, ECharts CDN, Tailwind CDN.
- Keep data payloads as `window.dashboardSourceData` and `window.moduleEventSourceData`.
- Use descriptive camelCase for JS helpers and state, for example `getModuleEventPanel` and `detailMetricOptions`.
- Keep module names and field labels exactly aligned with source spreadsheets.

## Testing Guidelines

There is no automated test suite yet. Minimum validation for every change:

- Check JavaScript syntax with `node --check`.
- Verify the dashboard loads in a browser.
- Confirm latest month, tooltip content, and event overlays render without overflow.
- When updating data, spot-check 2-3 modules against the Excel source.

## Commit & Pull Request Guidelines

This folder is not currently a Git repository, so no local commit history is available. If moved into Git:

- Use short imperative commit messages, for example: `update march dashboard data` or `fix event tooltip wrapping`.
- In PRs, include:
  screenshots for UI changes,
  the source Excel file used,
  the affected modules/months,
  and a brief validation note.

## Data Update Notes

- Update `data.js` from the latest monthly cross-table.
- Update `events.js` only from event rows that match modules shown in the dashboard.
- Treat `至今` as the current chart end month when rendering timeline overlays.
