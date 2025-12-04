## General
- Does the implementation meet the requirement / spec / user story?
- Does the implementation do not change the not related existing system behaviour?
- Can this solution be simplified?
- Is the code testable?
- Is a framework, API, library, or service used that should not be used?
- Could an additional framework, API, library, or service improve the solution?
- Is the code at the right abstraction level?
- Is the code modular enough?
- Can a better solution be found in terms of maintainability, readability, performance, or security?
- Does similar functionality already exist in the codebase? If yes, why isn’t it reused?
- Are there any best practices, design patterns or language-specific patterns that could substantially improve this code?
- Does this code adhere to OOP, and the SOLID, KISS, YAGNI, Design patterns?
- Can you think of any use case in which the code does not behave as intended?
- Can you think of any inputs or external events that could break the code?
- Were updates to documentation, configuration, or readme files made as required by this change?
- Are there any potential impacts on other parts of the system or backward compatibility?
- Do the existing tests reasonably cover the code change (unit/integration/system tests)?
- Are there some test cases, input or edge cases that should be tested in addition?

## General code
- Does this change add unwanted compile-time or run-time dependencies?
- Is the logic idempotent where it should be (retries, event handling, commands)?
- Are retry policies applied where needed (external services, transient faults)?
- Are there any obvious race conditions (shared state, static fields, caches)?
- Are edge cases covered (nulls, empty collections, limits, timeouts)?
- Is cyclomatic complexity reasonable (no 300-line methods, deeply nested ifs)?
- Are IDisposable/IAsyncDisposable instances properly disposed (using / await using)?
- Are input parameters validated where needed (public APIs, boundaries)?
- Are time, time zone, and culture issues handled correctly (DateTimeOffset, DateTimeKind, CultureInfo)?
- Is the visibility correct (internal/private vs public)? Anything public that can be internal?
- Are data contracts / DTOs clean and not leaking domain or internal entities?
- Any hard-coded secrets, keys, passwords, connection strings? (They should be removed.)

## Error Handling & Logging
- Are exceptions handled at the right boundaries (not swallowed, not over-caught)?
- Are we not using exceptions for control flow?
- Are error messages clear and useful for troubleshooting?
- Are logs written at appropriate levels (Debug/Info/Warn/Error/Critical)?
- Is PII or sensitive data avoided in logs?
- Are custom exception types meaningful and used where appropriate?

## Async, Concurrency & I/O
- Are async methods truly async end-to-end (no .Result/.Wait() blocking)?
- Is async/await used correctly (no async void except event handlers)?
- Are I/O operations (DB, HTTP, file, storage) using async APIs?
- Are concurrency primitives appropriate (lock, SemaphoreSlim, ConcurrentDictionary, etc.)?
- Is there a risk of deadlocks (sync-over-async, locks ordering)?
- Are cancellation tokens supported and properly passed through?
- Is parallelism bounded (no unbounded Task.Run, Parallel.ForEach without limits)?

## async await best practices
- await every task
- do not use "async void MethodName(){}" handle safe fire and forget to catch exceptions. note: Check async/await best practices nuget package


## Performance & Memory
- Any obvious performance issues on hot paths (unnecessary allocations, reflection, LINQ in tight loops)?
- Are large collections handled carefully (paging, streaming, chunking)?
- Is caching used where appropriate, and invalidation rules clearly defined?
- Are IEnumerable vs IQueryable used correctly (no unintended client vs server evaluation)?
- Are value types vs reference types chosen sensibly for high-frequency operations?
- Are Span<T>, pooling, or other low-level optimizations used only where justified and safe?

## Resources
- [Code review checklist](https://github.com/mgreiler/code-review-checklist)
- [async/await guidance](https://github.com/davidfowl/AspNetCoreDiagnosticScenarios/blob/master/AsyncGuidance.md#concurrentdictionarygetoradd) 
