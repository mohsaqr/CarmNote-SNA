# CarmNote SNA Downloads and Versions

[Documentation index](./INDEX.md) · [User guide](./USER-GUIDE.md) ·
[Menus and interface](./MENUS-AND-INTERFACE.md) ·
[Cell reference](./CELL-REFERENCE.md)

Each CarmNote SNA release is provided in two files. Both use the same
JavaScript numerical engine; one is the full build and one is minified.

## Quick recommendation

The recommended file is the full build ending in **`-full.html`**:

`sna-notebook_V2.1.22-full.html`

It is the recommended build for routine analysis, teaching, sharing,
and archiving.

## The two files

| Filename pattern | Engine | Packaging | Best use |
|---|---|---|---|
| `sna-notebook_V…-full.html` | JavaScript | Full | Recommended default; analysis, teaching, sharing, and archiving |
| `sna-notebook_V…-min.html` | JavaScript | Minified | Web hosting or bandwidth-sensitive direct download |

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

The minified file is **not** suitable as an ordinary email attachment. Many
institutional and commercial mail systems block or quarantine HTML containing
large minified scripts.

The preferred delivery methods are:

1. A link to the immutable file in the GitHub release repository.
2. A link from the approved LaCarm/notes website.
3. An institutionally approved file-sharing service.
4. Where policy permits attachments, the full build in an approved archive
   format—with the caveat that some gateways also scan or block archives.

Even the full `.html` build may be blocked by organizations that prohibit all
HTML attachments. A download link is the most reliable option.

## File identification

For `sna-notebook_V2.1.22-min.html`:

- `sna-notebook` — CarmNote SNA;
- `V2.1.22` — notebook release version;
- `min` — minified packaging;
- `.html` — complete self-contained notebook.

The version shown in the filename should match the version badge inside the
notebook.

## Integrity and archiving

Released files are immutable. The SHA-256 value in the release table verifies
a downloaded file. Long-term research archiving involves:

- keeping the exact original release file;
- keeping the saved analysis notebook produced from it;
- recording the filename, version, and checksum;
- preferring the full build unless storage or download constraints require
  the minified form.
