# CarmNote SNA Cell Reference

[Documentation index](./INDEX.md) ·
[Downloads and versions](./DOWNLOADS-AND-VERSIONS.md) ·
[User guide](./USER-GUIDE.md) ·
[Menus and interface](./MENUS-AND-INTERFACE.md)

This guide explains every cell available from the current CarmNote SNA notebook header. It is intended as a practical reference: what each cell does, what it needs, which controls matter, and what it produces.

The [User guide](USER-GUIDE.md) describes the overall workflow, and [Menus and interface](MENUS-AND-INTERFACE.md) describes commands outside individual cells.

## How to read this reference

Every cell is documented with the same five questions:

- **Purpose** — what analytical question it addresses.
- **Requires** — data or network state needed before it can run.
- **Main controls** — settings that materially affect the analysis.
- **Produces** — the principal tables, plots, or graph sources.
- **Cautions** — interpretation, reproducibility, or performance cautions.

## Generate

**Purpose:** Creates a synthetic network without loading a data file.

**Requires:** A model choice and its parameters.

**Main controls:**

- **Model:** Erdős–Rényi, Barabási–Albert, Watts–Strogatz, or stochastic block model (SBM).
- **Nodes:** Number of nodes to generate.
- **Model parameters:** Depending on the selected model, these include edge probability, links added per new node, neighborhood size, rewiring probability, number of blocks, and within- or between-block probabilities.
- **Directed:** Generates directed or undirected edges.
- **Seed:** Makes a generated example reproducible. The default is `42`.

**Produces:** A generated graph, a network summary, and a reusable network source for later cells.

**Cautions:** Synthetic networks illustrate model behavior; they are not substitutes for observed data. The model, parameters, direction setting, and seed are recorded when results are reported.

## Co-occurrence

**Purpose:** Builds a network from items that occur together in transactions, groups, documents, events, or other shared units.

**Requires:** Loaded tabular data or pasted transaction data.

**Main controls:**

- **Field nodes:** Column containing the items that become nodes.
- **Group by:** Column defining each transaction or co-occurrence unit.
- **Separator:** Splits multiple items stored in one field.
- **Similarity:** None, cosine, Jaccard, Dice, inclusion, association, equivalence, or relative similarity.
- **Counting:** Full, fractional, or attention counting. Attention counting also uses a decay value (`lambda`).
- **Scale:** None, min–max, z-score, logarithm, base-10 logarithm, square root, proportion, or binary.
- **Filters:** Weight threshold, minimum occurrence, top-N edges, and co-occurrence window.
- **Weight column:** Optional observation weight.
- **Aggregate by:** Sum, mean, minimum, or maximum when repeated values need aggregation.
- **Split by:** Creates separate networks for categories in another column.

**Produces:** A weighted co-occurrence network and a source that can be used by visualization and analysis cells. A split can produce several related networks.

**Cautions:** The `Group by` choice defines what “together” means. Similarity, counting, scaling, and filtering can substantially change the network. `Aggregate by` and `Split by` cannot be used together in the current interface.

## Network

**Purpose:** Builds one or more networks from an edge-list data set.

**Requires:** A loaded CSV or TSV file containing source and target columns.

**Main controls:**

- **From:** Source-node column.
- **To:** Target-node column.
- **Weight:** Optional edge-weight column.
- **Directed:** Treats ties as directed or undirected.
- **Split by:** Optional column used to construct one network per group, wave, class, or other category.

**Produces:** A graph source and a network summary. When `Split by` is used, the cell also produces grouped network results that later cells can analyze by group or as a merged network.

**Cautions:** Node identifiers should be unaltered by spreadsheet software, missing identifiers should be handled consistently, and the direction setting should match the meaning of the data.

## Visualize

**Purpose:** Draws a network and controls its layout, node appearance, edge appearance, labels, and export.

**Requires:** A graph source produced by Generate, Co-occurrence, Network, or another compatible cell.

**Main controls:**

- **Source:** Selects the graph to draw.
- **Split scope:** For grouped sources, selects one group or a merged network.
- **Canvas:** Sets height and allows pan or zoom.
- **Layout:** Force, circular, concentric, radial, grid, random, bipartite, spectral, shell, star, spiral, hierarchical, multidimensional scaling, Fruchterman–Reingold, Kamada–Kawai, arc, dual circle, community-grouped, degree-sorted, or heatmap.
- **Node color:** Colors by community, centrality, or a single color. Community coloring includes a method selector.
- **Node size:** Sizes nodes by a selected centrality measure or applies a fixed size.
- **Labels:** Shows, hides, and styles node labels.
- **Edges:** Controls weighted width, color, style, scale, threshold, arrows, gradient, minimum and maximum width, opacity, and labels.
- **Background and isolates:** Sets the background and optionally hides isolated nodes.

**Produces:** An interactive network plot. Plot actions include SVG, PNG, high-definition image, JPG, copy, and full-screen export or display. **Shake** reruns a stochastic layout to explore another arrangement.

