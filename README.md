# git-strategies

## GitLab Flow

[GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html) combines feature-driven development and feature branching with issue tracking.

With GitFlow, developers create a develop branch and make that the default while GitLab Flow works with the main branch right away.

GitLab Flow is great when you want to maintain multiple environments and when you prefer to have a [staging environment](https://www.flagship.io/test-environment/) separate from the production environment. Then, whenever the main branch is ready to be deployed, you can merge back into the production branch and release it.

Thus, this strategy offers propers isolation between environments allowing developers to maintain several versions of software in different environments.

While GitHub Flow assumes that you can deploy into production whenever you merge a feature branch into the main, GitLab Flow seeks to resolve that issue by allowing the code to pass through internal environments before it reaches production, as seen in the image below.

### In practice

The flow starts with **main** branch, the **pre-production** enviroment branch, and the **production** enviroment branch. All these branches should be protected, for developers do not commit directly to them.

To start a new developmnet demand, you must create a specific branch for this demand and peridically pushes for branch of the same name to the remote repository.

Upon finalizing the demand, a _Merge Request_ for the master is requested. A code review can be opened in GitLab and a discussion about the change can be started

![](https://github.com/jadsonjs/gitlab-flow/raw/master/images/flow3.png)

A merge must then be made between the **master** branch and the pre-production environment branch. A pipeline should be executed to build the project and run the automated tests.

When passing in the automated tests, a merge must be done for the production branch. A pipeline should be executed again, to run the automated tests one more time and deploy to production.

A tag must be created to mark a stable version of the system and the feature branch must be removed to make the repository more organized.

![](https://github.com/jadsonjs/gitlab-flow/raw/master/images/flow6.png)

### Pros

- This flow guarantees a clean state in the branches at any point in the project life cycle.
- It defines how to do Continuous Integration and Continuous Delivery
- It is very flexible according to the team's decisions
- It is less complex than GitFlow Workflow

### Cons

- It is more complex than GitHub Workflow
- Git's history becomes unreadable due to the various Merge Requests between branches.
