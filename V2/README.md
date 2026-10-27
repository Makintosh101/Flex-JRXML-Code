# V2 Proposal Templates

The six current originals were moved unchanged into `../orginal/`, including
their uncommitted edits. The unrelated tour-label and v0.1 files were left alone.

## Upload to Flex

Create separate custom reports for testing; do not overwrite the originals.
Upload all five V2 subreports first, then the V2 proposal:

| File | Internal JRXML report name |
| --- | --- |
| BE Smart Title Page V2.jrxml | V2 Smart Title Page |
| BE Smart Cover Letter V2.jrxml | V2 Smart Cover Letter |
| BE Smart Quote Summary V2.jrxml | V2 Smart Quote Summary |
| BE Smart Quote Itemised V2.jrxml | V2 Smart Quote |
| BE Smart Terms & Conditions V2.jrxml | V2 Smart Terms & Conditions |
| A Proposal V2.jrxml | V2 Smart Proposal |

Keep these internal names unchanged. The proposal selects subreports by exact
internal name, not by the custom report's display name or uploaded filename.
The V2 prefix also avoids matching the originals' Smart report-name lookups.
Upload all five subreports even if some sections will be switched off.
Configure the proposal's Flex parameters/options the same way as the original.

## Changes

- Exclude deleted and cancelled quotes from the itemised selection and standalone
  itemised report.
- Exclude quotes beneath a deleted or cancelled ancestor from itemised pages,
  summary rows, summary totals, and Terms & Conditions totals.
- Check six ancestor levels, matching the existing hierarchy depth.
- Check summary totals ancestry independently of its subfolder inclusion joins.
- Load only V2 subreports, and return the actual title-page report ID.
- Preserve existing layouts, formatting, financial calculations, and print options.
  Cover-letter and title-page changes are limited to internal report names.

Cancellation follows the existing status-name convention: `%Cancel%`. Confirm
that all relevant quote and folder cancellation statuses match this pattern.
Quotes without a matching status record are excluded, consistent with the
existing summary cancellation filter.

## Flex Test Checklist

Use a test project containing an active control quote alongside excluded quotes.
Verify summary rows, summary totals, itemised pages, and contract totals together.

| Case | Expected quote inclusion |
| --- | --- |
| Pencilled quote in active folders | Included |
| Deleted quote | Excluded |
| Cancelled quote | Excluded |
| Pencilled quote in a deleted Job Folder | Excluded |
| Pencilled quote in a cancelled Job Folder | Excluded |
| Active immediate folder inside a deleted/cancelled ancestor | Excluded |
| Multiple active sibling folders | Active quotes remain included |
| Standalone V2 itemised report for an excluded quote | No quote pages |

Repeat with subfolder inclusion enabled/disabled and the paper sizes you use.
Also test a project with no eligible quotes: the master report still uses its
existing no-data behavior, so it may produce no proposal pages.

Local checks cover XML parsing, SQL predicate fixtures, and V2 subreport lookup
isolation. Full MySQL query execution, JasperReports compilation, and PDF
rendering must be checked in Flex; they have not been validated locally.