# API reference

Base URL: `https://gridprice.app`

The GridPrice API is the same one the website, the Android app and its widgets use. It is free, needs no key or sign-up, and allows requests from any origin (`Access-Control-Allow-Origin: *`), so it can be read from a browser, a server or a smart-home hub alike.

- [Conventions](#conventions)
- [`GET /v1/providers`](#get-v1providers)
- [`GET /v1/current`](#get-v1current)
- [`GET /v1/feed`](#get-v1feed)
- [`GET /v1/history`](#get-v1history)
- [`GET /v1/card/<city>.svg`](#get-v1cardcitysvg)
- [Errors](#errors)
- [Caching and fair use](#caching-and-fair-use)
- [Price levels](#price-levels)

## Conventions

Every price is a point:

```json
{ "ms": 1791430500000, "price": 14.7 }
```

| Field | Meaning |
|---|---|
| `ms` | Start of the price interval, as a UTC Unix timestamp in **milliseconds**. |
| `price` | Price for that interval in **cents per kWh**. Can be negative: wholesale prices drop below zero when there is more wind or solar than the grid can use. |

Lists of points are always sorted oldest first.

The interval length depends on the source: five minutes for most feeds, 15 minutes for ERCOT, and one hour for Ameren Illinois, which publishes a day-ahead hourly price. See [coverage](coverage.md) for every feed.

A **provider** is one price feed, identified by an id such as `comed` or `ercot-lz_houston`.

## `GET /v1/providers`

Lists every provider id.

Request:

```
https://gridprice.app/v1/providers
```

Response:

```json
["comed", "ameren-il", "ercot-lz_houston", "ercot-lz_north", "...", "miso-ms"]
```

47 ids as of October 2026. The list only grows; ids are never renamed.

## `GET /v1/current`

The most recent price for one provider.

| Parameter | Required | Example |
|---|---|---|
| `provider` | yes | `comed` |

Request:

```
https://gridprice.app/v1/current?provider=comed
```

Response:

```json
{ "ms": 1791430500000, "price": 14.7 }
```

Returns `null` if the provider has no recent readings, which only happens when an operator's feed has been down for a long time.

## `GET /v1/feed`

Roughly the last 24 hours for one provider. This is what the charts on the site and in the app draw.

| Parameter | Required | Example |
|---|---|---|
| `provider` | yes | `ercot-lz_houston` |

Request:

```
https://gridprice.app/v1/feed?provider=ercot-lz_houston
```

Response:

```json
[
  { "ms": 1791345600000, "price": 4.309 },
  { "ms": 1791346500000, "price": 4.451 }
]
```

About 288 points for a five-minute feed, 96 for ERCOT and 24 for Ameren.

## `GET /v1/history`

Every stored price between two dates.

| Parameter | Required | Example | Notes |
|---|---|---|---|
| `provider` | yes | `nyiso-nyc` | |
| `start` | yes | `20260901` | `YYYYMMDD` |
| `end` | yes | `20260930` | `YYYYMMDD`, inclusive |

Request:

```
https://gridprice.app/v1/history?provider=nyiso-nyc&start=20260901&end=20260930
```

Response:

Dates are calendar days **in the operator's own time zone**. `start=20260901&end=20260901` for `nyiso-nyc` returns midnight to midnight Eastern time on September 1.

Limits and behaviour:

- **Up to 400 days per request.** Split longer ranges into several calls.
- **History begins on July 22, 2026**, when GridPrice started keeping every reading. Earlier dates return nothing rather than an error.
- **`start` after `end`** returns an empty list.
- History is permanent. Several operators delete their own data after a couple of weeks; GridPrice keeps it.

## `GET /v1/card/<city>.svg`

A live price card as an SVG image, for READMEs, blogs and dashboards. See [live price cards](cards.md) for the full guide.

```
https://gridprice.app/v1/card/chicago.svg
https://gridprice.app/v1/card/houston.svg?theme=light
https://gridprice.app/v1/card/ercot-lz_west.svg
```

## Errors

Errors come back as JSON with a 4xx status:

| Status | Body | Cause |
|---|---|---|
| 400 | `{"error":"unknown provider"}` | `provider` missing or not in `/v1/providers` |
| 400 | `{"error":"start/end must be YYYYMMDD"}` | `start` or `end` missing, or in another format such as `2026-09-01` |
| 404 | `{"error":"not found"}` | No such endpoint |

The card endpoint never errors. An unknown city or a feed that is down still returns a valid image saying so, so a README never shows a broken picture.

## Caching and fair use

| Endpoint | `Cache-Control` |
|---|---|
| `/v1/current`, `/v1/feed` | `public, max-age=60` |
| `/v1/history` | `public, max-age=300` |
| `/v1/card/...` | `private, max-age=300` (60 seconds when stale or offline) |

Prices only change every five minutes, so polling more often than that gains nothing. Please keep automated polling to **once every five minutes per provider** and cache on your side. There is no hard rate limit today; keeping it that way depends on everyone being reasonable.

## Price levels

The site, the app and the cards colour prices the same way:

| Level | Range (¢/kWh) | Colour |
|---|---|---|
| Cheap | below 4 | green |
| Normal | 4 to 8 | olive |
| Elevated | 8 to 14 | orange |
| High | 14 to 28 | deep orange |
| Very high | 28 and above | red |

These are guides, not tariff thresholds. A price that is "High" in Chicago in January can be routine in Texas in August.
