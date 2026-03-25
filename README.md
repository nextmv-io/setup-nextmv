# setup-nextmv

Setup your GitHub Actions workflow with the Nextmv CLI to manage and interact with your Nextmv Platform apps.

This action:

- Installs the Nextmv CLI.
- Installs `uv` with `astral-sh/setup-uv` only when needed to manage CLI versions.
- Configures the CLI with a provided API key. Even though the API key is optional, it is required for all `nextmv cloud` operations.

## Usage

```yaml
steps:
  - name: Install Nextmv CLI
    uses: nextmv-io/setup-nextmv@v1
    with:
      api-key: ${{ secrets.NEXTMV_API_KEY }}

  - name: Do something with CLI
    run: |
      nextmv cloud app push -a my-app-id --version-yes --update-instance-id staging
```

## Inputs

- `api-key`: Nextmv API key. If provided, the action automatically configures the CLI for `nextmv cloud` operations. While optional, an API key is required for all _cloud_ operations.
- `version`: Optional Nextmv CLI version (for example, `v1.3.0`). If omitted, installs the latest.
