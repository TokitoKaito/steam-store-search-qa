# Test Plan — Steam Store Search

## Objective

Verify that Steam store search works correctly: query handling, result output, filtering (price, language, tags, OS) and sorting.

## Glossary

- **Search results page** — the full results page with filters and sorting (`store.steampowered.com/search`). The object under test.
- **Search suggestions** — the dropdown list of up to 4 suggestions under the store search box. Out of scope.

> The account interface language is Ukrainian. UI element names are quoted in the original Ukrainian, with an English gloss in square brackets.

## Scope

- search box: entering a query, navigating to the results page (Enter / the "Пошук" [Search] button);
- results: relevance of the results to the query;
- filters: price, language, tags ("позначки"), OS — 4 of 12, the most significant;
- sorting: 7 options;
- loading further results on scroll;
- result card: presence of elements (image, title, platform, release date, rating, price).

## Out of scope

- search suggestions under the store search box;
- the game page itself (everything after clicking a card) — not tested, but used as a source of reference data when verifying filters;
- purchase, login;
- the remaining 8 filters;
- the order of results (title match versus description match): no expected order is defined anywhere, so there is nothing to compare against.

## Test approach

Functional and negative testing. Techniques: boundary value analysis (price, query length), equivalence partitioning (tags, OS, language), UI state checks (loading, empty results, behaviour in a reduced window).

## Environment

| Item | Value |
|---|---|
| Browsers | Opera GX 133.0.5932.81, Microsoft Edge 150.0.4078.105 |
| Steam client | version 1784778118 |
| OS | Windows 11 Home (build 22631) |
| Screen | 2560 x 1440 physical, Windows scaling 150% |
| Browser viewport | 1707 x 960 CSS pixels, page zoom 100% |
| Account interface language | Ukrainian |

Language filters do not affect the results of the checks — verified both with a language filter enabled and with none applied.

## Deliverables

- a checklist covering all areas in scope — [checklist.md](checklist.md);
- 14 test cases for the key checks — [test-cases.md](test-cases.md);
- bug reports for the defects found — [bug-reports/](bug-reports/).
