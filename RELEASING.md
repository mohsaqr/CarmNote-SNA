# How to cut a CarmNote SNA release

This repo distributes the **compiled CarmNote SNA only** — no source code.
The source repo (`../carm-sna`) is never touched by this process; the tool
only *reads* its `dist/` folder. The repo root is the release: `README.md`
(version table), `index.html` (latest build), `versions/` (immutable archive).

The full mechanism — philosophy, config schema, how to stand up a release
repo for another notebook — is documented in the CarmNote release playbook
(`Note/RELEASE-MECHANISM.md` in the workspace).

## One release, four steps

```bash
# 1. In the SOURCE repo (../carm-sna): bump notebook.version.cjs and
#    rebuild:
#      cd ../carm-sna && npm run build:notebook

# 2. In THIS repo: publish the current build (use --dry-run to preview)
node tools/release.cjs sna

# 3. Run the tests if you touched the tooling
node tools/release.test.cjs

# 4. Commit + tag + push (the tool never runs git itself)
git add README.md index.html versions
git commit -m "sna v2.1.22"
git tag sna-v2.1.22
git push && git push --tags
```

Optionally also attach the files to a GitHub Release for a nicer download
page:

```bash
gh release create sna-v2.1.22 versions/sna-notebook_V2.1.22*.html \
  --title "CarmNote SNA v2.1.22" --notes "See README.md for checksums."
```

## What the tool guarantees

- **Version truth:** the released version is read from the source repo's
  `notebook.version.cjs` — the same single source of truth the build stamps
  into the filename and the in-app header.
- **Immutability:** an already-released file is never overwritten. If the
  bytes differ, the release aborts — bump the version upstream and rebuild.
- **Exact bytes:** files are byte-copies of the build output; the README
  records size + SHA-256 for every artifact.
- **Latest pointer:** `index.html` is a copy of the newest default build.
  With GitHub Pages enabled (Settings → Pages → deploy from `main`),
  `https://<user>.github.io/CarmNote-SNA/` opens the live notebook.

## Keeping the tooling in sync

`tools/release.cjs` and `tools/release.test.cjs` are copies of the canonical
versions in the `CarmNote-TNA` repo. If you fix or extend the tool, make the
change in CarmNote-TNA first, run its tests, then copy both files here (and
to any other CarmNote-* release repo) and re-run the tests.

## Publishing on the CarmNote Store

After the tag and `git push --tags`, the release is published on the CarmNote
Store (https://carmstore.lacarm.com). The command runs from this repository's
root:

```bash
node "../Carmnote Store/server/tools/push.mjs" --all --dry-run   # what a push would send
node "../Carmnote Store/server/tools/push.mjs" --all             # publish
```

The push reads the new tag, the release files and the `carm-manifest` stamped
in each file (version, date, functions, release notes as news). It uploads
only what the store lacks and never replaces a published file; a faulty
version is yanked and superseded. The publish token is read from
`~/.config/carmstore/token` (issued with
`node "../Carmnote Store/server/tools/push-token.mjs" create --name <agent> --save`).

- Protocol: `../Carmnote Store/docs/PUSH-PROTOCOL.md`
- Agent procedure: the `carmstore-push` skill
  (`../Carmnote Store/skills/carmstore-push/SKILL.md`, installed in
  `~/.claude/skills`)
- Store-only text (capabilities, usage, figures):
  `../Carmnote Store/server/registry/<id>.json`
