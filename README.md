# artifactor

A minimal GitHub Actions mirror service. Paste a URL, get a downloadable artifact — useful when your enterprise network blocks certain domains but GitHub is accessible.

## Usage

1. Go to **Actions → Mirror URL to Artifact → Run workflow**
2. Fill in the inputs:

| Input | Required | Description |
|---|---|---|
| `url` | Yes | The `http://` or `https://` URL to download |
| `filename` | No | Override the output filename (defaults to the URL's last path segment) |
| `artifact_name` | No | Name for the artifact bundle (default: `mirrored-file`) |
| `retention_days` | No | Days to keep the artifact, 1–90 (default: `30`) |

3. Once the run finishes, open the completed workflow run and download the artifact from the **Artifacts** section at the bottom of the summary page.

## Downloading via API

If you want to script the download (e.g. pull the artifact straight into a CI job or a script):

```bash
# List artifacts for the repo
gh api repos/OWNER/REPO/actions/artifacts

# Download a specific artifact by ID
gh api repos/OWNER/REPO/actions/artifacts/ARTIFACT_ID/zip > mirrored.zip
```

Or via the GitHub web UI: run summary page → scroll to **Artifacts** → click the artifact name.

## Limits

- Only `http://` and `https://` URLs are accepted.
- GitHub artifact storage limits apply (500 MB per file is a practical safe ceiling; the hard cap is governed by your plan).
- Artifacts are deleted automatically after `retention_days`.
