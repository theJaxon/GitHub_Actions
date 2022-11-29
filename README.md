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
  2. PR Created (pull_request)
  3. New branch (create)
  4. New Repo Fork created (fork)
  5. New Issue opened (issues)
  6. New issue comment (issue_comment)
  7. Repository was starred (Watch)
  8. Discussion related (discussion)
  9. Manual trigger (workflow_dispatch)
  10. Workflow is scheduled (schedule)
  11. Workflow is called by other workflows (workflow_call)

---

### Actions
- An action is a custom application that performs a frequently repeated task