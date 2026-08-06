# Business Critical Systems — Status Page

A static status page (`index.html`) that shows the health of Business Critical
Systems. It embeds a live, read-only view of the source tracker spreadsheet
hosted on SharePoint, so the page updates automatically as owners update
system statuses — no redeploy needed.

## How it works

- `index.html` renders a header, a legend for the three status states
  (Working, Working with Issues, Not Working), and two panels:
  - **Tier 1 & 2 Progress** — an embedded chart from the tracker.
  - **Systems** — an embedded table view of the tracker.
- Both panels are SharePoint "embedview" iframes pointed at the same
  source document (`sourcedoc`), just scoped to a different `Item`.
- The page is a single static HTML file with no build step, so it can be
  served from GitHub Pages, or any static file host.

## Updating a system's status

Status is **not** edited on this page. Click "Open the tracker to edit" in
the toolbar (or use the tracker link below) to update a system's status
directly in the source spreadsheet:

https://uao365.sharepoint.com/:x:/s/ServiceManagement/IQDI4OS8OkV4R7riVSLSJ1tqAWH6EQhpYTLsbVEFaNCCAC8

Changes made there are picked up automatically the next time the embedded
iframes refresh.

## Updating the embed source

If the tracker document is moved or replaced, update both `src` URLs in
`index.html` (inside the `<iframe>` elements) with the new `sourcedoc`
GUID and `Item` reference.

## Local preview

Since this is a static file, open `index.html` directly in a browser, or
serve the directory with any static file server, e.g.:

```
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.
