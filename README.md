# poc-github-actions

![title](/docs/github-actions.png)

This repository is a Github Actions POC with various examples regarding how to create workflows 🤖 

## Contents 🇧🇷

- [Introdução ao Github Actions](https://www.zup.com.br/blog/github-actions-ci-cd)
- [Como executar um script usando GitHub Actions](https://www.zup.com.br/blog/executar-script-github-actions)
- [Github Actions – variáveis de ambiente e secrets](https://www.zup.com.br/blog/github-actions-variaveis-de-ambiente-e-secrets)

## Workflow YAML Basic Structure Explanation

```bash
name: Github action workflow name

on:
  push: # Run this workflow every time a new commit pushed to the repository
  pull_request:  # Run this workflow every time a new pull request is opened to the repository
  scheduled: # Run this workflow as a cron job
    - cron: "0 0 * * *"
  workflow_dispatch: # Run this workflow on demand (manually)

jobs: # All workflows need at list one job

  job-key: #First job
    name: Job Name
    runs-on: ubuntu-latest # Set the type of machine the workflow will run on
    steps: # Each job can be divided in many steps

      - name: Checkout code # Step name
        uses: actions/checkout@v2 # Action used on the step

      - name: Run Super-Linter # Another step name
        uses: github/super-linter@v3  # Action used on the step
        env:  # Environment variables used on the step
          DEFAULT_BRANCH: main
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Run specific commands # Another step name
        run: |
          ls -lha
          echo "This is a shell command"

```

## Examples

[![01 - Default Workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/01-default-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/01-default-workflow.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) to run some basic commands.

[![02 - Secret Workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/02-secret-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/02-secret-workflow.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) to run some basic commands using repository secrets.

[![03 - Python Script Workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/03-python-script-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/03-python-script-workflow.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) to execute a specific script [run.py](https://github.com/GuillaumeFalourd/poc-github-actions/blob/main/run.py) located on the repository.

[![04 - Remote Dispatch Action Initiator](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/04-dispatch-event-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/04-dispatch-event-workflow.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) to dispatch an event to the [ritchie-formulas-scheduler-demo repository](https://github.com/GuillaumeFalourd/ritchie-formulas-scheduler-demo).

[![05 - Container Workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/05-container-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/05-container-workflow.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) with a docker container where Ritchie CLI and Golang are installed, then check Ritchie CLI and Golang versions through commands.

[![06 - Docker Image Workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/06-docker-image-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/06-docker-image-workflow.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) and a docker image `foundeo/minibox:latest`. It also specify an `entrypoint` (the command to run inside the container) and `args` (command line arguments to pass to the command specified in entrypoint). It is possible to omit the `entrypoint` if the container already species the entrypoint you want to use.

[![07 - Action workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/07-action-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/07-action-workflow.yml)

This workflow will run an Action each time a `PUSH` event occurs on the repository. This specific action runs a Ritchie CLI formula.

[![08 - Outputs workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/08-outputs-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/08-outputs-workflow.yml)

This workflow illustrates how to set outputs in a job to use them on another job. This specific workflow prints `Hello-World`.

[![09 - Artifacts workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/09-artifacts-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/09-artifacts-workflow.yml)

This workflow illustrates how to pass data between jobs in the same workflow. For more information, see the [actions/upload-artifact](https://github.com/actions/upload-artifact) and [download-artifact](https://github.com/actions/download-artifact) actions. The full math operation performed in this workflow example is `(3 + 7) x 9 = 90`.

[![10 - Environment workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/10-environment-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/10-environment-workflow.yml)

This workflow illustrates how to use `environment` variables from the whole workflow, a specific job, or a specific step.

[![11 - Input workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/11-input-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/11-input-workflow.yml)

This workflow illustrates how to use `input` variables on a `workflow_dispatch` event.

[![12 - Run Workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/12-run-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/12-run-workflow.yml)

This workflow illustrates how to run a workflow once another specific one has been completed (with success or failure).

[![13 - Create Pull Request](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/13-create-pull-request.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/13-create-pull-request.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) to automatically create a Pull Request committing updated files.

[![14 - Auto Merge](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/14-auto-merge.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/14-auto-merge.yml)

This workflow illustrates how to automatically merge a Pull Request with a specific label `automerge`.

[![15 - Push Dev](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/15-push-dev.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/15-push-dev.yml)

This workflow only run when a push is made to the `dev` branch.
Note that with this implementation, the workflow needs to be present on the specific branch as well (here `dev`).

[![16 - Conditional](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/16-conditional.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/16-conditional.yml)

This workflow illustrates how to use conditional through the `if` variable.

[![17 - Issue Greeter](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/17-issue-greeter.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/17-issue-greeter.yml)

This workflow illustrates how to write an automatic comment on a new issue, without using action, through the github API.

[![18 - Specific File](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/18-specific-file.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/18-specific-file.yml)

This workflow illustrates how to trigger a workflow when specific files are updated by a `push` or `pull_request` event.

[![19 - Push Event](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/19-push-event.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/19-push-event.yml)

This workflow illustrates how use the [checkout action](https://github.com/actions/checkout) to create a push event, updating a file and committing it to the branch.

[![20 - Generate Patch Tag with Cherry Pick](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/20-generate-patch-tag-cherry-pick.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/20-generate-patch-tag-cherry-pick.yml)

This workflow illustrates how use cherry-pick to generate a new repository tag informing 3 inputs (`reference tag`, `new tag`, and `commit hash`).

[![21 - Generate Release Branch with Cherry Pick](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/21-generate-release-branch-cherry-pick.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/21-generate-release-branch-cherry-pick.yml)

This workflow illustrates how use cherry-pick to generate a new release branch informing 3 inputs (`reference tag`, `new tag`, and `commit hash`).

[![22 - Install runner tools](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/22-install-runner-tools.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/22-install-runner-tools.yml)

This workflow illustrates how to install tools not supported by the ubuntu runner using `apt-get install`.

[![23 - Upload reset Asset](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/23-upload-release-asset.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/23-upload-release-asset.yml)

This workflow illustrates how to upload a release asset. [Example]( https://github.com/GuillaumeFalourd/poc-github-actions/releases/tag/821d0256)

[![24 - Github Context](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/24-contexts.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/24-contexts.yml)

This workflow illustrates how to access various context variables on a workflow.

[![25 - Artifacts between Workflows 1](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/25-artifacts-between-workflows-1.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/25-artifacts-between-workflows-1.yml) [![25 - Artifacts between Workflows 2](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/25-artifacts-between-workflows-2.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/25-artifacts-between-workflows-2.yml)

These workflows illustrate how to share datas between various workflows using artifacts.

[![26 - Create branch on another repo](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/26-create-release-branch-other-repo.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/26-create-release-branch-other-repo.yml)

This workflow illustrates how to create a new branch on another repository based on the current repository tag.

[![27 - Check Tags](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/27-check-tags.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/27-check-tags.yml)

This workflow illustrates how to use outputs between jobs with the `needs` context to check tags and manage them to perfom some operation according to their name.

[![28 - Create Pull Request (Workflow)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/28-create-pull-request.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/28-create-pull-request.yml)

This workflow illustrates how to create a new Pull Request based on a branch name after a push event.

[![29 - Check Actor on PR or PUSH](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/29-check-actor-pr-or-push.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/29-check-actor-pr-or-push.yml)

This workflow illustrates how to add a comment on a new Pull Request based on the github actor name after a PR event.

[![30 - Webhook Release](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/30-webhook-release.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/30-webhook-releaseh.yml)

This workflow illustrates how to call a webhook on each release extracting the release tag.

[![31 - Untouchable file](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/31-untouchable-file.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/31-untouchable-file.yml)

This workflow illustrates how to close a Pull Request automatically if it updates on file that shouldn't be modified.

[![32 - PR approved and labeled](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/32-pr-approved-and-labeled.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/32-pr-approved-and-labeled.yml)

This workflow illustrates how to perform a specific action when approving a Pull request if it contains a specific label.

[![33 - Reusable workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/33-reusable-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/33-reusable-workflow.yml)

This workflow illustrates how to implement a [reusable workflow](https://docs.github.com/en/actions/learn-github-actions/reusing-workflows).

[![34 - Workflow Call](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/34-workflow-call.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/34-workflow-call.yml)

This workflow illustrates how to use and call a reusable workflow (cf workflow 33 above).
