# gh-pages-workflow

Workflow to build and deploy a Hugo site to GitHub Pages on push.

---

## Features

- Automated build and deployment of Hugo static sites
- Triggered on pushes to `main` and `gh-pages` branches
- Uses GitHub Actions with two main jobs: build and deploy
- Installs Hugo CLI and Dart Sass for site generation
- Supports Node.js dependencies installation for JavaScript modules
- Uploads build artifacts for deployment to GitHub Pages
- Concurrency control to avoid overlapping deployments

## Tech Stack

- GitHub Actions
- Hugo static site generator
- Dart Sass
- Node.js (optional, for JS dependencies)

## Getting Started

### Prerequisites

- GitHub repository with Hugo site source
- Enable GitHub Pages on the repository

### Installation

1. Copy the `hugo.yaml` workflow file to `.github/workflows/hugo.yaml` in your repository.
2. Adjust Hugo version or other environment variables if needed.
3. Commit and push the workflow file.

### Running

- The workflow triggers automatically on push to `main` or `gh-pages` branches.
- You can also trigger it manually from the GitHub Actions tab.

## Project Structure

```
.github/workflows/hugo.yaml  # GitHub Actions workflow for build and deploy
index.md                     # Documentation and explanation of the workflow
readme.md                    # Repository README
```

## Future Work / Roadmap

- Add support for additional Hugo versions via inputs
- Integrate cache for Node.js dependencies to speed up builds
- Add testing steps for site validation
- Support deployment to other branches or custom domains
- Enhance concurrency management with cancellation of queued runs

---

This workflow aims to simplify and automate the build and deployment process of Hugo sites on GitHub Pages, reducing manual steps and ensuring consistent deployments.
