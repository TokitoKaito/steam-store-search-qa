# Test Cases — Steam Store Search

Object under test: the search results page — `store.steampowered.com/search`  
Environment: see the [test plan](test-plan.md)

**Case priority:** `High` — included in the smoke run before a release; `Medium` — included in the full regression run; `Low` — a rare scenario, run as needed.

UI element names are quoted in the original Ukrainian, with an English gloss in square brackets.

---

## TC-001 — Searching by the name of an existing game returns that game in the results

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** search query — witcher; expected game — The Witcher 3: Wild Hunt

**Steps:**

1. Place the cursor in the "Введіть критерій пошуку чи позначку" [Enter a search term or tag] field
2. Enter the query witcher
3. Press Enter
4. Review the first 10 result cards

**Expected result:** the result list is not empty and no zero-results message is shown; "The Witcher 3: Wild Hunt" is present among the first 10 cards; card titles contain the substring witcher, case-insensitive

**Priority:** High

---

## TC-002 — A non-existent query returns an empty result set

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** search query — srgwdfwrg

**Steps:**

1. Place the cursor in the "Введіть критерій пошуку чи позначку" [Enter a search term or tag] field
2. Enter the query srgwdfwrg
3. Press Enter
4. Inspect the results area

**Expected result:** "Результатів вашого пошуку: 0" [Your search returned 0 results] is displayed; no product cards appear in the results; no error message is shown

**Priority:** Low

---

## TC-003 — Character case in the query does not affect the results

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** queries — witcher and WITCHER; comparison depth — the first 10 cards

**Steps:**

1. Enter the query witcher and press Enter
2. Record the titles of the first 10 cards and their order
3. Enter the query WITCHER and press Enter
4. Record the titles of the first 10 cards and their order
5. Compare both result sets

**Expected result:** both result sets contain the same cards in the same order; the total number of results found is identical

**Priority:** Medium

---

## TC-004 — A query consisting only of double quotes is handled without a server error

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** queries — " (one quote) and """ (three quotes); control query — witcher

**Steps:**

