# Live price cards

A GridPrice card is an SVG image of the live electricity price in one city. It is drawn by the price server each time it is requested, so dropping one into a page gives that page a price that keeps itself up to date.

<p align="center">
  <img src="https://gridprice.app/v1/card/austin.svg" width="460" alt="Live electricity price in Austin">
  <img src="https://gridprice.app/v1/card/austin.svg?theme=light" width="460" alt="Live electricity price in Austin, light theme">
</p>

## Use one

The URL is:

```
https://gridprice.app/v1/card/<city>.svg
```

### In Markdown (GitHub, GitLab, most docs sites)

```markdown
[![Electricity price in Austin](https://gridprice.app/v1/card/austin.svg)](https://gridprice.app)
```

For a page with a light background, add `?theme=light` to the image URL. On GitHub you can also serve both and let the reader's theme pick, the way the [project page](../README.md) does at the top.

## Cities

| City | Slug | Feed |
|---|---|---|
| Chicago | `chicago` | ComEd hourly pricing |
| Houston | `houston` | ERCOT, CenterPoint |
| Dallas–Fort Worth | `dallas` | ERCOT, Oncor |
| Austin | `austin` | ERCOT, Austin Energy |
| San Antonio | `san-antonio` | ERCOT, CPS Energy |
| New York City | `new-york` | NYISO, Con Edison |
| Long Island | `long-island` | NYISO, PSEG Long Island |
| Buffalo | `buffalo` | NYISO West |
| Albany | `albany` | NYISO Capital |
| Los Angeles | `los-angeles` | CAISO SP15 |
| San Diego | `san-diego` | CAISO SP15 |
| San Francisco | `san-francisco` | CAISO NP15 |
| Boston | `boston` | ISO-NE, Eversource |
| Hartford | `hartford` | ISO-NE Connecticut |
| Providence | `providence` | ISO-NE Rhode Island |
| Seattle | `seattle` | Western EIM |
| Portland | `portland` | Western EIM |
| Phoenix | `phoenix` | Western EIM |
| Las Vegas | `las-vegas` | Western EIM |
| Salt Lake City | `salt-lake-city` | Western EIM |
| Boise | `boise` | Western EIM |
| Albuquerque | `albuquerque` | Western EIM |
| Minneapolis | `minneapolis` | MISO |
| Milwaukee | `milwaukee` | MISO |
| Des Moines | `des-moines` | MISO |
| Detroit | `detroit` | MISO |
| Indianapolis | `indianapolis` | MISO |
| St. Louis | `st-louis` | MISO |
| New Orleans | `new-orleans` | MISO |
| Oklahoma City | `oklahoma-city` | SPP |
| Kansas City | `kansas-city` | SPP |
| Omaha | `omaha` | SPP |

`/v1/card.svg` with no city is Chicago.

Any provider id from [`/v1/providers`](api.md#get-v1providers) works in place of a city, for zones without a named city: `/v1/card/ercot-lz_west.svg`, `/v1/card/miso-ar.svg`.

## Options

| Query | Effect |
|---|---|
| `?theme=light` | White card for light backgrounds. Dark is the default. |

## What the card shows

- The current price in cents per kWh, coloured by [level](api.md#price-levels).
- The level itself: Cheap, Normal, Elevated, High or Very high.
- How the price compares with the average of the last 24 hours, as a percentage.
- A sparkline of the last 24 hours with the average marked as a dashed line.
- When it was updated, in the city's own time zone.
- A status pill:
  - **LIVE** when the reading is current.
  - **STALE** when the newest reading is more than 90 minutes old, which means the operator's feed has stalled. The card then says "Last price" instead of "Updated".
  - **OFFLINE** when there is no recent data for that feed at all, or the city is unknown.

The card always returns HTTP 200 with a valid image, so a page never shows a broken picture.

## How fresh is it?

The card is served with `Cache-Control: private, max-age=300`, five minutes, which is one price interval. GitHub's image proxy honours that, so a README shows a price at most a few minutes old. Stale and offline cards are cached for only 60 seconds, so they recover quickly once the feed returns.

`private` is deliberate: it stops Cloudflare's edge, which caches anything ending in `.svg` for hours by default, from holding on to an old card.

## Accessibility

Every card carries an SVG `<title>` and `<desc>` that a screen reader announces in full, for example: "The live electricity price in Chicago (ComEd hourly pricing) is 14.7 cents per kWh, rated high. That is 81% above the 24-hour average of 8.1 cents." Still give the `<img>` its own `alt` text.

## Safety

The SVG contains no scripts, no external fonts and no linked images, and every value written into it is XML-escaped. That is what lets it render through GitHub's image proxy, and it is safe to embed anywhere that accepts images.
