# MessageFlow Aggregator

A GitHub Actions-based aggregator that automatically collects AsyncAPI specifications from multiple source repositories and generates unified documentation using MessageFlow.

```
Source Repo A ──┐
Source Repo B ──┼──> MessageFlow Aggregator ──> Generated Docs
Source Repo C ──┘         (this repo)
```

Specifically, this aggregator repository listens for notifications from [the example source repo](https://github.com/holydocs/messageflow-source-workflow-example), triggering automatic generation of the [documentation](/docs).

## Overview

This repository shows how to create your own central hub that:
- Receives notifications when source repositories have new commits on the main branch
- Automatically fetches and aggregates AsyncAPI specifications
- Generates comprehensive documentation for all collected APIs
- Maintains a single source of truth for your distributed API landscape

## Quick Start

### Set Up

1. **Create Your Own Aggregator Repository**
   - Adjust and create [.github/workflows/generate-messageflow-docs.yml](.github/workflows/generate-messageflow-docs.yml) in your aggregator repository

2. **Add the Notification Workflow to Source Repository**
   - Create [.github/workflows/notify-messageflow-aggregator.yml`](https://github.com/holydocs/messageflow-source-workflow-example/blob/main/.github/workflows/notify-messageflow-aggregator.yml) in each source repository

3. **Create a CI Bot Account**
   - Create a new GitHub account for your CI bot or use existing service account
   - Add the bot as a collaborator to:
     - Aggregator repository (with write access)
     - All source repositories (with read access)

4. **Create Personal Access Token (PAT)**
   - Log in as the CI bot account
   - Go to Settings → Developer settings → Personal access tokens → Tokens (classic)
   - Generate new token with `repo` scope
   - Save the token securely

5. **Configure Aggregator/Source Repository Secrets**
   - In aggregator repository:
     - Go to Settings → Secrets and variables → Actions
     - Add new secret: `INTEGRATION_PAT` with the bot's PAT

### Run

1. Push an AsyncAPI file to any source repository
2. The source repository will notify this aggregator
3. Check the Actions tab to see the aggregation workflow run
4. Generated documentation will appear in the `docs/` directory
