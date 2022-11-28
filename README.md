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

#### Steps
- Execute a **`Shell Script` or an `Action`**
- An action can be your own script or 3rd party action
- Steps are executed `sequentially` and they can be conditonally executed

---

