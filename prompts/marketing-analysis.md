# GA4 marketing questions

## Inspect organic landing pages

> Use get_ga4_organic_landing_pages for [property ID] and [dates]. Keep its Google organic session scope explicit. Show native sessions, engaged sessions and engagement rate, with pagination and native reporting restrictions. Don't sum users across page rows or average rates.

## Inspect recorded outcomes

> First retrieve observed event names and current key-event configuration separately. For my chosen event [event name], use get_ga4_landing_page_outcomes for [dates]. Keep traffic context separate from selected event counts. Request native event-specific rates only where available and preserve their documented denominator. Don't equate event occurrences with unique converting sessions.

## Compare acquisition scopes

> Retrieve get_ga4_channel_acquisition and get_ga4_first_user_acquisition for [property ID] and [dates]. Explain what each native dataset measures. Don't treat first-user acquisition as the source of later sessions or as event-scoped attribution.

## Build a compatible custom report

> Discover metadata and check compatibility for [dimensions] and [metrics]. Then retrieve the report for [dates] with query_ga4_report. Preserve numeric strings, native headers and restrictions. Compatibility does not guarantee available data or property access.

## Compare periods or properties

> Use get_ga4_period_datasets for [periods], or get_ga4_property_datasets for [property IDs], with the same report recipe. Preserve each property's timezone, scope and currency. Do not add users across properties or silently normalise currencies.

## Inspect an ordered funnel

> Use query_ga4_funnel for [property ID] and [dates] with these observed event steps: [steps]. State whether entry is open or closed and what order, direct-follow and timing constraints apply. Use native aggregates; don't infer ordered progression from unordered event totals. If capped, narrow the request because no offset cursor exists.

## Inspect audience breakdowns

> For [property ID] and [dates], use get_ga4_audience_breakdown by [country or device]. Keep traffic scope explicit. Describe native aggregates and reporting restrictions without scoring audience quality.
