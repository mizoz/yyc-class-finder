# YYC Class Finder

A small web app that helps Calgarians find upcoming City of Calgary recreation programs without scrolling through a large open-data table.

**Live site:** https://city-picks.vercel.app

## Why

The City of Calgary publishes its recreation program listings as open data, but the raw dataset is hard to browse. YYC Class Finder starts with the practical questions a parent, student or adult learner would ask (how old, how much, which day, what kind of activity) and returns a short list of matching classes, each linked back to the official source.

## Features

- Filter active programs by age, maximum price, day of the week and keyword
- Searches course names, program sections and venue names
- Shows dates, times, price, age range, venue and a short description for each class
- Only returns classes dated today or later (Calgary time)
- Save classes to a short list in the browser
- Links back to the official City of Calgary dataset for verification
- Server-side API route with 15-minute caching, so the city API is not hit on every search
- No API key or account needed

## How it works

The Next.js route `apps/web/app/api/programs/route.ts` queries the City of Calgary Socrata API:

- Dataset: Recreation Program Listings
- Endpoint: `https://data.calgary.ca/resource/q9hh-gfbx.json`
- Source page: https://data.calgary.ca/Recreation-and-Culture/Recreation-Program-Listings/q9hh-gfbx

Filters are translated into SoQL `$where`, `$order` and `$limit` parameters (user input is escaped), and the response is trimmed to the fields the interface needs.

Program data belongs to the City of Calgary and is used under its open-data licence. Always confirm details and register through the City's official channels.

## Quick start

Requirements: Node.js 20+ and npm 10+.

```bash
npm install
npm run dev        # http://localhost:3000
```

Other scripts:

```bash
npm run build      # production build
npm run start      # serve the production build
npm run typecheck  # TypeScript checks
```

## Project structure

```txt
apps/web     Next.js app (UI and the /api/programs route)
vercel.json  Vercel build settings
```

## Deployment

`vercel.json` builds the app from the repository root and serves `apps/web/.next`. No environment variables are required.

## Tech stack

- Next.js 14 (App Router) and React 18
- TypeScript
- Plain CSS
- City of Calgary Open Data (Socrata API)
- Vercel

## License

MIT. See [LICENSE](LICENSE).