1. Enter a single double quote in the search field: "
2. Press Enter
3. Inspect the results area
4. Enter the query witcher in the same field and press Enter
5. Repeat steps 1-4 for the three-quote query: """

**Expected result:** no server error message is displayed; "Результатів вашого пошуку: 0" [Your search returned 0 results] is shown, as it is for the other special characters; the search field remains operable and the control query in step 4 is processed normally

**Priority:** Low

**Related defect:** BUG-001, BUG-003 (the case does not pass on the current build)

---

## TC-005 — Price filter "до 40 ₴" [up to 40 UAH] limits the results to products no more expensive than 40 UAH

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** filter threshold — 40 UAH; check depth — the first 15 cards

**Steps:**

1. In the "Уточнити за ціною" [Refine by price] block, set the slider to the 40 UAH mark
2. Wait for the results to refresh
3. Review the prices on the first 15 cards

**Expected result:** the final price (discounted, where a discount applies) on every card reviewed does not exceed 40 UAH; the boundary is inclusive — a product priced exactly 40 UAH counts as passing the filter; no cards priced above the threshold appear in the results

**Priority:** High

---

## TC-006 — Price filter "Безкоштовно" [free] limits the results to free products

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** filter value — "Безкоштовно"; check depth — the first 15 cards

**Steps:**

1. In the "Уточнити за ціною" [Refine by price] block, set the slider to the "Безкоштовно" mark
2. Wait for the results to refresh
3. Review the first 15 cards

**Expected result:** every card reviewed shows "Безкоштовно" instead of a price; no cards with a numeric price or a discount appear in the results

**Priority:** High

**Related defect:** BUG-004 (the case does not pass on the current build)

---

## TC-007 — The language filter limits the results to products supporting the selected language

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** filter "Уточнити за мовою" [Refine by language], value — "Фінська" [Finnish]; check depth — the first 5 cards; games only, DLC excluded

**Steps:**

1. In the "Уточнити за мовою" block, select "Фінська"
2. Wait for the results to refresh
3. Open the card of the first product in the results
4. In the supported-languages block on the product page, look for Finnish
5. Return to the results and repeat steps 3-4 for the remaining four cards

**Expected result:** Finnish is present in the list of supported languages on the page of each of the five products checked

**Priority:** Medium

---

## TC-008 — The tag filter limits the results to products carrying the selected tag

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** filter "Уточнити за позначкою" [Refine by tag], value — "Стратегія" [Strategy]; check depth — the first 5 cards

**Steps:**

1. In the "Уточнити за позначкою" block, select "Стратегія"
2. Wait for the results to refresh
3. Open the card of the first product in the results
4. Expand the full tag list by clicking "+" next to the popular tags
5. Look for the "Стратегія" tag
6. Return to the results and repeat steps 3-5 for the remaining four cards

**Expected result:** the "Стратегія" tag is present in the tag list on the page of each of the five products checked

**Priority:** Medium

---

## TC-009 — The OS filter limits the results to products supporting the selected system

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** filter "Уточнити за ОС" [Refine by OS], value — macOS; check depth — the first 5 cards

**Steps:**

1. In the "Уточнити за ОС" block, select macOS
2. Wait for the results to refresh
3. Review the platform icons under the title on the first 5 cards

**Expected result:** the macOS icon is present on every card reviewed; no cards without this icon appear in the results

**Priority:** High

---

## TC-010 — Sorting by "за датою випуску" [release date] orders the results from newest to oldest

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** sorting value — "за датою випуску"; check depth — the first 10 cards; released products only

**Steps:**

1. In the "Упорядкувати" [Sort by] list (default "за доречністю" [relevance]), select "за датою випуску"
2. Wait for the results to refresh
3. Review the release dates on the first 10 cards

**Expected result:** the cards are ordered by descending release date — the date of each following card is not later than the date of the preceding one across the whole range reviewed

**Priority:** Medium

---

## TC-011 — Sorting by "за найнижч. ціною" [lowest price] orders the results by ascending price

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** sorting value — "за найнижч. ціною"; check depth — the first 5 cards

**Steps:**

1. In the "Упорядкувати" [Sort by] list (default "за доречністю" [relevance]), select "за найнижч. ціною"
2. Wait for the results to refresh
3. Review the prices on the first 5 cards

**Expected result:** the final price of each following card is not lower than the price of the preceding one across the whole range reviewed; free products ("Безкоштовно") [free] appear at the start of the list

**Priority:** Medium

---

## TC-012 — Sorting by "за назвою" [title] orders the results alphabetically in ascending order

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** sorting value — "за назвою"; check depth — the first 10 cards

**Steps:**

1. In the "Упорядкувати" [Sort by] list (default "за доречністю" [relevance]), select "за назвою"
2. Wait for the results to refresh
3. Review the titles of the first 10 cards

**Expected result:** the titles are in non-descending order — the title of each following card does not precede the title of the preceding one in alphabetical comparison

**Note:** the ordering rule for titles beginning with digits or special characters relative to titles beginning with letters is not defined anywhere, so such pairs are not verified by this case

**Priority:** Low

---

## TC-013 — Scrolling the page down loads the next batch of results

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** the search results page with no filters applied

**Steps:**

1. Record the title of the last card in the current list
2. Scroll the page to the end of the result list
3. Wait for loading to complete

**Expected result:** the "Завантаження подальшого вмісту..." [Loading further content...] indicator is displayed; within a few seconds new cards appear below the recorded card; cards previously shown do not disappear from the list

**Priority:** High

---

## TC-014 — A filter and a sorting option applied at the same time do not conflict

**Preconditions:** store.steampowered.com/search is open, no filters applied

**Test data:** filter "Уточнити за ОС" [Refine by OS], value — macOS; sorting value — "за датою випуску" [release date]; check depth — the first 10 cards

**Steps:**

1. In the "Уточнити за ОС" block, select macOS
2. In the "Упорядкувати" [Sort by] list, select "за датою випуску"
3. Wait for the results to refresh
4. Review the platform icons and release dates on the first 10 cards

**Expected result:** the macOS icon is present on every card reviewed; at the same time the cards are ordered by descending release date — the date of each following card is not later than the date of the preceding one

**Priority:** Medium

