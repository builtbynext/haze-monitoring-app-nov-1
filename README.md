# Haze Watch

Static single-page app. No build step, no dependencies, no API keys.

- Haze data (24-hour PSI, PM2.5, PM10): National Environment Agency via data.gov.sg, Singapore only.
- Weather for every city: Open-Meteo.

The browser calls both APIs directly, so the page only shows live numbers when it is served over http(s)
or opened as a local file. If a feed is unreachable it shows an error and never substitutes sample values.

## Deploy to Vercel

1. Unzip, then from this folder run `npx vercel` (preview) or `npx vercel --prod`.
   When asked, accept the defaults. Framework preset: Other. Build command and output directory: leave empty.
2. Or drag the folder into https://vercel.com/new.

`vercel.json` sets clean URLs, security headers and a Content-Security-Policy that allows only
`api-open.data.gov.sg`, `api.open-meteo.com` and Google Fonts. If you add another data source,
add its host to `connect-src`.

## Notes

- data.gov.sg rate-limits unauthenticated requests. The page makes one NEA request per load and every 10 minutes.
  If you expect heavy traffic, request a free API key from data.gov.sg and proxy the call through a Vercel function.
- Open-Meteo's free tier is for non-commercial use. Check their terms for commercial deployments.
