# Google Analytics 4 MCP (GA4)

A **Google Analytics 4 MCP (GA4) Model Context Protocol (MCP) server built by Typenode**, wrapping Google's official Analytics Data and Admin APIs. Its **19 read-only tools** let AI assistants such as Claude and ChatGPT retrieve your data and answer questions in plain language.

**Runs on Typenode.** The repository contains tool contracts, permission requirements and usage recipes. The implementation runs on Typenode and is not included here. You need your own Typenode Workspace and Google connection; there is no standalone npm or Python server here.

**[Get this template](https://typenode.ai/templates/google-analytics-mcp)** · **[Setup instructions](docs/setup.md)** · **[Copy-paste prompts](prompts/getting-started.md)**

> Current interface reference: the maintainer installations have live evidence. Independent customer installation of the latest published snapshot still needs verification. These JSON contracts are documentation, not executable workflows. See [verification](docs/verification.md).

## What can you do with it?

Built for SEO and marketing managers who want to ask questions about their own authorised data. The tools retrieve native reports and useful preset datasets; your AI client performs the comparison, interpretation and explanation.

| Question | Retrieval tool | Evidence supplied |
|---|---|---|
| Which landing pages receive Google organic sessions? | `get_ga4_organic_landing_pages` | Retrieve session traffic and native engagement metrics. |
| What recorded outcomes accompany landing-page traffic? | `get_ga4_landing_page_outcomes` | Retrieve separate traffic context, selected event counts and optional native registered event-specific rates. |
| Which channels drive sessions? | `get_ga4_channel_acquisition` | Inspect session acquisition by channel, source/medium or campaign. |
| How were users first acquired? | `get_ga4_first_user_acquisition` | Keep first-user acquisition separate from subsequent session acquisition. |
| How do comparable reporting periods differ? | `get_ga4_period_datasets` | Retrieve the same report recipe for each period; comparison belongs to the AI client. |
| Where do users stop progressing through a recorded event sequence? | `query_ga4_funnel` | Retrieve native ordered funnel aggregates using explicit steps and sequence constraints. |

See [more task recipes](prompts/marketing-analysis.md), including limitations that should remain visible in an answer.

## Available tools

The names and descriptions below match the saved server bindings. The linked JSON files document each tool's input/output contract. No Google configuration write tools are included.

### Properties and measurement configuration

| Tool | What it retrieves |
|---|---|
| [`list_ga4_properties`](tools/list_ga4_properties.json) | Discover accessible Google Analytics accounts and properties as native account summaries. Page size counts account summaries, each of which can contain multiple property summaries. |
| [`get_ga4_property`](tools/get_ga4_property.json) | Get one GA4 property’s native configuration, including available reporting timezone and currency. This does not change settings. |
| [`list_ga4_data_streams`](tools/list_ga4_data_streams.json) | List one GA4 property’s web and app streams, including available website URLs. Stream discovery helps select a site scope; it does not prove an exact GSC property match. |
| [`list_ga4_key_events`](tools/list_ga4_key_events.json) | List configured GA4 key events and native configuration. Current registration does not establish when an event was tracked or its historical counts. |
### Report discovery and primitives

| Tool | What it retrieves |
|---|---|
| [`get_ga4_report_metadata`](tools/get_ga4_report_metadata.json) | Discover standard, custom and comparison metadata for a GA4 property. Returns a bounded, optionally filtered catalog; comparison queries are outside v1. |
| [`check_ga4_report_compatibility`](tools/check_ga4_report_compatibility.json) | Check Core report dimensions, metrics and filters; optionally list compatible additions. This endpoint does not validate funnel or realtime reports and does not guarantee data access or nonempty results. |
| [`query_ga4_report`](tools/query_ga4_report.json) | Retrieve one bounded page of a GA4 Core report with native headers, numeric strings, restrictions and optional aggregates. Core compatibility checking is enabled by default and adds one read; pagination is not a snapshot. |
| [`get_ga4_report_totals`](tools/get_ga4_report_totals.json) | Retrieve dimensionless native GA4 totals for explicit dates and filters. Never sum users across detail rows or average their rates; dimension filters still define the selected population. |
| [`get_ga4_report_time_series`](tools/get_ga4_report_time_series.json) | Retrieve native GA4 metrics grouped by day, week, month or hour in the property reporting timezone. Missing intervals remain missing. |
### Marketing retrieval presets

| Tool | What it retrieves |
|---|---|
| [`get_ga4_organic_landing_pages`](tools/get_ga4_organic_landing_pages.json) | Retrieve landing-page traffic and engagement for Google organic sessions by default, or explicitly all organic search. Preserve native page identifiers; URL alignment with GSC belongs to the client. |
| [`get_ga4_landing_page_outcomes`](tools/get_ga4_landing_page_outcomes.json) | Retrieve separate landing-page traffic context, selected event counts and optional native event-specific key-event rates. At most three report datasets; event filtering never narrows the context or rate denominator. |
| [`get_ga4_channel_acquisition`](tools/get_ga4_channel_acquisition.json) | Retrieve session acquisition by channel, source/medium or campaign with selected native metrics. This differs from first-user acquisition and event-scoped attribution. |
| [`get_ga4_first_user_acquisition`](tools/get_ga4_first_user_acquisition.json) | Retrieve native first-user acquisition groups and compatible metrics. Describes original acquisition rather than the source of subsequent sessions. |
| [`get_ga4_event_performance`](tools/get_ga4_event_performance.json) | Retrieve observed event names and native counts/user metrics for explicit dates and optional event selection. Event occurrences are not unique converting sessions or configured key-event discovery. |
| [`get_ga4_audience_breakdown`](tools/get_ga4_audience_breakdown.json) | Retrieve native metrics by country or device category with explicit traffic scope. Returns recorded aggregates without evaluating audience quality. |
### Dataset bundles and funnels

| Tool | What it retrieves |
|---|---|
| [`get_ga4_performance_overview`](tools/get_ga4_performance_overview.json) | Retrieve independent native totals, daily trend and landing-page datasets, optionally session channels. At most four report datasets; no calculated summary or cross-dataset join. |
| [`get_ga4_period_datasets`](tools/get_ga4_period_datasets.json) | Retrieve the same Core report recipe for up to six named periods. Returns independent datasets and continuations without calculating differences or matching absent rows. |
| [`get_ga4_property_datasets`](tools/get_ga4_property_datasets.json) | Retrieve the same Core report recipe for up to six GA4 properties. Preserve each property’s scope, result and failure; never combine users or silently normalize currencies. |
| [`query_ga4_funnel`](tools/query_ga4_funnel.json) | Retrieve ordered native GA4 funnel aggregates with explicit step, entry and sequence constraints. Uses the Alpha API; capped reports have no offset continuation and require a narrower request. |

## Quick start

1. Prepare a Typenode Workspace, a Google Cloud OAuth application and access to your reporting properties.
2. Enable the required Google APIs and connect Google in your chosen Typenode Environment with the read-only scope below.
3. Activate your copy of the hosted MCP template through Typenode: **[https://typenode.ai/templates/google-analytics-mcp](https://typenode.ai/templates/google-analytics-mcp)**. The [setup guide](docs/setup.md) documents prerequisites and connection checks.
4. Obtain your own Environment-specific MCP endpoint, add it to your AI client and complete Typenode consent.
5. Ask: **“List the Google Analytics properties I can access.”** Then select a returned property and make a dated report request.

## Requirements and permissions

| Requirement | Why it is needed |
|---|---|
| Typenode account | Hosts and executes your copy of the Workflows and MCP server; normal account/billing prerequisites apply. |
| Customer-owned Google Cloud project and OAuth client | The tested custom OAuth setup authenticates API reads. |
| Enabled APIs | Google Analytics Data API, Google Analytics Admin API. |
| Google OAuth scope | `https://www.googleapis.com/auth/analytics.readonly`. |
| Google property access | The consenting account must be authorised for the selected property and method; an OAuth scope does not grant property access. |
| Compatible AI client | Supports Typenode's authenticated remote MCP endpoint and can discover/invoke its tools. |

Credential values belong in secure Typenode configuration. Property identifiers and date ranges are call arguments, not hardcoded installation defaults. Google renewal and client-to-Typenode renewal are distinct authentication boundaries; [setup](docs/setup.md) explains both.

The MIT licence covers the files in this repository, not the hosted implementation or service access. Typenode hosting, AI-client subscriptions and Google's quotas are separate. Check [provider quota guidance](https://developers.google.com/analytics/devguides/reporting/data/v1/quotas) and current Typenode account terms; this package does not promise free runtime usage.

## Example request

Ask your AI client to retrieve a report for your selected property and dates. Underneath, it can call `query_ga4_report` with arguments like these:

```json
{
  "ga4_property_id": "123456789",
  "start_date": "2026-09-01",
  "end_date": "2026-09-30",
  "dimensions": ["landingPagePlusQueryString"],
  "metrics": ["sessions", "engagementRate"]
}
```

The property and dates above are invented examples. Replace them with your own selection. The result includes typed native evidence, effective request, coverage notes and request accounting. Report results expose continuation where supported; errors provide a documented correction.

Browse [requests for every tool](examples/tool-calls.json), a [complete representative request](examples/sample.request.json), its [synthetic response](examples/sample.response.json), and [example interpretation guidance](examples/README.md). These examples demonstrate interface shapes and do not claim observed results for a real business.

## How it works

Your AI client invokes a named MCP tool. Typenode validates the request, performs bounded official Google API reads using your connected Credential, and returns a structured result. Presets reduce repetitive request construction; bundles return independent datasets and their outcomes.

The server adds request validation, bounded output, pagination, explicit source/error evidence and retrieval presets. Format checks omitted from advertised input schemas still run in preflight; other schema constraints can reject at admission. It does not author business recommendations, join the sibling servers' datasets or reconstruct unavailable metrics. Query results can change as Google data changes; pagination is not a snapshot.

## Limitations

GA4 reports recorded and sometimes modeled aggregates, not complete raw user histories. Missing instrumentation cannot be reconstructed. Preserve native restrictions and metadata; missing measurements remain unknown.

Session acquisition, first-user acquisition and event-scoped attribution describe different populations. Event counts are not unique converting sessions; users and rates should not be summed across detail rows. Current key-event configuration is not proof of historical tracking. Funnels use the Alpha API and provide no offset continuation when capped.

Empty results do not prove absence of real-world activity. Preserve dates, filters, reporting populations, source metadata and unresolved evidence. A partially returned bundle is not an entirely successful report; continue a selected dataset through its documented primitive without reacquiring all siblings.

See [verification and pending release checks](docs/verification.md) for the distinction between live evidence, synthetic checks and unverified setup/authentication guarantees.

## Frequently asked questions

### Can I use this with Claude or ChatGPT?

The tools are designed for clients that support Typenode's authenticated remote MCP connection. Add your own endpoint and complete the client-to-Typenode consent flow. Check current client support and refresh discovery after catalog changes; a healthy connection badge alone does not prove tool access.

### Does it change my Google account or reporting configuration?

No. The tools perform read-only API operations using `https://www.googleapis.com/auth/analytics.readonly`. Some reporting methods use HTTP POST to retrieve data; that does not make them configuration writes.

### Do I need a Google Cloud project?

Yes for the tested customer-owned custom OAuth setup. Enable the relevant APIs and register an OAuth application. You also need Google account permission on the properties you query. See [Google's access guidance](https://developers.google.com/analytics/devguides/reporting/data/v1/quickstart).

### Does cloning the GitHub repository start the MCP server?

No. These files document the interface of a hosted server. Obtain the template at [https://typenode.ai/templates/google-analytics-mcp](https://typenode.ai/templates/google-analytics-mcp) and connect your own account; the contracts are not executable Workflows. See [setup](docs/setup.md) for prerequisites and current activation status.

### Is there an official Google Analytics MCP server?

Yes. Google documents its own [read-only Analytics MCP server](https://developers.google.com/analytics/devguides/MCP). This repository is an independent Typenode template with named marketing retrieval presets, bounded dataset bundles and a complementary GSC package. Choose according to your hosting and workflow needs; this is not Google's official server.

### Can I combine GSC and GA4?

Yes: connect both sibling servers and let the AI client orchestrate their reads. GSC describes search visibility and clicks; GA4 describes recorded traffic and outcomes. Align dates, property scope and URL identities explicitly. These aggregates do not establish query-to-person signup attribution. See [combined recipes](prompts/with-gsc.md).

### Where do the data and credentials go?

Credentials are configured in your Typenode Workspace/Environment. Retrieved reporting data passes through Typenode execution and to the connected AI client. Review both services' data-handling terms for your account. This repository contains no live credential values or private execution captures.

## What is in this repository?

- [manifest.json](manifest.json): reference metadata, requirements and links to the tool contracts.
- [tools/](tools/): names, descriptions, input/output schemas and reference safety annotations. Host propagation of annotations is not certified. No implementation code or Workflow graphs.
- [docs/setup.md](docs/setup.md): account/credential requirements, hosted activation status and first-read checks.
- [prompts/](prompts/): copy-paste task recipes, not protocol-registered prompt resources.
- [examples/](examples/): illustrative calls and source-shaped responses.

Use the contracts to inspect supported arguments, plan client integrations and understand response shapes. Editing a contract file does not change the hosted tool. Workflow customisation and publication, where supported, happen within Typenode.

## Related templates and support

The complementary **Google Search Console MCP** covers the other side of search visibility and recorded on-site activity. Use the combined recipe linked above to understand which questions need both.

For an implementation issue, include the tool name, package version, sanitised arguments and error/coverage evidence in a repository issue. Keep tokens, OAuth client secrets, consent URLs and private datasets out of public reports.

Created by Typenode. This template is not affiliated with or endorsed by Google. The contracts and documentation in this repository are provided under the [MIT licence](LICENSE); the hosted implementation is excluded from this repository and licence grant. Third-party names and marks belong to their respective owners.
