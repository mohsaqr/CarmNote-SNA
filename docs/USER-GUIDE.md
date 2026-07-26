# CarmNote SNA User Guide

[Documentation index](./INDEX.md) ·
[Downloads and versions](./DOWNLOADS-AND-VERSIONS.md) ·
[Menus and interface](./MENUS-AND-INTERFACE.md) ·
[Cell reference](./CELL-REFERENCE.md)

This guide explains how to download CarmNote SNA, prepare an edge list, build
a network, run analyses, export results, and save a portable notebook.
CarmNote SNA is a self-contained HTML application: it requires no
installation, account, server, or internet connection after download.

## Download and open CarmNote SNA

[Download the latest recommended build](../index.html?raw=1), keep the
`.html` extension, and open it in a current web browser.

If GitHub shows the HTML source instead of downloading the file, use the
**Download raw file** button. Do not copy the displayed source into a new
file.

## Prepare an edge list

CarmNote SNA accepts CSV or TSV with one edge per row:

```csv
From,To,Weight,Group
Alice,Bob,3,Class-A
Bob,Carla,1,Class-A
Carla,Alice,2,Class-A
Alice,David,1,Class-B
```

`From` and `To` are required. `Weight` is optional; if it is omitted, each row
is treated as one edge. An additional grouping column can be selected with
**Split by** to build one network per group. Node identifiers can be names,
codes, or numbers, but use the same spelling consistently.

Use a header row and save spreadsheet data as **CSV UTF-8** or TSV. Excel
files (`.xlsx` and `.xls`) are not read directly. Comma, tab, semicolon, and
pipe delimiters are supported.

## Load and build the network

1. Drop the data file on the opening panel, click **Upload CSV / TSV**, or use
   **File → Load Data**.
2. Review the preview and confirm the detected **From**, **To**, and optional
   **Weight** columns.
3. Choose **Directed: Yes** when `A → B` differs from `B → A`; choose **No**
   when ties are symmetric.
4. Click **Rebuild**, or add/use the **Network** cell, review its optional
   **Split by** setting, and click **Build Network**.

Check the displayed node and edge counts before interpreting results.

## Add and run analyses

A useful first workflow is:

1. **Visualize** to inspect the graph and adjust its layout.
2. **Properties** for graph-level structure.
3. **Centrality** to rank nodes using the selected measures.
4. **Community** to detect cohesive groups.
5. **Cliques** to enumerate fully connected subsets.
6. **Text** to document decisions and interpretations beside the results.

Each analysis cell can choose its source network when the notebook contains
multiple build cells. Configure the cell and use its run button; the play
button in the header reruns all cells in notebook order.

## Export results

Result tables can be copied or downloaded as CSV, TSV, JSON, or Markdown.
Network figures can be downloaded as SVG, PNG, or JPEG where offered. Use
**File → HTML Report**, **Word (.doc)**, or **Print / PDF** for a
notebook-level output.

## Save, resume, and share

Click **Save** or press <kbd>Ctrl</kbd>/<kbd>Cmd</kbd>+<kbd>S</kbd> to
download a self-contained `.html` file with the data, settings, cells, and
results embedded. This downloaded file is the portable copy to archive or
share.

CarmNote also autosaves a working copy in the current browser, but browser
storage is not a substitute for the downloaded file. Use **Save** whenever
you need a durable copy on disk.

The lower-left lock control provides four sharing states:

- **Editable** — the notebook can be changed normally.
- **Read-only** — a soft presentation state that can be returned to editable.
- **Locked** — a frozen copy; editing requires **Duplicate to editable copy**.
- **Sealed** — locked with a SHA-256 fingerprint that flags later changes.

Set the intended state first, then click **Save** to download that version.
Keep an editable saved copy before locking or sealing important work.

## Troubleshooting

- **The browser shows code:** return to GitHub and use **Download raw file**.
- **Excel will not load:** export the sheet as CSV UTF-8 or TSV.
- **The graph direction is wrong:** change **Directed** and rebuild.
- **The node or edge count is unexpected:** verify the From/To/Weight mapping,
  spelling of node IDs, blank rows, and whether repeated edges are intentional.
- **Analysis cells use the wrong graph:** change the cell's source-network
  selector, then rerun it.
- **A new release restores an unsuitable browser state:** choose
  **File → Reset notebook storage & reload**. This clears CarmNote SNA's
  browser library but does not delete saved `.html` files.
