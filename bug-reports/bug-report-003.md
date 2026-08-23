# BUG-003 — After a failed search request, search on the results page stops working and is not restored by refreshing the page

| | |
|---|---|
| **Severity** | Medium |
| **Priority** | Medium |
| **Reproducibility** | 5 out of 5 attempts in the browsers, 5 out of 5 attempts in the Steam client. |

**Preconditions:** a query that makes the search request fail (see BUG-001)

**Environment:** Steam client (version 1784778118) and browsers Opera GX 133.0.5932.81, Microsoft Edge 150.0.4078.105; Windows 11 Home (build 22631); screen resolution 2560 x 1440 physical, Windows scaling 150%, browser viewport 1707 x 960 CSS pixels, page zoom 100%. Reproduces both in the client and in the browsers. Account interface language: Ukrainian.

## Steps to Reproduce

1. Open the Steam store (in a browser — store.steampowered.com; in the client — the "Крамниця" [Store] tab)
2. Go to the full search results page (in a browser — store.steampowered.com/search)
3. In the search field, enter a single double quote: " — and press Enter. The request fails and an error page is displayed (BUG-001)
4. In the same field, enter a valid query, for example witcher, and press Enter
5. Refresh the page (F5)

## Expected

Step 4 — the new query is processed normally and its results are displayed;
step 5 — the search page opens in a working state.

## Actual

Step 4 — the new query is not processed: the same error page as in step 3 is returned;
step 5 — refreshing does not restore operation. The query containing the quote is stored in the page URL (term=%22), so after refreshing the error page opens, and it has no search field at all. Operation is restored only by opening the search page again from scratch.

## Severity and priority rationale

- **Severity: Medium** — a key store function becomes unavailable, and the standard recovery action (refreshing the page) does not help. A workaround exists — open the search page again.
- **Priority: Medium** — the defect is only reachable through BUG-001, but it concerns error-response handling in general and will appear on any other failed response on this page.

## Notes

- the behaviour of the page after the defect occurs is unstable, and no stable recovery condition could be identified. Some subsequent actions restore search, others do not:
  - searching via the "Пошук" [Search] button sometimes works, but stops after the next press of Enter
  - clicking outside the input field and back into it before pressing Enter: the query is processed
  - a query that returns no results (for example, "афаумймйфм") clears the error
- observed on the same failed response as the one described in BUG-001. In browsers, BUG-002 additionally occurs.
