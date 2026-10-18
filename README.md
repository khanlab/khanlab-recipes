# khanlab conda recipes

[rattler-build](https://rattler.build) recipes for third-party packages that
khanlab tools need but that are not available on conda-forge or bioconda.
(khanlab's own packages, such as zarrnii and vesselfm, are built with
pixi-build in their own repositories.) The recipes here are published
to the [`akhanf/khanlab`](https://prefix.dev/channels/akhanf/khanlab) channel
on prefix.dev.

| Package | Version | Source | Needed by |
|---|---|---|---|
| `ngff-zarr` | 0.34.0 | PyPI | zarrnii |
| `imaris-ims-zarr` | 0.2.0 | PyPI | zarrnii |
| `dynamic-network-architectures` | 0.4.4 | PyPI | SPIMquant (LANTERN) |

## Notes

- **ngff-zarr** is held at 0.34.0, the version zarrnii is tested against. From
  0.44 it depends on `zarrista`, a Rust extension that is not on conda-forge.

## Adding or updating a package

1. Add or edit `recipes/<name>/recipe.yaml`. To update, change `version` and
   the source `sha256`, and reset the build `number` to 0. To rebuild the same
   version, increase the build `number` instead.
2. Build locally:

   ```bash
   pixi exec rattler-build build --recipe-dir recipes --output-dir output \
     -c conda-forge -c https://prefix.dev/akhanf/khanlab
   ```

3. Open a PR. CI builds and tests the recipes whose version or build number
   isn't on the channel yet. Merging to `main` uploads them, using the
   `PREFIX_API_KEY` repository secret.
