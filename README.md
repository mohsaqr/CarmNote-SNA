# CarmNote SNA

> **Reference:** Saqr, M., & López-Pernas, S. (2026). *CarmNote: A Portable,
> Reproducible, Single-File Computational Software Purely in JavaScript.*
> The 26th International Symposium on Computers in Education (SIIE 2026).

**A portable, reproducible, single-file computational software for Social
Network Analysis**

[**Mohammed Saqr**](https://saqr.me) — Professor of Learning Analytics and
Artificial Intelligence, University of Eastern Finland ·
[**Sonsoles López-Pernas**](https://sonsoles.me) — Associate Professor,
University of Eastern Finland

CarmNote SNA is a self-contained JavaScript implementation of Social Network
Analysis delivered as a single HTML document, powered by the snajs engine.
The software integrates computation, visualisation, user interaction, and
analysis-state persistence within a single executable file that requires
neither internet connectivity nor server-side infrastructure. All
computation executes locally within the browser, allowing analyses to be
created, distributed, reproduced, and preserved without external
dependencies, software installation, or environment reconstruction.

This repository distributes the compiled software only. Every file under
[`versions/`](./versions/) is the complete software: download one file, open
it in a web browser, load a CSV or TSV edge list, and analyse. Nothing is
installed and no data leave the machine. The current build is
[`index.html`](./index.html); the table at the end of this page lists every
published version with its checksum.

## Design

CarmNote belongs to the family of Carm software and stands for **Contained**,
**Architecture**-driven, **Runnable**, and **Model**-based design. Contained
refers to the integration of code, interface, visualisations, data, and
results within a single self-sufficient artefact, so that distribution,
execution, and preservation are unified. Architecture-driven refers to the
fact that guarantees such as reproducibility and confidentiality arise from
structural design rather than external policy or user behaviour. Runnable
refers to execution directly within a standard web browser without
installation, configuration, or elevated privileges. Model-based refers to
the embedding of the complete analytical model — data, parameters,
procedures, and outputs — within the same file, so that the analysis can be
inspected, executed, and reproduced as a single unit.

Because the whole workflow lives in one file, an analysis can be initiated by
one researcher, extended by another, and redistributed without any shared
computational environment or software stack. Each saved file preserves the
complete analytical state, allowing subsequent users to resume work directly
from the last computed configuration, modify parameters, extend the analysis,
and re-export the updated artefact. All data remain on the client side,
loaded into local memory and processed by the browser's native JavaScript
runtime, which ensures that sensitive data never leave the user's device.

CarmNote SNA is part of [**Dynalytics**](https://dynasite.org/) — an
overarching framework and methodological ecosystem for the analysis and
rigorous validation of the dynamics of dynamical systems. Dynalytics
encompasses a diverse family of models — transition networks, co-occurrence
networks, psychological networks, and higher-order networks — unified by a
single philosophy of scientific rigour, in which analysis and validation are
inseparable: a multi-level confirmatory testing battery validates every
supported model and every analytical claim, through split-half reliability
for internal consistency, bootstrapping for edge-level stability,
case-dropping for centrality stability, and permutation-based comparisons
for groups, conditions, and temporal phases.

## Functions

CarmNote SNA covers the analysis surface of the snajs engine. The graph is
built from a dropped CSV or TSV edge list (From / To / optional Weight),
directed or undirected, with the weight column selectable at import.

Centrality analysis provides approximately ninety-five measures, including
degree, closeness, betweenness, PageRank, eigenvector, authority and hub
scores, coreness, constraint, leverage, k-reach, alpha, Bonacich power,
Laplacian, subgraph, and communicability centrality, together with
distance-derived, neighbourhood, community-aware, brokerage, and mode-free
families of measures. Community structure is detected with Walktrap,
Louvain, fast-greedy, and label-propagation algorithms, and maximal cliques
are enumerated via Bron–Kerbosch. Graph-level metrics include density,
diameter, assortativity, and transitivity.

Every analysis runs client-side. The notebook maintains a library of saved
notebooks with a four-tier lock state and a SHA-256 reproducibility seal:
saving and re-opening the file restores the complete prior analysis.

## Variants

Each version is published as a full build and as a minified build of the
same software; files ending in `-min.html` are the minified form. The
full build is the default and is what `index.html` points to. CarmNote SNA
implements its entire numerical engine in pure TypeScript-compiled
JavaScript.

## Releases

Released payloads are immutable: the checksummed bytes are never altered.
Asset names and links follow the current public naming convention. Downloads
can be verified against the SHA-256 checksums below.

<!-- releases:begin -->
| Version | Date | File | Size | SHA-256 |
|---|---|---|---|---|
| 2.1.22 | 2026-07-12 | [sna-notebook_V2.1.22-full.html](./versions/sna-notebook_V2.1.22-full.html) | 0.64 MB | `f909883866769efef39268bbf3a7e22cb79fd5918cfc98f8e3d4dfa989d37f5b` |
| 2.1.22 | 2026-07-12 | [sna-notebook_V2.1.22-min.html](./versions/sna-notebook_V2.1.22-min.html) | 0.54 MB | `eb2a54bc0771d3888df4888e1880f726e5680b366025b37b10a7a40d23bbd198` |
<!-- releases:end -->