**Cautions:** A layout changes positions, not the underlying graph. Visual proximity is not evidence unless the chosen layout and analysis justify that interpretation. Thresholds and hidden-isolate settings are recorded because they affect what viewers see.

## Properties

**Purpose:** Summarizes the overall structure of a network.

**Requires:** A graph source and, for split networks, a selected scope.

**Main controls:**

- **Source:** Selects the network.
- **Scope:** Selects an individual group or the merged network when applicable.

**Produces:** Graph-level properties, degree-distribution information, weight-distribution information, and an adjacency summary.

**Cautions:** Directed, weighted, disconnected, and merged networks can give metrics different interpretations. Networks are comparable only when their construction and filtering rules are compatible.

## Centrality

**Purpose:** Estimates the structural position or importance of each node.

**Requires:** A graph source and, for split networks, a selected scope.

**Main controls:**

- **Measures:** Out-strength, in-strength, closeness, betweenness, random-shortest-path betweenness, diffusion, clustering, and PageRank.
- **Normalize:** Returns normalized or unnormalized values where supported.
- **Self-loops:** Includes or excludes self-loops.

All measures except diffusion are selected by default.

**Produces:** Node-level centrality results and associated summaries or charts.

**Cautions:** Centrality measures answer different questions and may not be comparable across networks of different size or density without suitable normalization. Diffusion centrality is computationally expensive—approximately \(O(n^4)\)—and can be slow on large networks.

## Community

**Purpose:** Detects groups of nodes that are more densely connected to one another than to the rest of the network.

**Requires:** A graph source and, for split networks, a selected scope.

**Main controls:**

- **Method:** Louvain, Walktrap, Fast Greedy, Label Propagation, Leading Eigenvector, or Edge Betweenness.

**Produces:** A community assignment for each node and a community summary.

**Cautions:** Methods use different optimization criteria and can return different partitions. Some algorithms contain stochastic elements or tie-breaking behavior; settings and rerun information are retained when reproducibility matters.

## Cliques

**Purpose:** Finds fully connected groups of nodes.

**Requires:** A graph source and, for split networks, a selected scope.

**Main controls:**

- **Clique size:** Minimum requested clique size; the default is `3`.
- **Minimum weight:** Ignores ties below the selected edge-weight threshold.

**Produces:** Clique memberships and a table of detected cliques.

**Cautions:** Clique enumeration can become expensive in large or dense graphs and can produce a very large result. A weight threshold can improve focus but changes the graph being searched.

## Text

**Purpose:** Adds interpretation, instructions, headings, captions, or other narrative material to the notebook.

**Requires:** No data source.

**Main controls:**

- Title, heading, bold, italic, and underline formatting.
- Bulleted and numbered lists.
- Text alignment, superscript, and subscript.
- Image and table insertion.
- Clear and lock controls.

**Produces:** A formatted narrative cell that is included when the notebook or report is saved or exported.

**Cautions:** The data source, construction choices, filters, direction, weights, and interpretation are stated next to the relevant outputs so the notebook remains understandable when shared.

## Code

**Purpose:** Runs custom JavaScript for analyses or outputs not covered by the visual cells.

**Requires:** JavaScript knowledge and, when needed, data or network objects already present in the notebook.

**Main controls and facilities:**

- Access to the notebook state through `S`.
- Access to D3 and CarmNote SNA functions.
- Helpers for printing text and tables.
- `Shift+Enter` to run code.

**Produces:** Custom calculations, text, tables, or other JavaScript-generated output.

**Cautions:** Code cells can change notebook state and can execute any JavaScript included in the file. Code in a notebook received from someone else should be reviewed before it is run. Custom logic should be explained, and dependence on undocumented state avoided, if the notebook must be reproducible.

## Compatibility: Metrics cells from older notebooks

Some previously saved notebooks may contain a **Metrics** cell even though it is not a separate button in the current header.

The compatibility cell can calculate a selectable set of graph measures, including measures related to size, density, path length or diameter, transitivity, reciprocity, and connected components. It uses the same source and split-scope pattern as the current analysis cells.

A compatibility cell is not to be deleted merely because it is absent from the current header. When an older notebook is reviewed, the cell is run and its output checked; **Properties** is the cell for new work unless the older cell provides a specifically needed measure.

## A reproducible cell sequence

A clear SNA notebook usually follows this order:

1. A **Text** cell describing the question, data source, and unit of analysis.
2. **Network**, **Co-occurrence**, or **Generate** to create the graph.
3. **Properties** to check the graph before interpretation.
4. **Visualize** for a readable graphical overview.
5. **Centrality**, **Community**, or **Cliques** only when they answer the stated question.
6. A final **Text** cell recording construction choices, filters, limitations, and conclusions.
7. **Save** to export a portable HTML copy.

The commands used to load, save, lock, print, and export the notebook are described in [Menus and interface](MENUS-AND-INTERFACE.md).
