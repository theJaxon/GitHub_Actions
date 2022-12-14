# GitHub_Actions
Learning about GitHub Actions for CI Workflows

### Core Components
#### Workflows
- A workflow may include **1 or more `jobs`**
- Triggered in response to **`Events`**

#### Jobs
- A Job may include **1 or more `Steps`**
- Defines a **Runner** (An execution Environment that can be either Mac, Windows or Linux)
- Jobs by default **Run in Parallel** (Unless it's specified otherwise)
- Can be conditionally executed
- A Job can contain the **`needs`** keyword to indicate it relies on another job (So that the execution become sequential)

#### Steps
- Execute a **`Shell Script` or an `Action`**
- An action can be your own script or 3rd party action
- Steps are executed `sequentially` and they can be conditonally executed

---

### [Workflow Triggers (Events)](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)
- The Type of event that causes the action to be triggered
- Can be for a reason like
  1. New commit (push)
  2. PR Created (pull_request) *NOTE: PRs based on Forks DO NOT Trigger a workflow
  3. New branch (create)
  4. New Repo Fork created (fork)
  5. New Issue opened (issues)
  6. New issue comment (issue_comment)
  7. Repository was starred (Watch)
  8. Discussion related (discussion)
  9. Manual trigger (workflow_dispatch)
  10. Workflow is scheduled (schedule)
  11. Workflow is called by other workflows (workflow_call)

- There can be multiple triggers defined ex: `on: [push, workflow_dispatch]

```yaml
# Trigger whenever a PR is created that target any of these branches
name: Test PR
on:
  pull_request:
    types:
    - opened
    branches:
    - main
    - 'dev-*'
    - 'feature/*'
```

---

### [Skip workflow runs via Commit messages](https://docs.github.com/en/actions/managing-workflow-runs/skipping-workflow-runs)
- Workflow runs triggered by the push and pull_request events can be skipped by including a command in commit message
- ex `[skip ci]` `[skip actions]`

#### Activity Types
- More detailed control over when a workflow will be triggered
- So you specify fine grained details like `pull_request` (opened, closed, edited)

#### Filters
- Give more detailed control over when a workflow will be triggerd just like Activity Types
- ex: on `push` to specific branch

---

### Actions
- An action is a custom application that performs a frequently repeated task

### [Contexts](https://docs.github.com/en/actions/learn-github-actions/contexts)
- Reserved keywords for accessing information about workflows
- Syntax used is `${{ <context> }}`

### [Expressions](https://docs.github.com/en/actions/learn-github-actions/expressions)
- Can be used to programmatically set environment variables in workflow files and access contexts
- Example `run: echo "${{ toJSON(github) }}"`

---

### Artifacts
- Outputs generated by a job (Binaries, log files etc)
- Can be Downloaded and used manually via Github UI or REST API
- Can be downloaded and used by some other jobs 

### [Job Outputs](https://docs.github.com/en/enterprise-server@3.4/actions/using-workflows/workflow-commands-for-github-actions)
- For re-using a value in different jobs (ex: file name generated in a previous build step)
- `set-output` is usually combined with `echo` command for storing the echo output ex: `::set-output name=script-file::`
- `needs` contains the outputs for all jobs

---

### Caching actions
- Relies on cache action
- A Path is provided where the files located there are to be cached
- A `Key` is constructed preferably with the hash of a specifc file so that based on changes in that file it's detected that cache should be invalidated

---

### Locally Testing with Act
```bash
# Run specific Workflow
act -W .github/workflows/checks.yml
```

---

### Custom Actions
#### Types of custom actions
1. JavaScript Actions - Execute JS File
2. Docker Actions - Create Dockerfile with required configuration
3. Composite Actions - Combine multiple workflow steps in 1 single action (`run commands` and `uses actions`) which allows for re-using shared steps