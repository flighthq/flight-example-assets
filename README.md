# flight-example-assets

A curated set of fonts, images, sounds, videos, and data files for use in Flight example projects. Assets are hosted on GitHub Releases and downloaded on demand rather than committed to the repository.

## Quick start

```sh
npm install
npm run download
```

Assets are written to `public/assets/`. Files that already exist are skipped.

## Integrating into your own project

The download script (`scripts/download-assets.ts`) is designed to be reused. It exports a `downloadAssets` function you can call directly from a build script or setup step:

```ts
import { downloadAssets } from './scripts/download-assets.ts';

await downloadAssets(manifest.assets, 'public/assets');
```

Where `manifest.assets` is an array of `{ url: string, path: string }` objects — `path` is relative to the target directory. You can point it at your own manifest or compose it with the one from this repo.

To use this repo's asset list, copy or reference `assets.manifest.json`:

```ts
import manifest from './assets.manifest.json' with { type: 'json' };

await downloadAssets(manifest.assets, 'public/assets');
```

## `assets.manifest.json`

The download manifest — a flat array of `{ url, path }` entries. This is the only file the download script reads. Add an entry here when a new asset is uploaded to the release.

## `manifest.json`

A metadata catalog of all assets organized by category (fonts, images, sounds, videos). Includes descriptions and MIME types. Not used by the download script — useful for tooling, documentation, or validating the asset list.

## Adding a new asset

1. Upload the file to the GitHub release at [flighthq/flight-assets](https://github.com/flighthq/flight-assets).
2. Add an entry to `assets.manifest.json`:
   ```json
   { "url": "https://github.com/flighthq/flight-assets/releases/download/v4/filename.ext", "path": "filename.ext" }
   ```
3. Optionally add a metadata entry to `manifest.json`.
