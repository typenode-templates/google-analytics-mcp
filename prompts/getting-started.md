# Getting started with Google Analytics 4 MCP (GA4)

These are copy-paste usage recipes, not protocol-registered MCP prompts. Connect your own server first. Choose an accessible property from discovery and replace bracketed values with your selections. Use explicit calendar dates for reproducible comparisons.

## Discover accessible properties

> List the Google Analytics properties I can access. If there are more pages, continue until the accessible list is complete. Show the exact property identifiers returned by the tools.

Expected first tool: `list_ga4_properties`. For GA4, account-summary page sizes count account summaries, not individual properties. For GSC, keep Domain and URL-prefix identifiers intact.

## Make a first report

> Use [selected property] for [start date] through [end date]. Retrieve Google organic landing-page sessions, engaged sessions and engagement rate. Show the source scope, freshness/coverage notes and whether more data remains.

## Inspect before concluding

> Explain what the tools actually returned and what remains unknown. Keep empty or absent measurements distinct from zero. If a result is partial, show the next safe retrieval step before making a broad conclusion.

## Continue a report safely

> Continue this dataset using its next cursor and the same effective request and page size. If this is a bundle, resume only the selected dataset with the documented primitive rather than rerunning all siblings. State whether the source boundary was reached; do not claim the API contains every real-world event or query.

Expected report primitive: `query_ga4_report`. Native funnels have no offset continuation. A cursor is a continuation mechanism, not an authorization credential or a data snapshot.
