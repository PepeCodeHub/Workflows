# Workflows Repository
This repository contains reusable GitHub Actions workflows for automating various tasks such as creating GitHub releases and publishing Docker containers. 🚀

### Reusable GitHub Release Workflow

This workflow automates the process of creating a GitHub release. It can be reused in other workflows by calling it with the necessary inputs. 📦

#### Inputs

- `tag_name` (required): The Git tag name for the release (e.g., v1.0.0). 🏷️
- `release_name` (optional): The name of the release (e.g., Release v1.0.0). Defaults to the tag name if not provided. 📝
- `release_body` (optional): The body of the release notes. Defaults to a standard message if not provided. 📄
- `asset_path` (optional): The path to the asset file to upload. 📂
- `asset_name` (optional): The name of the asset file for the release. 🗂️

#### Secrets

- `ORG_PAT` (required): GitHub token for authentication. 🔑

#### Jobs

- `create-release`: Creates a GitHub release and optionally uploads an asset. 🚀

#### Example

To use this workflow in your repository, you can call it from your own workflow file as shown below. 📋

```yaml
name: Create Release
on:
    push:
        tags:
            - 'v*.*.*'

jobs:
    call-reusable-workflow:
        uses: ./.github/workflows/release.yml
        with:
            tag_name: ${{ github.ref }}
            release_name: Release ${{ github.ref }}
            release_body: "Release notes for ${{ github.ref }}"
        secrets:
            ORG_PAT: ${{ secrets.ORG_PAT }}
```

### Reusable Docker Publish Workflow

This workflow automates the process of building and publishing Docker images to Docker Hub and GitHub Container Registry (GHCR). It can be reused in other workflows by calling it with the necessary inputs. 🐳

#### Inputs

- `docker_image_name` (required): The name of the Docker image to build and publish. 🏷️

#### Secrets

- `DOCKERHUB_USERNAME` (required): Docker Hub username for login. 🔑
- `DOCKERHUB_TOKEN` (required): Docker Hub token or password for login. 🔑
- `GHCR_TOKEN` (required): GitHub token for publishing to GitHub Container Registry. 🔑

#### Jobs

- `build-and-publish`: Builds the Docker image, tags it, and pushes it to Docker Hub and GHCR. 🚀

#### Example

To use this workflow in your repository, you can call it from your own workflow file as shown below. 📋

```yaml
name: Publish Docker Image
on:
    push:
        branches:
            - main

jobs:
    call-reusable-workflow:
        uses: ./.github/workflows/docker-publish.yml
        with:
            docker_image_name: my-docker-image
        secrets:
            DOCKERHUB_USERNAME: ${{ secrets.DOCKERHUB_USERNAME }}
            DOCKERHUB_TOKEN: ${{ secrets.DOCKERHUB_TOKEN }}
            GHCR_TOKEN: ${{ secrets.GHCR_TOKEN }}
```
