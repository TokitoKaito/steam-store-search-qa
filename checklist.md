# Checklist — Steam Store Search

Object under test: the search results page — `store.steampowered.com/search`  
Environment: see the [test plan](test-plan.md)

**Result values:** `Pass` — works as expected; `Fail` — defect, report linked in the comment; `Blocked` — cannot be verified.

| # | Check | Result | Comment |
|---|---|---|---|
| 1 | Search by word (witcher) | Pass |  |
| 2 | Empty search | Pass |  |
| 3 | Very long query | Pass |  |
| 4 | Search using digits | Pass |  |
| 5 | Search using emoji | Pass |  |
| 6 | WITCHER and witcher return the same results | Pass |  |
| 7 | Non-existent word returns nothing | Pass |  |
| 8 | Search using special characters | Fail | Double quote breaks the search. See [BUG-001](bug-reports/bug-report-001.md), [BUG-002](bug-reports/bug-report-002.md), [BUG-003](bug-reports/bug-report-003.md). All other special characters tested return "Результатів: 0" [0 results]. |
| 9 | Search in different scripts (Cyrillic, CJK) | Pass |  |
| 10 | Element layout in a reduced window (browser) | Pass | On narrowing the window the top header row collapses into a burger menu — standard responsive behaviour, not a defect. The collapse occurs at a window width of 909 CSS pixels. |
| 11 | Behaviour in a reduced window (Steam client) | Pass | The client window cannot be narrowed below its minimum size. |
| 12 | Search in Cyrillic: "відьмак" | Pass | Ukrainian-localised account: a game is found by the user locale if its title is localised. |
| 13 | Partial-word query | Blocked | Expected behaviour is not defined: `witcher` finds the game, `witc` does not, `wit` returns other products. The rule is unknown and there is nothing to compare against. Question for the analyst. |
| 14 | Leading and trailing spaces in the query | Pass |  |
| 15 | Price filter "до 40 ₴" [up to 40 UAH] limits results to products no more expensive than 40 UAH | Pass | Boundary is inclusive: a product priced exactly 40 UAH appears in the results. |
| 16 | Price filter "Будь-яка ціна" [any price] does not limit results by price | Pass |  |
| 17 | Price filter "Безкоштовно" [free] returns only free products | Fail | A paid Battlefield title with a visible price appears under the filter. See [BUG-004](bug-reports/bug-report-004.md). |
| 18 | Language filter narrows results to products supporting the selected language | Pass | DLC without the specified languages are not filtered out. Expected behaviour for DLC is not defined — question for the analyst. |
| 19 | Tag filter narrows results to products carrying the selected tag | Pass |  |
| 20 | OS filter narrows results to products supporting the selected OS | Pass |  |
| 21 | Each of the 7 sorting options changes the order of results | Pass |  |
| 22 | A filter and a sorting option applied together do not conflict | Pass |  |
| 23 | The next batch of results loads when scrolling down | Pass |  |
| 24 | Result card contents: image, title, platform, release date, rating, price | Pass |  |
| 25 | Navigating to the results page via the "Пошук" [Search] button | Pass | Observed while reproducing BUG-003: the button submits the query and opens the results. |

**Totals:** 22 Pass, 2 Fail, 1 Blocked.
