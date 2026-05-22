# Development Log

## 2026-05-22

- Add provider login map + button

## 2026-05-22

- Fix map bugs add arrow key + enter on address hot search dropdown

## 2026-05-22

- Add event trigger for sqlite refresh post daily import job

## 2026-05-22

- Add full binary address->token->index pairing load into memory + hot search

## 2026-05-21

- Review staging PRs before main

## 2026-05-21

- Add automated dev PR review

## 2026-05-15 to 2026-05-21

This week focused on making ESI/address lookup faster, more reliable, and easier to operate in production.

### Search performance

- Added a deploy-time binary token index for address candidate matching.
- Moved the hot address suggestion path onto the in-memory token index so typeahead can avoid expensive database scans.
- Added startup warmup logic so the address index and database paths are ready before users hit the search flow.
- Improved search-button behavior so exact ESIID retrieval can bypass slower comparison work when an ESIID is available.
- Kept fuzzy address search separate from the token index path so fuzzy matching can still use ranking-oriented search.

### Address reliability

- Added regression coverage for address edge cases discovered during testing, including directional streets, aliases, padded house numbers, and partial address inputs.
- Improved handling for address suggestions so selecting a recommended address can populate the ESIID field for faster follow-up searches.
- Added logic to avoid stale suggestion-filled ESIIDs affecting later manual address edits.
- Added diagnostics around zero-result address searches to make production misses easier to investigate.

### Production readiness

- Added database and address-index artifact integrity checks for deployment validation.
- Improved database warmup behavior for production startup.
- Adjusted artifact loading and deployment behavior so large generated search assets can live outside git.
- Continued tuning Railway deployment behavior around startup, health checks, and persistent data.

### Product and UI

- Updated search methods and search page layout.
- Improved dropdown behavior, including click-off handling.
- Refined homepage and legal-page presentation for production launch.
- Updated README and public project materials.

### Public build log

- Added the workflow that can publish sanitized private development updates into this public devlog.

### Source commits summarized

- `2026-05-21` `901f394` Add public devlog publishing workflow
- `2026-05-21` `4b01932` Add tokenization binary file, hot searching, and warmup logic
- `2026-05-20` `505beb6` Add db warmup
- `2026-05-20` `0b77248` Add additional logic for capturing edge cases
- `2026-05-20` `b32d5e2` Fix address search and add FTS bm25 ranking
- `2026-05-20` `5cb7fc9` Update layouts
- `2026-05-20` `9f56d19` Update search methods
- `2026-05-20` `13de69f` Enable click-off of dropdowns in search
- `2026-05-20` `7140f90` Updates to ignore files, switch to non restore on start
- `2026-05-19` `0221e7f` Update readme
- `2026-05-19` `495582e` Build new
- `2026-05-15` `08a7df3` Adjust legal page, fix home page for production launch
- `2026-05-15` `ac9f304` Update search, adjust daily load scripts, add staging env in blob storage
