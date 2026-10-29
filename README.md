# Google Play Scraping Benchmark

AIMultiple benchmark of Bright Data, SerpApi, Nimble and Zyte on Google Play app product pages, measuring success rate, completion time and the number of parsed metadata fields returned.

> [Read the benchmark on AIMultiple](https://aimultiple.com/google-play-scrapers)

## Workload

The test set holds 1,000 real Google Play product page URLs from keyword searches across app categories. Each URL went once to each provider, for 4,000 requests. Bright Data (Google Play Store, Collect by URL API) and SerpApi (Google Play Product API) returned JSON. Nimble and Zyte returned browser-rendered HTML.

Requests ran one at a time, 2 seconds apart, with a 30-second backoff on HTTP 429, a 300-second submission timeout and a 600-second execution timeout.

- Success: HTTP 200 to 399 or a clean 404, no timeout or error, and extractable data. JSON needed one of title, rating, developer or number_of_reviews; HTML needed a match on at least one CSS selector listed before the run.
- Completion time: wall-clock, from request sent to final response, including queueing and polling.

## Benchmark results

Metadata fields and completion time for the four providers in the results (the article includes only providers with a success rate above 90%):

| Provider | Output | Metadata fields | Completion time (s) |
| --- | --- | ---: | ---: |
| Bright Data | JSON | 26 | 8 |
| SerpApi | JSON | 11 | 1 |
| Zyte | HTML | 0 | 4 |
| Nimble | HTML | 0 | 9 |

SerpApi responded fastest but returned 11 fields to Bright Data's 26. Nimble and Zyte return no parsed fields, so their HTML still needs a parser.

## Scope

Results cover sequential requests only, not concurrent load. Google Play pages and provider APIs change, and the HTML results depend on each provider's rendering settings.

## Ownership

The benchmark implementation was developed for AIMultiple and belongs to AIMultiple. This repository contains a documentation summary. Source code and benchmark datasets are not distributed here.
