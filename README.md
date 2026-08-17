# QA Portfolio — Steam Store Search

Manual testing of the search functionality of the Steam store (`store.steampowered.com/search`): query handling, result output, filters and sorting.

A full manual testing cycle on a live public product: test plan → checklist → test cases → defect reports.

Companion project: [steam-web-api-postman](https://github.com/TokitoKaito/steam-web-api-postman) — API-level testing of the same product with Postman: 6 requests, 26 assertions.

## Findings

Four defects were found. Three of them share a single trigger but are separate defects: they affect different environments and require different fixes.

| ID | Title | Severity | Priority | Affects |
|---|---|---|---|---|
| [BUG-001](bug-reports/bug-report-001.md) | Store search returns a server error for a query consisting only of an odd number of double quotes | Medium | Medium | Client + browsers |
| [BUG-002](bug-reports/bug-report-002.md) | Site header is duplicated inside the search results area on a server error | Low | Medium | Browsers only |
| [BUG-003](bug-reports/bug-report-003.md) | After a server error, search on the results page stops working and is not restored by refreshing | Medium | Medium | Client + browsers |
| [BUG-004](bug-reports/bug-report-004.md) | Price filter "Безкоштовно" [free] returns a paid game in the results | Low | Medium | Client + browsers |

## Artifacts

| Document | Contents |
|---|---|
| [Test plan](test-plan.md) | Objective, scope, out of scope, test approach, environment, deliverables |
| [Checklist](checklist.md) | 25 checks covering every area in scope, with results |
| [Test cases](test-cases.md) | 14 test cases with steps, test data and expected results |
| [Bug reports](bug-reports/) | 4 defect reports with steps to reproduce and screenshots |

## Scope

**In scope:** the search box and navigation to the results page; relevance of results to the query; the price, language, tag and OS filters; the 7 sorting options; loading further results on scroll; the contents of a result card.

**Out of scope:** the search-suggestions dropdown; the game page itself (used only as a source of reference data when verifying filters); purchase and login; the remaining 8 filters; the order of results, because no expected ordering is defined anywhere and there is nothing to compare against.

## Environment

Steam client 1784778118 and browsers Opera GX 133.0.5932.81, Microsoft Edge 150.0.4078.105; Windows 11 Home (build 22631); 2560 x 1440 physical, Windows scaling 150%, browser viewport 1707 x 960 CSS pixels, page zoom 100%.

The account interface language is Ukrainian, so UI element names are quoted in the original Ukrainian with an English gloss in square brackets. The screenshots show the same Ukrainian interface.

## Notes on method

Two observations are recorded as open questions rather than as passes or failures, because the expected behaviour is not defined anywhere and there was nothing to compare the observed result against:

- **Partial-word search:** `witcher` finds the game, `witc` does not, `wit` returns unrelated products. The matching rule is unknown, so the check is marked **Blocked** rather than guessed at.
- **Language filter and DLC:** DLC that do not list the selected language are not removed from the results. Whether that is intended is a product decision.

On a real product both would be clarified with the requirements owner. Recording them honestly is more useful than inventing an expected result.

## Author

Daniil, steepdan2003@gmail.com
