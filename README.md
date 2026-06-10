# artifactor

A minimal GitHub Actions mirror service. Paste a URL, get a public download link — useful when your enterprise network blocks certain domains but GitHub is accessible.

Each run creates a GitHub Release with the file attached as an asset. Release assets are publicly downloadable without authentication.

## Usage

1. Go to **Actions → Mirror URL to Artifact → Run workflow**
2. Fill in the inputs:

| Input | Required | Description |
|---|---|---|
| `url` | Yes | The `http://` or `https://` URL to download |
| `filename` | No | Override the output filename (defaults to the URL's last path segment) |
| `tag` | No | Git tag for the release (default: `mirror-YYYYMMDD-HHMMSS`) |
| `release_name` | No | Human-readable release title (defaults to the tag) |

3. When the run finishes, the public download URL is printed at the bottom of the job log:

```
========================================
  Public download URL:
  https://github.com/OWNER/REPO/releases/download/TAG/FILENAME
========================================
```

You can also find the file under the **Releases** page of this repo.

## Direct download (no browser)

```bash
curl -L -O https://github.com/OWNER/REPO/releases/download/TAG/FILENAME
```

## Notes

- Only `http://` and `https://` URLs are accepted.
- Each run creates a separate release. Old releases can be deleted from the Releases page when no longer needed.
- The repo must be **public** for unauthenticated downloads to work. Private repos require a token (`Authorization: Bearer <token>`) on the download request.
