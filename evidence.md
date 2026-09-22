# Class 07 - CI/CD Delivery Evidence

## Repository

Repository:

https://github.com/juliaescoriza/class07-python-app

Final branch: `main`

Final commit:

`cba0a8354a1ab1f743b0ed772c26478791223f1c`

---

## 1. Repository and Python CI pipeline

The first pipeline was added in commit:

`88da857c735fed66622cde5c71df51d3395a2841`

Commit:

https://github.com/juliaescoriza/class07-python-app/commit/88da857c735fed66622cde5c71df51d3395a2841

The corresponding GitHub Actions run was successful:

https://github.com/juliaescoriza/class07-python-app/actions/runs/35755748288

Run: `Class 07 delivery #1`

The workflow was triggered by a push to `main` and the `test` job completed successfully.

---

## 2. Main-only trigger

The workflow was changed to run only on pushes to `main` in commit:

`1417de25ac558332c2e78a3a55f08f89ab7033bc`

Commit:

https://github.com/juliaescoriza/class07-python-app/commit/1417de25ac558332c2e78a3a55f08f89ab7033bc

The resulting workflow contains:

```yaml
on:
  push:
    branches: [main]
```

The corresponding successful GitHub Actions run was:

https://github.com/juliaescoriza/class07-python-app/actions/runs/35756567542

Run: `Class 07 delivery #2`

### Non-main branch check

A separate branch named `trigger-check` was created from the main branch.

Commit:

`3fa949c`

Commit message:

`Check the non-main trigger`

The branch was pushed to GitHub. No GitHub Actions run was created for that branch push because the workflow trigger only accepts pushes to `main`.

The branch was then merged into `main` using a fast-forward merge and pushed to GitHub. This produced the subsequent main-branch run:

`Class 07 delivery #3`

The Actions history shows the branch-check commit followed by the successful main-branch run.

---

## 3. Published image in GitHub Container Registry

The final successful publication was performed by:

Commit:

`cba0a8354a1ab1f743b0ed772c26478791223f1c`

Commit message:

`Add release recording helper`

Commit:

https://github.com/juliaescoriza/class07-python-app/commit/cba0a8354a1ab1f743b0ed772c26478791223f1c

Successful GitHub Actions run:

https://github.com/juliaescoriza/class07-python-app/actions/runs/35758666965

Run: `Class 07 delivery #5`

The package was published to GitHub Container Registry:

https://github.com/juliaescoriza/class07-python-app/pkgs/container/class07-python-app

Published image tag:

```text
ghcr.io/juliaescoriza/class07-python-app:sha-cba0a8354a1ab1f743b0ed772c26478791223f1c-run-35758666965-1
```

Registry digest:

```text
sha256:34b66987a2d891faf6af7c58f14f7a0c395fa436c430af512ca89736ac8bfeab
```

Platform:

```text
linux/amd64
```

The image was built, checked with the supplied HTTP smoke test, and then published. No second build was performed between the image verification and publication.

### Exact image retrieved from GHCR

The exact digest reference used for the final local verification was:

```text
ghcr.io/juliaescoriza/class07-python-app@sha256:34b66987a2d891faf6af7c58f14f7a0c395fa436c430af512ca89736ac8bfeab
```

The image was pulled successfully using Docker with the `linux/amd64` platform.

The image was then started locally and tested using the supplied `smoke_test.py`.

Command:

```text
python smoke_test.py "http://127.0.0.1:52204"
```

Result:

```text
PASS: health + 3 HTTP scoring cases
```

This verification was performed against the image retrieved from GHCR by its immutable digest, without rebuilding the image locally.

---

## Notes

There was an earlier publication attempt in run #4, associated with commit `9200431`, which failed during the package job. The final successful publication and release evidence is therefore based on run #5 and commit `cba0a83`.

The final repository working tree was clean and synchronized with `origin/main` after the completed work.

---

## AI-use declaration

AI assistance was used during this activity. ChatGPT was used to explain CI/CD concepts, interpret the activity instructions, troubleshoot the Windows/Docker environment, and assist with documenting the observed results. All commands were executed and verified in the student's own repository and environment, and the final evidence records actual GitHub Actions, GHCR, Docker, and smoke-test results.

