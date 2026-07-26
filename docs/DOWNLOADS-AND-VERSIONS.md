# CarmNote SNA Downloads and Versions

[Documentation index](./INDEX.md) · [User guide](./USER-GUIDE.md) ·
[Menus and interface](./MENUS-AND-INTERFACE.md) ·
[Cell reference](./CELL-REFERENCE.md)

Each CarmNote SNA release is provided in two files. Both use the same
JavaScript numerical engine; one is the full build and one is minified.

## Quick recommendation

Use the full file ending in **`.html`** without `.beta.min`:

`sna-notebook_V2.1.22.html`

It is the recommended build for routine analysis, teaching, sharing,
and archiving.

## The two files

| Filename pattern | Engine | Packaging | Best use |
|---|---|---|---|
| `sna-notebook_V….html` | JavaScript | Full | Recommended default; analysis, teaching, sharing, and archiving |
| `sna-notebook_V….beta.min.html` | JavaScript | Minified | Web hosting or bandwidth-sensitive direct download |

CarmNote SNA does not currently have a separate WASM release. Both files run
the same JavaScript analysis engine.

## Full versus minified

Minification removes formatting, shortens internal identifiers where safe,
and compresses most JavaScript into very long lines. It changes packaging,
not the scientific method.

The minified build:

- has the same user interface and intended numerical results;
- is smaller to download;
- does not materially speed up network analysis;
- is harder to review, compare, debug, or audit as text;
- is more likely to look suspicious to email gateways and malware scanners
  because it contains dense, obfuscated-looking JavaScript inside HTML.

### Email warning

Do **not** use the minified file as an ordinary email attachment. Many
institutional and commercial mail systems block or quarantine HTML containing
large minified scripts.

Prefer one of these delivery methods:

1. Send a link to the immutable file in the GitHub release repository.
2. Send a link from the approved LaCarm/notes website.
3. Use an institutionally approved file-sharing service.
4. If policy permits attachments, use the full build in an approved archive
   format—but assume that some gateways also scan or block archives.

Even the full `.html` build may be blocked by organizations that prohibit all
HTML attachments. A download link is the most reliable option.

## What “beta” means

In these filenames, `beta` refers to the minified build pipeline. It does not
identify a different network-analysis engine or different statistical
results. The unminified file remains the conservative release default.

## How to identify a file

For `sna-notebook_V2.1.22.beta.min.html`:

- `sna-notebook` — CarmNote SNA;
- `V2.1.22` — notebook release version;
- `.beta.min` — minified packaging;
- `.html` — complete self-contained notebook.

The version shown in the filename should match the version badge inside the
notebook.

## Integrity and archiving

Released files are immutable. Use the SHA-256 value in the release table to
verify a downloaded file. For long-term research archiving:

- keep the exact original release file;
- keep the saved analysis notebook produced from it;
- record the filename, version, and checksum;
- prefer the full build unless storage or download constraints require the
  minified form.
