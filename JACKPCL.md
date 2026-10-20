# JackPCL

Personal downstream of the official PCL source tree (independent repository — upstream sync runs via the Sync workflow).

## Branch

- Working branch: `jack-pcl`
- Initial base: PCL `2.99.0.0`
- Local patch: `RestrictMcDownload = False`
- Launch-time nag prompts removed (sponsorship + buy-Minecraft)

The tree keeps the upstream source structure intact and carries only small JackPCL-specific patches.

## Build

GitHub Actions workflow: **JackPCL Build**

It runs automatically when relevant files are pushed to `jack-pcl`, and can also be started manually from the Actions page.

A successful run uploads an artifact containing:

- `JackPCL.exe`
- `BUILD_INFO.txt`
- `JackPCL-<version>-<commit>.zip`

Artifacts are retained for 90 days.

## Optional API credentials

The public source tree does not include upstream private API credentials. If these features are needed in a source build, add repository Actions secrets with these names:

- `CLIENT_ID` — Microsoft OAuth client ID
- `CURSEFORGE_API_KEY` — CurseForge API key

The build workflow works without them, but features that depend on those credentials may be unavailable.

## Sync with official PCL

GitHub Actions workflow: **Sync JackPCL Upstream**

Run it manually when you want to merge the latest official `Meloong-Git/PCL` `main` branch into `jack-pcl`.

The workflow:

1. fetches official upstream,
2. merges it into `jack-pcl`,
3. verifies/re-applies `RestrictMcDownload = False`,
4. pushes the result,
5. which then triggers a fresh JackPCL build.

If upstream removes or substantially changes the restriction flag, the sync workflow intentionally fails instead of making an unsafe automatic edit.

## Notes

This is a personal downstream and is not an official PCL build. Keep the upstream licence and attribution requirements in mind before redistributing modified binaries.
