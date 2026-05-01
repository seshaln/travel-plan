# travel-plan

Personal trip plans. One repo = one site via GitHub Pages, Jekyll renders README.md.

- Repo: https://github.com/seshaln/travel-plan
- Pages: https://seshaln.github.io/travel-plan/
- Source: `main` branch, root `/`

## Structure

- `README.md` — current active trip plan (rendered as the site)
- `<trip>.md` — draft/source text for a specific trip (e.g. `azores.md`). README is built from it with route, links, photos
- Past trips: the original README was Gran Canaria January 2026, see git history (commit `1a31976`)

## README conventions

- TOC with anchors at top
- Days as H1 (`# 2 мая, ...`)
- Day subsections: "Логика дня", morning/lunch/afternoon/dinner, "Что бронировать"
- Schedules as markdown tables with columns **Время | План | Стоимость**
- Places as clickable Google Maps links: `[Name](https://maps.google.com/?q=...)`
- Photos hotlinked from Wikimedia Commons
- Trip content is in Russian; CLAUDE.md and meta is in English

## Wikimedia thumb URL — important

Wikimedia only allows these sizes in `/thumb/.../{N}px-...`:

```
20, 40, 60, 120, 250, 330, 500, 960, 1280, 1920, 3840
```

Any other size → HTTP 400 ("Use thumbnail steps listed on https://w.wiki/GHai").

Current pick: **500px** (compact for README). The original file (without `/thumb/...`) also works but is heavy.

Thumb URL pattern:
```
https://upload.wikimedia.org/wikipedia/commons/thumb/<a>/<ab>/<file>.jpg/500px-<file>.jpg
```

How to get a URL: either `og:image` from a Wikipedia article (gives thumb), or the `commons.wikimedia.org/wiki/File:...` page (gives original).

## Workflow to add a trip

1. Drop a draft `<place>.md` with the route in free form
2. Replace README.md: same tables + add maps links + Wikimedia photos (500px)
3. Update TOC
4. Commit + push → Pages rebuilds in ~30s

## Commands

- Check Pages build: `gh api repos/seshaln/travel-plan/pages/builds/latest --jq '{status, error}'`
- Verify thumb URL before commit: `curl -sI -o /dev/null -w "%{http_code}\n" "<url>"` (expect 200)
