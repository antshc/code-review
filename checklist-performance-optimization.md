# Macro performance optimization

## Use Pagination to Efficiently Load Large Datasets

Always implement server-side pagination when returning large collections in ASP.NET Core APIs  to reduce memory usage, response size, and improve overall performance and scalability.

```
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    [HttpGet]
    public IActionResult GetUsers(int pageNumber = 1, int pageSize = 10)
    {
        var users = Enumerable.Range(1, 100).Select(i => $"User {i}");

        var pagedUsers = users
            .Skip((pageNumber - 1) * pageSize)
            .Take(pageSize);

        return Ok(pagedUsers);
    }
}
```

## Avoid retrieving all records at once

Avoid retrieving all records at once from a database table or external system and then processing them in memory. This approach can lead to high memory usage and poor performance.

**Instead of:**

```
var allUsers = await _dbContext.Users.ToListAsync();
```

**Do:**

```
var records = await _dbContext.Users
        .Skip(skip)
        .Take(take)
        .ToListAsync();
```

## Use Task Parallelization for Parallel Workloads

Use `Task.WhenAll()` to execute multiple independent asynchronous operations concurrently when their results are not dependent on one another. Be careful not to overload external systems or databases by triggering too many simultaneous operations at once. Throttle concurrency to maintain stability and prevent failures.

Instead of:

```
foreach (var x in Enumerable.Range(1, 5))
{
    var result = await GetResult(x); // Awaits sequentially
    results.Add(result);
}
```

Do:

```
var tasks = Enumerable.Range(1, 5).Select(GetResult);
var results = await Task.WhenAll(tasks);
```

Or

```
await Parallel.ForEachAsync(items, async (item, ct) =>
{
    await DoSomethingAsync(item, ct);
});
```

## Use Task Pre-Fetching to Maximize Concurrency

When you need to await multiple independent asynchronous operations, \*\*start all tasks first, then `await` **them later**, to allow them to run concurrently rather than sequentially.

Instead of:

```
return new UserProfile
{
    UserDetails = await GetUserDetailsAsync(userId),
    UserOrders = await GetUserOrdersAsync(userId)
};
```

Do:

```
var detailsTask = GetUserDetailsAsync(userId); // start both
var ordersTask = GetUserOrdersAsync(userId);

return new UserProfile
{
    UserDetails = await detailsTask,
    UserOrders = await ordersTask
};
```

## Eliminate Repeat Actions

Avoid calling the same asynchronous method multiple times when the result remains unchanged. Instead, store the result and reuse it as needed to prevent redundant execution. This simple idea can appear in many different forms throughout your code, making it easy to miss repeated calls if you're not careful.

Instead of:

```
var x = GetX(); // GetValue() called internally
var y = GetY(); // GetValue() called again

return new Result
{
    X = await x,
    Y = await y
};

async Task<int> GetX()
{
    var value = await GetValue(); // ← repeated call
    return value.X;
}
```

Do:

```
var value = await GetValue();

return new Result
{
    X = value.X,
    Y = value.Y
};
```


## Use Appropriate Caching Strategies

Use caching strategically to minimize redundant computation and external resource access. Choose the appropriate caching mechanism based on the scope and lifecycle of your data:

* **Field/Local Cache:** For short-lived or per-request expensive computations (e.g., calculating a value used multiple times in one method), store data in a local field or variable to avoid re-execution.

* **IDictionary or Concurrent Dictionary:** Use for per-instance or in-memory read-heavy scenarios like lookups that don’t need eviction or expiration.

- **IMemoryCache:** Use for caching data within a single app instance (in-memory). Ideal for data that's reused across multiple requests like configuration, metadata, or API responses.

- **IDistributedCache:** Use for multi-instance applications (e.g., in cloud or Kubernetes) where cache must persist across servers (e.g., Redis or SQL Server). Good for session data, user preferences, or shared configuration.

* **ASP.NET Core Output Caching (Response Caching):** Use to cache rendered responses based on request parameters, headers, or route. Especially useful for pages or APIs with slow backends but deterministic outputs.

  ```
  [HttpGet]
  [OutputCache(Duration = 60)]
  public IActionResult GetProductList() => Ok(_productService.GetAll());
  ```

## Cancel long-running operations when the HTTP client disconnects or the user navigates away.

**Scenario:**

A user sends a search request but quickly updates the query. The first request should be canceled to reduce backend load and latency.

When a user refreshes the page multiple times in quick succession, previously initiated requests that are no longer needed should be canceled to conserve resources and reduce backend load.

**Example:**

```
[HttpGet("search")]
public async Task<IActionResult> SearchData(CancellationToken cancellationToken)
{
    var result = await _searchService.PerformSearchAsync(cancellationToken);
    return Ok(result);
}
```

## Async All the Things

When working with asynchronous code, **you should make your methods async if they call other async methods**. This ensures that the benefits of async programming—such as non-blocking I/O, better scalability, and reduced thread usage—are fully realized.

## Avoid using `.Wait()` or `.Result`

Avoid using `.Wait()` or `.Result` on asynchronous code, as they block the calling thread and can lead to deadlocks, especially in environments with synchronization contexts (e.g., ASP.NET or UI threads). Always prefer `await` to keep the code non-blocking and responsive.

**Instead of:**

```csharp
// This blocks the thread and may cause deadlocks
var result = GetDataAsync().Result;
```

**Do:**

```csharp
// This is non-blocking and avoids deadlocks
var result = await GetDataAsync();
```

## Prefer Async Streams for Large Result Sets

* When returning large collections, use `IAsyncEnumerable<T>` to avoid loading all data at once into memory.
* Reduces memory footprint and improves UX in streaming scenarios.

**Do:**

```csharp
await foreach (var product in _repository.GetAllAsync())
{
    yield return new ProductDto(){ ... };
}

private async IAsyncEnumerable<Product> GetAllAsync()
{
    await using var context = new AppDbContext();
    await foreach (var product in context.Products.AsAsyncEnumerable())
    {
        yield return product;
    }
}
```

## Offload Heavy Tasks Using Separate HTTP Requests After Page Load

Avoid loading heavy or slow-to-fetch data (like inventory availability) during the initial HTTP response. Instead, return the main content quickly and fetch additional data with separate HTTP requests after the page has rendered.

## Offload Long-Running or Resource-Intensive Operations to a BackgroundService

Avoid executing time-consuming or computationally heavy operations—such as report generation, file processing, or batch data export—within the HTTP request pipeline. Instead, enqueue the task and process it asynchronously using a `BackgroundService`. \*\*Scenario: \*\*An admin requests invoice generation for all customers (e.g., 10,000 invoices). This involves heavy computation (PDF rendering, DB querying, cloud storage upload) and could take several minutes.

## Stay Up to Date – Use the Latest .NET Version for Performance Gains

Each new .NET release includes significant performance optimizations in areas such as garbage collection, JIT compilation, HTTP pipelines, and asynchronous I/O. Microsoft actively invests in benchmarking and tuning core libraries for faster runtime execution and lower memory usage.

## Use Proper Indexing to Speed Up Query Performance

Create and maintain indexes on columns that are frequently used in **WHERE**, **JOIN**, **ORDER BY**, or **GROUP BY** clauses to significantly reduce query execution time. While optimizing SQL query performance can be complex, creating proper indexes is a fundamental rule you should always follow when writing new queries.
