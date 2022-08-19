# git-strategies

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

![](https://nvie.com/img/git-model@2x.png)

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
