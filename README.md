# easypng-action

A GitHub Action wrapper around [easypng](https://www.npmjs.com/package/easypng), for compressing and
converting PNG, JPEG, WebP, and AVIF images in CI. Uses mozjpeg, pngquant-style palette quantization,
libwebp, and libavif under the hood.

See also: [EasyPNG](https://amanghuman.com/easypng.html), the browser version of the same tool.

## Usage

```yaml
- name: Compress images
  uses: amanghuman/easypng-action@v1
  with:
    path: assets/images
    recursive: "true"
    format: webp
    quality: "80"
    out: dist/images
```

### Fail the build if anything is still too large

```yaml
- name: Compress images
  uses: amanghuman/easypng-action@v1
  with:
    path: assets/images
    recursive: "true"
    max-size: "150"
    max-size-except: |
      hero.jpg=500
      *.svg
```

### Multiple paths or glob patterns

```yaml
- name: Compress images
  uses: amanghuman/easypng-action@v1
  with:
    path: |
      assets/logos/*.png
      assets/photos/**/*.jpg
```

## Inputs

| Name | Description | Default |
|---|---|---|
| `path` | Files, directories, or glob patterns to compress, one per line for multiple. Required. | |
| `out` | Output directory. | `easypng-output` |
| `format` | Output format: `original`, `png`, `jpeg`, `webp`, `avif`. | `original` |
| `quality` | Quality 1-100 for jpeg/webp/avif and PNG palette quantization. | `75` |
| `colors` | PNG palette size, 2-256, or 0 for lossless PNG. | `256` |
| `resize` | Resize before compressing: `50%`, `1920`, or `800x600`. | (skip) |
| `target-size` | Best-effort target size in KB. | (skip) |
| `max-size` | Fail if any compressed file is still over this size in KB. | (skip) |
| `max-size-except` | Exceptions to `max-size`, one `pattern` or `pattern=kb` per line. | (skip) |
| `recursive` | Recurse into subdirectories when a directory is given. | `false` |
| `concurrency` | Max files encoded in parallel. | (auto) |
| `version` | Which `easypng` npm version to run. | `latest` |

## Outputs

| Name | Description |
|---|---|
| `succeeded` | Number of files compressed successfully. |
| `failed` | Number of files that failed to compress. |
| `total-original-size` | Total original size in bytes. |
| `total-compressed-size` | Total compressed size in bytes. |
| `total-saved-percent` | Overall percent saved. |
| `over-budget-count` | Number of files still over the max-size budget. |
| `result-json` | The full JSON result, same shape as `easypng --json`. |

## License

MIT
