# Template
## Summary
Short explanation of what was changed and why.

## Why This Change Was Needed
- What problem does it solve?
- What risks does it mitigate?
- What alternative approaches did you consider and why were they rejected?

## Implementation Details
- Key technical details.
- Architecture / design decisions.
- Any important trade-offs.

## Test Results
### Automated Tests
- [ ] Unit tests added/updated  
- [ ] Integration tests added/updated  
**Summary of outcomes:**  
- Test suite passed  
- Coverage change (optional): +X%

### Manual / Scenario Tests
| Scenario | Expected Result | Actual Result | Status |
|---------|-----------------|---------------|--------|
|  |  |  |  |

**Performance / Benchmark Data (if applicable):**
- Before:  
- After:

## Screenshots / Logs (Optional)
Attach screenshots, logs, diagrams if it helps reviewers.

## Breaking Changes
- Yes/No  
If yes → describe migration steps.

## Checklist
- [ ] Code is self-documented  
- [ ] Tests written or updated  
- [ ] No confidential data in logs  
- [ ] Meets acceptance criteria  
- [ ] Added reasoning and test results to PR description

# Example
## Summary
Implemented real-time inventory validation during the Add-to-Cart operation.  
If the warehouse reports that an item is no longer available, the cart now prevents overselling and displays a clear message to the user.

## Why This Change Was Needed
- Previously, inventory checks occurred only during checkout, causing users to reach payment with unavailable items in the cart.
- This created a poor UX and generated support tickets.
- Adding early validation reduces cart abandonment and prevents order failures.
- Alternative approach considered: validating only on page load. Rejected because stock changes too frequently in high-traffic scenarios.

## Implementation Details
- Added `IInventoryService` call inside `CartService.AddItemAsync()`.
- Introduced a lightweight caching layer with a 5-second TTL to avoid calling warehouse API on every request.
- Added retry logic for warehouse timeouts (max 2, exponential backoff).
- New error message UI component: “Item currently out of stock. Please try again later.”
- Updated domain logic to ensure cart state remains consistent if inventory check fails.

## Test Results
### Automated Tests
- Updated 8 existing unit tests.
- Added 6 new tests covering:
  - Successful add-to-cart when stock is available.
  - Out-of-stock scenario.
  - Warehouse timeout → retry → success.
  - Warehouse timeout → retry exhausted → fail gracefully.
  - Correct cache invalidation.
  - UI message rendering.

**All automated tests passed.**  
Coverage for the Cart module increased from **78% → 89%**.

### Manual / Scenario Tests
| Scenario | Expected Result | Actual Result | Status |
|---------|-----------------|---------------|--------|
| Item available | Added to cart | Works as expected | ✔️ |
| Item becomes out of stock during browsing | Cart shows “Out of Stock” error | Works as expected | ✔️ |
| Warehouse API slow (2–5s delay) | Retry succeeds without blocking UI | Verified | ✔️ |
| Warehouse permanently unavailable | Cart displays fallback message; no crash | Verified | ✔️ |
| High concurrency (100 parallel add-to-cart requests) | No overselling or race conditions | Verified | ✔️ |

### Performance / Load
- **Before:** Avg add-to-cart latency: 240 ms  
- **After:** Avg add-to-cart latency: 180 ms (−25%)  
- Warehouse API calls reduced by ~40% due to short-term caching.

## Breaking Changes
None.

## Checklist
- [x] Added reasoning explaining the change  
- [x] Included automated + manual test results  
- [x] Updated tests  
- [x] No sensitive data logged  
- [x] Meets e-commerce UX and business rules  


