# Fodla_Builder

On-demand macOS build compute for Heathen's FOSS Godot Foundation-tier addons. Not a source repo — the real source lives on [Codeberg](https://codeberg.org/Heathen-Engineering). This repo exists only because Codeberg has no macOS CI runners.

## Usage

Trigger the "macOS build" workflow manually (Actions tab → Run workflow, or `gh workflow run build.yml -f repo=... -f ref=... -f addon_dir=...`), giving it:

- `repo` — the Codeberg repo path to build, e.g. `Heathen-Engineering/Godot-GameplayTags-Foundation`
- `ref` — the git tag to build
- `addon_dir` — path to the addon's `CMakeLists.txt` directory within that repo

No automatic triggers (no push/PR/schedule). It only ever builds what's explicitly requested.

## Known issue

`CMAKE_OSX_ARCHITECTURES` is set to build a universal (arm64 + x86_64) binary, but each product's own `CMakeLists.txt` currently hardcodes its output filename's architecture suffix to `x86_64` regardless of what was actually built (see each repo's own `CMakeLists.txt`, the `ARCH` variable). Fix that per-repo before trusting the output filename on a universal build.
