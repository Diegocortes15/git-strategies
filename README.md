# git-strategies

## GitLab Flow

[GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html) combines feature-driven development and feature branching with issue tracking.

With GitFlow, developers create a develop branch and make that the default while GitLab Flow works with the main branch right away.

GitLab Flow is great when you want to maintain multiple environments and when you prefer to have a [staging environment](https://www.flagship.io/test-environment/) separate from the production environment. Then, whenever the main branch is ready to be deployed, you can merge back into the production branch and release it.

Thus, this strategy offers propers isolation between environments allowing developers to maintain several versions of software in different environments.

While GitHub Flow assumes that you can deploy into production whenever you merge a feature branch into the main, GitLab Flow seeks to resolve that issue by allowing the code to pass through internal environments before it reaches production, as seen in the image below.
