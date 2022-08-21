# git-strategies

<<<<<<< HEAD
## Git Flow

Git flow is a branching strategy created by [Vincent Driessen](https://github.com/nvie). It enables parallel development where developers can work separately from the master branch on features where a feature branch is created from the master branch. Afterwards, when changes are complete, the developer merges these changes back to the master branch for release. 

This branching strategy consists of main branches and support branches.

- **Main branches**    
    - `master`: This branch contains production code. All development code is merged into `master` in sometime.
    - `develop`: This branch contains pre-production code. When the features are finished then they are merged into `develop`.  

-  **Support branches**
   -  `feature`: Feature branches are used to develop new features for the upcoming releases. May branch off from `develop` and must merge into `develop`.
   -  `hotfix`: hotfix branches are necessary to act immediately upon an undesired status of `master`. May branch off from `master` and must merge into `master` and `develop`.
   -  `release`: Release branches support preparation of a new production release. They allow many minor bug to be fixed and preparation of meta-data for a release. May branch off from `develop` and must merge into `master` and `develop`.

### In practice

- New development (new features, non-emergency bug fixes) are built in `feature` branches.  
- `Feature` branches are branched off of the `develop` branch, and finished features and fixes are merged back into the `develop` branch when they’re ready for release.  
- When it is time to make a release, a `release` branch is created off of `develop`.  
- The code in the `release` branch is deployed onto a suitable test environment, tested, and any problems are fixed directly in the `release` branch. This deploy &rarr; test &rarr; fix &rarr; redeploy &rarr; retest cycle continues until you’re happy that the release is good enough to release to customers.  
- When the release is finished, the `release` branch is merged into `master` and into `develop` too, to make sure that any changes made in the `release` branch aren’t accidentally lost by new development.  
- The `master` branch tracks released code only. The only commits to `master` are merges from `release` branches and `hotfix` branches.  
- `Hotfix` branches are used to create emergency fixes.  
- They are branched directly from a tagged release in the `master` branch, and when finished are merged back into both `master` and `develop` to make sure that the hotfix isn’t accidentally lost when the next regular release occurs.  

![Git flow diagram](https://i.ibb.co/dgbP6Lj/GitFlow.jpg)

### Pros

- It allows for parallel development to protect the production code so the main branch remains stable for release while developers work on separate branches.
- The various types of branches make it easier for developers to organize their work.
-  Ideal when handling multiple versions of the production code.

### Cons
- As more branches are added, they may become difficult to manage as developers merge their changes from the development branch to the main.
- It could become increasingly difficult to figure out where exactly an issue is.
- It is not an efficient approach for teams wanting to implement continuous integration and continuous delivery.
=======
## Contents

- [GitHub Flow](#github-flow)
- [GitLab Flow](#gitlab-flow)

## GitHub Flow

[GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow) is established on creating branches around features and 
deploying often through Main.

Whereas Git Flow focuses on keeping an alternate environment found in a dev branch, GitHub Flow makes use of a more direct and agile approach by merging (and deleting thereafter) completed working branches into main and assuming that whenever the prior happens then Main is ready for deployment.

Having less intermediate steps, GitHub Flow favours simplicity and ease of use over thorough control, but that doesn't mean that is doesn't have tools to help maintain a proper production environment. Before any changes can be done to Main, merges from branches must go through a Pull Request such that they can be reviewed for functionality, quality and correctness before they are introduced and deployed.

As such GitHub Flow is a workflow that is extremely easy to pick up and follow, which also provides some deployment guidelines to ensure quality and agility making it a popular choice for development projects.

### In practice

The flow starts with the **main** branch which becomes the base for future branches made with the purpose of developing new features.

Once a _feature branch_ has finalized its development process, a Pull Request must be made in order to bring its changes over to **main**. Since the new changes are to be deployed once the Pull Request is approved, most of the times project directives are set in place such that there needs to be a review and subsequent green light provided by teams like QA in order to proceed with the merge.

![](https://i0.wp.com/build5nines.com/wp-content/uploads/2018/01/GitHub-Flow.png?fit=900%2C310&ssl=1)

When the feedback has been discussed and implemented, the final version in the _feature branch_ is evaluated via testing and if there are no problems then the merge is carried out to **main** and promptly deployed.

### Why use GitHub Flow?

[How GitHub Flow works and when to choose it](https://githubflow.github.io/)

### Pros

- Its simple which makes it easy to understand and apply.
- It allows its old and new users to hit the ground running which also increases they're chances of mastering additional tools to improve its effectiveness and quality.
- It favours agile projects that require constant deployment and generation of value.
- It incentivizes consensus on the quality and the need of changes through the use of Pull Requests.

### Cons

- Its less strict and it initially lacks tools to secure control over a project.
- It could be considered volatile compared to other Flows due to its fast deployment.
- Its not the best fit for projects that ship more infrequently.
>>>>>>> main

## GitLab Flow

[GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html) combines feature-driven development and feature branching with issue tracking.

With GitFlow, developers create a develop branch and make that the default while GitLab Flow works with the main branch right away.

GitLab Flow is great when you want to maintain multiple environments and when you prefer to have a [staging environment](https://www.flagship.io/test-environment/) separate from the production environment. Then, whenever the main branch is ready to be deployed, you can merge back into the production branch and release it.

Thus, this strategy offers proper isolation between environments allowing developers to maintain several versions of software in different environments.

While GitHub Flow assumes that you can deploy into production whenever you merge a feature branch into the main, GitLab Flow seeks to resolve that issue by allowing the code to pass through internal environments before it reaches production, as seen in the image below.

### In practice

The flow starts with **main** branch, the **pre-production** environment branch, and the **production** environment branch. All these branches should be protected, for developers do not commit directly to them.

To start a new development demand, you must create a specific branch for this demand and periodically pushes for branch of the same name to the remote repository.

Upon finalizing the demand, a _Merge Request_ for the main is requested. A code review can be opened in GitLab and a discussion about the change can be started

![](https://github.com/jadsonjs/gitlab-flow/raw/master/images/flow3.png)

A merge must then be made between the **main** branch and the pre-production environment branch. A pipeline should be executed to build the project and run the automated tests.

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
