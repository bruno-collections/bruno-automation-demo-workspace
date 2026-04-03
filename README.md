# Bruno Automation Demo Workspace

This workspace is an example built to show how Bruno fits into automation workflows.

## What is inside

- A Bruno workspace with one YAML-based collection
- Workspace environments for `local`, `ci`, and `staging`
- Collection environments for `local`, `ci`, and `staging`
- A collection-level `.env.sample` for secret demos
- Clean request names and a simple three-folder flow for recording
- Example pipelines for GitHub Actions, Jenkins, and Azure Pipelines

## Collection flow

The collection is arranged in three sections:

1. `01 Smoke Checks` - quick requests that show environment-aware API validation
2. `02 CI Workflow` - a chained workflow that captures runtime variables and reuses them
3. `03 Release Gates` - pre-deploy and post-deploy checks for pipeline demos

## Demo endpoint

This workspace uses Bruno's public echo server:

- `https://echo.usebruno.com`

Bruno's docs use the Bruno echo server in request examples, and the public `usebruno/bruno-echo-server` repository shows the endpoint returning the POST body while mirroring request headers in the response headers.

## Open in Bruno

Option A:
1. Open Bruno
2. Open or import the workspace from this folder
3. Open `workspace.yml`

Option B:
1. Open Bruno
2. Open only the collection folder at `collections/bruno-automation-demo`
3. Bruno should pick up the collection environments from `environments/*.bru`

## Run from the Bruno app

Choose one of the workspace environments at the top right:

- `local`
- `ci`
- `staging`

Then use this on-camera flow:

1. Run `01 Smoke Checks`
2. Run `02 CI Workflow`
3. Show the repo and one of the pipeline files
4. Return to Bruno and run `03 Release Gates`

If you open only the collection, Bruno should also detect the collection environments from `collections/bruno-automation-demo/environments/*.bru`.

## Run from the CLI

From the collection root:

```bash
cd collections/bruno-automation-demo
bru run --global-env ci --workspace-path ../..
```

Filter to just the smoke checks:

```bash
bru run --global-env ci --workspace-path ../.. --tags smoke
```

Override values from CI:

```bash
bru run --global-env ci --workspace-path ../.. \
  --env-var platform_name="GitHub Actions" \
  --env-var build_id="12345" \
  --env-var commit_sha="abc123"
```

## Files you may want on screen

- `workspace.yml`
- `environments/ci.yml`
- `collections/bruno-automation-demo/opencollection.yml`
- `.github/workflows/bruno-api-tests.yml`
- `Jenkinsfile`
- `azure-pipelines.yml`

## Notes

- The collection uses YAML request files for Bruno's OpenCollection format.
- The workspace includes workspace-scoped global environments in `environments/*.yml`.
- The collection includes collection environments in `collections/bruno-automation-demo/environments/*.bru`.
- A `.env.sample` file is included at the collection root for secret-handling demos.
- The CI files are designed as readable demo assets, not as production-hardened pipelines.
