# Pandoc devcontainer

# Building

```bash
devcontainer build --workspace-folder src
```

# Usage

Create a `.devcontainer.json` or `.devcontainer/devcontainer.json` file in your repository root with the following content.

```json
{
  "name": "Pandoc markdown editing",
  "image": "ghcr.io/fclad/pandoc-markdown-devcontainer:latest"
}
```
