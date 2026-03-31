# setup-nextmv

Setup your GitHub Actions workflow with the Nextmv CLI to manage and interact with your Nextmv Platform apps.

This action:

- Installs the Nextmv CLI.
- Installs `uv` with `astral-sh/setup-uv` only when needed to manage CLI versions.
- Configures the CLI with a provided API key. Even though the API key is optional, it is required for all `nextmv cloud` operations.

## Example Usage

This example shows how to use the action to install the Nextmv CLI and then use it to push an app to the Nextmv Platform (the app is [`nextroute`](https://github.com/nextmv-io/community-apps/tree/develop/go-nextroute) in this case).

```yaml
name: Push to staging
on:
  push:
    branches:
      - main
jobs:
  sandbox:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v6

      - name: Install Nextmv CLI
        uses: nextmv-io/setup-nextmv@v1
        with:
          api-key: ${{ secrets.NEXTMV_API_KEY }}

      - name: Push new version of nextroute and update staging instance
        run: |
          nextmv cloud app push -a nextroute --version-yes --update-instance-id staging
        working-directory: ./nextroute  # Location of the app to push
```

## Inputs

- `api-key`: Nextmv API key. If provided, the action automatically configures the CLI for `nextmv cloud` operations. While optional, an API key is required for all _cloud_ operations.
- `version`: Optional Nextmv CLI version (for example, `v1.3.0`). If omitted, installs the latest.
