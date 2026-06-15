# regtab.github.io

Source for the RegTab project site, published with **Material for MkDocs**
at <https://regtab.github.io/>.

The page content lives in `docs/`; everything in the repository root
(`mkdocs.yml`, `requirements.txt`, this file, `serve.bat`) is build/tooling
configuration and is **not** part of the published site.

## Local preview

On Windows, double-click `serve.bat`, or run from any OS:

```bash
pip install -r requirements.txt
mkdocs serve
```

Then open <http://127.0.0.1:8000>. The server reloads on file changes.

## Publishing

Publishing is automated by the `Deploy docs` GitHub Actions workflow
(`.github/workflows/docs.yml`): on every push to `main` it builds the site
and deploys it to GitHub Pages.

One-time setup (already done for this repository):

1. Settings -> Pages -> Build and deployment -> Source = **GitHub Actions**.
2. Push to `main`; wait for the `Deploy docs` run to finish under the Actions tab.

To publish a change, just commit and push to `main`.
