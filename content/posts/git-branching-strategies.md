---
author: arul
category:
  - software-development
cover:
  alt: git-branching-flow-header
  image: /wp-content/uploads/2023/03/git-branching-flow-header-1.png
date: "2023-03-06T07:24:00+00:00"
guid: https://arulselvan.net/?p=671
tag:
  - git
  - strategy
  - technical
title: Git & Branching Strategies
url: /git-branching-strategies/

---
**What is Git?**

Git is a free and open-source distributed version control system just like any other version control system gives the developer power to track, manage, and organize their code. it's very popular among the developer community because of its lightweight and branching capability. Unlike centralized version control systems, Git branches are cheap and easy to merge.

**What is Branching Strategy?**  
 A branching strategy is a strategy that software development teams adopt when writing, merging, and deploying code when using a version control system.

Basically, It is a set of rules and workflow that developers can follow to stipulate how they interact with a shared codebase.

The git branching strategy is completely dependent on the team and environment, but below are some of the popular branching strategies suitable for most of the team.

- GitFlow
- GitHub Flow
- GitLab Flow
- Trunk-Based Development

**GitFlow:**

![](/wp-content/uploads/2023/03/image-773x1024.png)

Conceived in 2010 by Vincent Driessen

     The central repo will hold two main branches **master** and **develop** with an infinite lifetime.

**master** to be the main branch where the source code of `HEAD` always reflects a _production-ready_ state.

**develop** to be the main branch where the source code of `HEAD` always reflects a state with the latest delivered development changes for the next release,  Some would call this the “integration branch”, every feature is merged into this develop branch.


**feature**\*, **release**\*, and **hotfix**\\* are short-living support branches that will have only a limited lifetime and removed once the purpose is completed.

**feature**\\* branches (or sometimes called topic branches) are used to develop new features for the upcoming or a distant future release.

**release**\\* branches support the preparation of a new production release, like version bumping or any last minutes changes, once released planned release-related code is moved to the release branch, so the `develop` branch is cleared to receive features for the next big release.

**hotfix**\\* branches are very much like release branches in that they are also meant to prepare for a new production release, but unplanned. When a critical bug in a production version must be resolved immediately, a hotfix branch may be branched off from the corresponding tag on the master branch that marks the production version. The essence is that the work of team members (on the `develop` branch) can continue, while another person is preparing a quick production fix.

**Pros**

- Parallel development
- Multiple versions support source code
- The code in the main is updated only with code that has been thoroughly tested and refined

**Cons**

- could overcomplicate and slow the development process
- Not Ideal for a continuous delivery model

Ideal for the product need to develop multiple feature parallel with multiple versions or Open source where required strict access control

**Detail Reference**: [https://nvie.com/posts/a-successful-git-branching-model/](https://nvie.com/posts/a-successful-git-branching-model/)

**GitHub Flow:**

![](/wp-content/uploads/2023/03/image-1-e1678249659121-1024x284.png)

GitHub flow is a lightweight, branch-based workflow. GitHub says GitHub flow is useful for everyone, not just developers. For example, GitHub, they use for our site policy, documentation, and roadmap.

Unlike Git-Flow, GitHub-Flow involves no release branches. In the ideas of GitHub-Flow, once a code is merged with the master, its ready to go, it can be deployed to production and GitHub-Flow believes that hotfixes are identical to minor feature changes, so only there are two types of branches involved in this flow, the **master** branch, and the **feature** branch

Below are the basics steps involved in GitHub-Flow

- Create a new branch
- Make changes and add a commit
- Create a Pull Request for any discussion and review of the code
- Merging code with the master/main

**Pros**

- Focuses on Agile principles, encourages fast feedback loops
- allows for quick and continuous deployment, there is no development branch concept where finished features sit and wait for the release.
- Clear and simple collaboration rule

**Cons**

- Doesn’t support multiple version release branch
- Lack of dedicated develop branch, if not tested before the merge with main, susceptible to bugs in prod.
- emphasizes constant deployment, not ideal for the team parallelly develop multiple features and want to make larger release

Ideal For Products that required continuous deployment and release, such as SaaS products

**Detail Reference**: [https://docs.github.com/en/get-started/quickstart/github-flow](https://docs.github.com/en/get-started/quickstart/github-flow)

**GitLab Flow:**

![](/wp-content/uploads/2023/03/image-2.png)

GitHub flow assumes you can deploy to production every time you merge a feature branch. While this is possible in some cases, such as SaaS applications, there are some cases where this is not possible, such as:

- You don’t control the timing of a release. For example, an iOS application is released when it passes App Store validation.
- You have deployment windows - for example, workdays from 10 AM to 4 PM when the operations team is at full capacity - but you also merge code at other times.

In these cases, you can create a production branch that reflects the deployed code. You can deploy a new version by merging `main` into the `production` branch,If you need to know what code is in production, you can check out the production branch to see, this basically prevents the overhead of releasing, tagging, and merging that happens with Git flow

    GitLab is a simpler alternative to Git-Flow and but has proper isolation between environments, allowing developers to maintain several versions of software in different environments.

**Pros:**

- Compare to Git-Flow it's simple
- More organized and structured compared to GitHub
- The slight modification allows CI/CD

**Cons:**

- Not the simplest branch
- Can lead collaboration to messy
- can become very complex if you want to maintain multiple versions.

Ideal For Products that are demanding for quality, continuous deployment, and release, such as basic platform products or where you don’t have control over the release time like iOS app release

**Detail reference:** [https://docs.gitlab.com/ee/topics/gitlab\_flow.html](https://docs.gitlab.com/ee/topics/gitlab_flow.html)

**Scaled Trunk-Based Development**:

![](/wp-content/uploads/2023/03/image-3.png)

Trunk-based development paves the way for continuous integration as the trunk is kept constantly updated, normal trunk even don’t require a feature branch, and we can commit directly to the main, but the scaled trunk approach is equal to GitHub flow except for the release branch creation. After the release planning, if some bugs were identified they should be committed in the **master**(trunk) and only issues should be cherry-picked to the release branch.

**Pros**

- A key enabler of CI/CD allows for quicker releases
- Enhances collaboration
- Separate branch for release planning
- Better visibility

**Cons**

- Not suitable for a team with more Junior developers
- Limited control compare to git flow and GitLab

Mostly suited for all kinds of products

**Detail Reference:** [https://trunkbaseddevelopment.com/](https://trunkbaseddevelopment.com/)

**How to Choose the right Branching Strategy?**

Ultimately, the answer depends on you and your team’s environment, product, and specific development needs. Trunk based approach is very simple and suit for most of the use cases, but its fine to start off with any one strategy, then adapt it over time according to your specific needs :)
