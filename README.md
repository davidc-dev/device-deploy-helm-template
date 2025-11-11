# device-app Helm Chart

This repository contains the `device-app` Helm chart along with automation to publish it as a GitHub Pages‑hosted Helm repository.

## Local Development

```bash
helm lint .
helm template device-app .
```

## Publishing via GitHub Pages

1. Ensure GitHub Pages is enabled on the repository and points to the `gh-pages` branch (project site mode).  
2. Push to `main`/`master` or create a tag that matches `v*`. The workflow in `.github/workflows/publish-helm.yaml` will:
   - Lint and package the chart.
   - Merge the new package/index with anything that already exists on `gh-pages`.
   - Publish the contents of the Helm repo to the `gh-pages` branch using the built-in `GITHUB_TOKEN`.
3. Consumers can add the repo with:
   ```bash
   helm repo add device-app https://<your-user>.github.io/<repo>/
   helm repo update
   helm install my-device device-app/device-app
   ```

Notes:
- The workflow automatically reuses the existing `gh-pages` branch, so prior releases remain available.
- If you want to host multiple charts, place them in subdirectories and adjust `CHART_DIR` in the workflow accordingly.
