# CarmNote SNA Menus and Interface

[Documentation index](./INDEX.md) ·
[Downloads and versions](./DOWNLOADS-AND-VERSIONS.md) ·
[User guide](./USER-GUIDE.md) · [Cell reference](./CELL-REFERENCE.md)

This reference follows the interface from top to bottom. Cell-specific
controls are documented separately in the
[Cell reference](./CELL-REFERENCE.md).

## Header

### CarmNote and version badge

Identify the notebook type, release version, and compiled build. The filename
and in-app version should agree.

### File menu

#### New Notebook

Creates a blank workspace. Save the current notebook first if a durable copy
is required.

#### Load Data

Opens a CSV/TSV file picker. The file should contain an edge list or data
suitable for a Co-occurrence cell.

#### Save

Downloads the current notebook as a self-contained `.html` file containing
data, graphs, settings, cells, and results.

#### Publish

Downloads a presentation-oriented read-only copy. Keep an editable saved copy
before publishing.

#### Copy All

Copies notebook content and results, subject to browser clipboard
permissions.

#### Word (.doc)

Downloads a Word-compatible document.

#### HTML Report

Downloads a report-oriented HTML export. It is not the same as the editable
portable notebook produced by **Save**.

#### Print / PDF

Opens the browser print dialog. Choose a PDF printer for a static PDF.

#### Create Assignment

Creates an assignment-oriented notebook workflow in which selected content
can be distributed for completion and submission. Keep an unrestricted
editable copy before creating an assignment.

#### Clear All

Removes active data, graphs, and cells from the current notebook.

#### Reset notebook storage & reload

Clears CarmNote SNA's browser-persisted workspace and reloads a clean notebook.
Use this if stale or incompatible state is being restored. Downloaded `.html`
files are not deleted.

### Cell buttons

Each button adds a new cell:

| Button | Purpose |
|---|---|
| **Generate** | Create a synthetic benchmark graph |
| **Co-occurrence** | Build a network from items co-occurring within transactions or groups |
| **Network** | Build an SNA graph from an edge list |
| **Visualize** | Draw a selected source graph |
| **Properties** | Compute structural graph properties and distributions |
| **Centrality** | Compute node-importance measures |
| **Community** | Detect cohesive node groups |
| **Cliques** | Find fully connected node subsets |
| **Text** | Add formatted narrative documentation |
| **Code** | Run advanced JavaScript against the notebook state |

See the [Cell reference](./CELL-REFERENCE.md) for every cell.

### Run All

The play icon reruns all unlocked executable cells in notebook order.
Generated, co-occurrence, and edge-list build cells should occur before cells
that consume their graphs.

### Save

Downloads the portable self-contained notebook. The keyboard shortcut is
<kbd>Ctrl</kbd>/<kbd>Cmd</kbd>+<kbd>S</kbd>.

### Lock All

Locks or unlocks all executable cells. Locked cells retain their settings and
cached results and are not rerun accidentally.

### Print

Opens the browser print flow for paper or PDF output.

## Opening panel

### Upload CSV / TSV

Loads an edge-list file. Expected roles are:

- **From/Source** — origin node;
- **To/Target** — destination node;
- **Weight** — optional tie weight.

### Generate Random Network

Creates a quick synthetic graph for exploration without loading data.

## Data panel

After loading a file, the data panel shows the filename, number of edges and
nodes, column badges, an initial preview, and summary metrics.

### From

Selects the source-node column.

### To

Selects the target-node column.

### Weight

Selects an optional numeric weight. Choose none for an unweighted edge list.

### Directed

- **Yes** — `A → B` is distinct from `B → A`.
- **No** — ties are symmetric.

### Rebuild

Recreates the active graph after a mapping or directedness change.

### Compute summary metrics

For very large graphs, expensive summary metrics are deferred. This button
runs them on demand.

### Add-cell strip

Offers context-sensitive shortcuts for adding build, visualization, analysis,
text, and code cells below the data panel.

## Source network and scope

Build cells register their graphs. Analysis and Visualize cells expose a
**Source network** selector so one notebook can contain several graphs.

If a build cell was split by a grouping column, scope controls choose between:

- each group as small multiples;
- a merged network.

Always verify the selected source before interpreting a cell.

## Visualize settings panel

The **Settings** button on a Visualize cell opens a movable control panel.

### Canvas

Controls height, horizontal/vertical pan, and zoom.

### Network

Chooses source, split-network scope, layout, node coloring, community method,
background, and isolate visibility. Layouts include force, circular,
concentric, radial, grid, random, bipartite, shell, hierarchical, arc,
heatmap, and others.

### Nodes

Controls size measure, scale, color, label visibility, label size, and label
color.

### Edges

Controls weight-based width, line color/style, scale, display threshold,
arrows, weight-gradient coloring, width/opacity ranges, and edge labels.

### Visualize

Renders the graph with current settings.

### Shake

Restarts layout motion to help separate overlapping nodes in force-based
views.

### Duplicate and reset

The panel header can duplicate the Visualize cell or reset its controls.

## Cell controls

Each cell provides:

- **Settings** for Visualize cells;
- **Minimize** to collapse the cell;
- **Lock** to freeze settings and cached output;
- **Remove** to delete the cell;
- a cell-specific run button;
- table and plot exports when results are available.

## Plot exports

Network plots offer:

- **SVG** — scalable vector output;
- **PNG** — high-resolution raster output;
- **HD** — ultra-high-resolution PNG;
- **JPG** — high-resolution JPEG;
- **Copy** — copy a PNG to the clipboard;
- **Fullscreen** — expand the plot.

Prefer SVG for publication figures and PNG/HD for slides or raster workflows.

## Table exports

Enhanced tables provide:

- download as CSV, TSV, JSON, or Markdown;
- copy as TSV;
- copy as HTML for Word/Google Docs;
- copy as Markdown.

## Lower-left notebook lock menu

### Editable

Normal working state.

### Read-only

Soft read-only state that can be returned to editable.

### Locked

Frozen state. Editing requires **Duplicate to editable copy**.

### Sealed

Frozen state with a SHA-256 fingerprint. Later changes to canonical notebook
state are flagged.

### Copy fingerprint

Copies the seal metadata for external recording.

### Duplicate to editable copy

Creates an editable copy while preserving the locked/sealed original.

Select the intended state, then click **Save** to download that version.

## Browser persistence versus portable save

CarmNote SNA autosaves the active workspace in the current browser. Browser
storage can be cleared, limited, or tied to one profile/device. The durable,
shareable research artifact is the `.html` file downloaded with **Save**.

## Footer: About, License, and How to cite

Opens the bundled offline panel containing the software description,
research-license terms, citation text, BibTeX, and contact details.
