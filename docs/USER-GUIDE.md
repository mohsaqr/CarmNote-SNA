# CarmNote SNA User Guide

[Documentation index](./INDEX.md) ·
[Downloads and versions](./DOWNLOADS-AND-VERSIONS.md) ·
[Menus and interface](./MENUS-AND-INTERFACE.md) ·
[Cell reference](./CELL-REFERENCE.md)

This guide describes how CarmNote SNA is downloaded, how an edge list is
prepared, and how a network is built, analysed, exported, and saved as a
portable notebook. CarmNote SNA is a self-contained HTML application: it
requires no installation, account, server, or internet connection after
download.

## Downloading and opening CarmNote SNA

The [latest recommended build](../index.html?raw=1) is downloaded with its
`.html` extension kept and is opened in a current web browser.

If GitHub shows the HTML source instead of downloading the file, the
**Download raw file** button retrieves the file itself. Copying the displayed
source into a new file is not a substitute.

## Edge-list preparation

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
codes, or numbers, but their spelling must be consistent.

Files require a header row; spreadsheet data are saved as **CSV UTF-8** or
TSV. Excel files (`.xlsx` and `.xls`) are not read directly. Comma, tab,
semicolon, and pipe delimiters are supported.

## Loading and building the network

1. The data file is dropped on the opening panel, uploaded with
   **Upload CSV / TSV**, or loaded with **File → Load Data**.
2. The preview is reviewed and the detected **From**, **To**, and optional
   **Weight** columns are confirmed.
3. **Directed: Yes** applies when `A → B` differs from `B → A`; **No** applies
   when ties are symmetric.
4. **Rebuild** is selected; alternatively, the **Network** cell is added or
   used, its optional **Split by** setting reviewed, and **Build Network**
   selected.

The displayed node and edge counts are checked before results are
interpreted.

## Adding and running analyses

A typical first workflow is:

1. **Visualize** for inspecting the graph and adjusting its layout.
2. **Properties** for graph-level structure.
3. **Centrality** for ranking nodes with the selected measures.
4. **Community** for detecting cohesive groups.
5. **Cliques** for enumerating fully connected subsets.
6. **Text** for documenting decisions and interpretations beside the results.

Each analysis cell can choose its source network when the notebook contains
multiple build cells. Each cell is configured and then executed with its run
button; the play button in the header reruns all cells in notebook order.

## Exporting results

Result tables can be copied or downloaded as CSV, TSV, JSON, or Markdown.
Network figures can be downloaded as SVG, PNG, or JPEG where offered.
**File → HTML Report**, **Word (.doc)**, and **Print / PDF** produce
notebook-level output.

## Saving, resuming, and sharing

**Save** or <kbd>Ctrl</kbd>/<kbd>Cmd</kbd>+<kbd>S</kbd> downloads a
self-contained `.html` file with the data, settings, cells, and results
embedded. This downloaded file is the portable copy to archive or share.

CarmNote also autosaves a working copy in the current browser, but browser
storage is not a substitute for the downloaded file. **Save** is the command
that produces a durable copy on disk.

The lower-left lock control provides four sharing states:

- **Editable** — the notebook can be changed normally.
- **Read-only** — a soft presentation state that can be returned to editable.
- **Locked** — a frozen copy; editing requires **Duplicate to editable copy**.
- **Sealed** — locked with a SHA-256 fingerprint that flags later changes.

The intended state is set first, and **Save** then downloads that version.
An editable saved copy should be kept before important work is locked or
sealed.

## Troubleshooting

- **The browser shows code:** the file is downloaded again from GitHub with
  **Download raw file**.
- **Excel will not load:** the sheet is exported as CSV UTF-8 or TSV.
- **The graph direction is wrong:** **Directed** is changed and the network
  rebuilt.
- **The node or edge count is unexpected:** the From/To/Weight mapping, the
  spelling of node IDs, blank rows, and whether repeated edges are intentional
  are verified.
- **Analysis cells use the wrong graph:** the cell's source-network selector
  is changed and the cell rerun.
- **A new release restores an unsuitable browser state:**
  **File → Reset notebook storage & reload** clears CarmNote SNA's browser
  library but does not delete saved `.html` files.
