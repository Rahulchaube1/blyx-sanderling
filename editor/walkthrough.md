## Carry cache age across a local storage interval

Returns [mode, current age, ticks until mode changes]. Mode 0 serves fresh, 1 serves under explicit stale grace, and 2 requires validation. The host parses and enforces other cache directives. Invalid arguments and nonfinite results return an empty vector.

1. Open an empty file named `sanderling-demo.blyx`.
2. Type `blyx-sanderling-demo` and select **Sanderling — runnable example**. You can also use **Snippets: Fill File with Snippet**.
3. Choose **Blyx: Run File** from the command palette. Change an argument near the end of `fn main()` to try another input.

Expected output

```text
1
13
3
```

[Work through the example in the browser](https://www.blyx-lang.space/play?example=package-sanderling)
