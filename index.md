---
slug: "github-gh-pages-workflow"
title: "gh-pages-workflow"
repo: "justin-napolitano/gh-pages-workflow"
githubUrl: "https://github.com/justin-napolitano/gh-pages-workflow"
generatedAt: "2025-11-23T09:01:22.866130Z"
source: "github-auto"
---


# Building and Deploying Hugo Sites with GitHub Actions: A Reference

## Motivation

Managing static site deployments manually is error-prone and inefficient. This project automates the build and deployment of Hugo sites to GitHub Pages using GitHub Actions. It addresses the need for a reliable, repeatable workflow that integrates site generation, dependency management, and deployment in a single pipeline.

## Problem Statement

Deploying Hugo sites typically involves local builds followed by manual pushes to a deployment branch or service. This workflow can lead to inconsistencies, missed steps, or outdated sites. Automating this process ensures the site is always up-to-date with the latest source changes, reduces human error, and streamlines continuous delivery.

## Implementation Overview

The workflow is defined in a YAML file (`hugo.yaml`) that executes on pushes to the `main` and `gh-pages` branches, as well as manual triggers. It uses GitHub Actions permissions to grant the necessary access for content reading and page writing.

Concurrency is managed to allow only one deployment at a time without canceling in-progress runs, ensuring production deployments complete fully.

### Jobs

Two main jobs run sequentially:

1. **Build Job**
   - Runs on an Ubuntu VM.
   - Installs a specified version of Hugo CLI by downloading the Debian package and installing it.
   - Installs Dart Sass via snap for CSS preprocessing.
   - Checks out the repository including submodules recursively.
   - Configures GitHub Pages environment using `actions/configure-pages@v4`.
   - Installs Node.js dependencies if lock files are present, enabling JavaScript module builds.
   - Runs Hugo build with garbage collection and minification flags, setting the base URL dynamically from the Pages output.
   - Uploads the generated site as an artifact for deployment.

2. **Deploy Job**
   - Runs on an Ubuntu VM.
   - Uses `actions/deploy-pages@v4` to deploy the uploaded artifact to GitHub Pages.

### Environment and Permissions

- The workflow sets the shell to bash by default.
- Permissions include read access to repository contents and write access to GitHub Pages and ID tokens.

### Concurrency

- The `concurrency` key groups runs under "pages" and disables canceling in-progress runs, avoiding deployment interruptions.

## Practical Considerations

- The workflow assumes the repository contains a valid Hugo site with optional Node.js dependencies.
- It requires no manual intervention once set up, improving developer productivity.
- The use of submodules is supported, which is relevant for sites that include external content or themes.
- The base URL for Hugo is dynamically set to the GitHub Pages URL, ensuring correct asset linking.

## Summary

This workflow encapsulates best practices for CI/CD of Hugo static sites on GitHub Pages. It balances automation with control, providing a robust, maintainable pipeline. Returning to this project, one can understand the rationale behind each step and extend or customize it as needed for evolving site requirements or infrastructure changes.
