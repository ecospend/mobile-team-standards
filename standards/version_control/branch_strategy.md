# Branching Strategy

All projects at Ecospend Mobile Team will follow the [Gitflow](https://nvie.com/posts/a-successful-git-branching-model/) pattern for branching. More recently, some projects have experimented that environmental branching like *test* or *pre-prod*, but Gitflow is the standard for all new projects and also old ones will follow it in the future.

## Branching Models

### Gitflow

Gitflow is a branching model that organizes a repository into distinct branches, each with a unique purpose. It facilitates the ability to generate quality software via a stable release and development process.

![Gitflow branching strategy diagram](images/git-flow.png)
*[Diagram created by Vincent Driessen](https://nvie.com/posts/a-successful-git-branching-model/)*


### Branches Overview


| Branch        | Protected? | Base Branch | Description    |
| :-------------|:-----------|:------------|:---------------|
| `master`      | YES        | N/A         | What is live in production (**stable**).<br/>A pull request is required to merge code into `master`. |
| `develop`     | YES        | `master`    | The latest state of development (**unstable**). |
| feature       | NO         | `develop`   | Cutting-edge features (**unstable**). These branches are used for any maintenance features / active development. |
| `release/*` | NO      | `develop`    | A temporary release branch that follows the [semver](http://semver.org/) versioning. This is what is sent to UAT for QAs.<br/>A pull request is required to merge code into any `release/*` branch. |
| `bugfix/*`        | NO         | `release/*` | Any fixes against a release branch should be made in a bug-fix branch. The bug-fix branch should be merged into the release branch and also into develop. This is one area where we’re **deviating** from GitFlow. |
| `hotfix/*`    | NO         | `master`    | These are bug fixes against production.<br/>This is used because develop might have moved on from the last published state.<br/>Remember to merge this back into develop and any release branches. |

#### Branches

##### master

* Each commit in `master` (i.e. it is called `main` now) should reflect a stable release and be tagged with that release's version number.
* The latest commit in `master` reflects the build currently available in the App Store/Google Play.
* Until the first version of the app is released, `master` will usually reflect the initial state of the repository.

##### develop

* The main development branch, which reflects the most current **non-shipped** version of the app.
* Serves as the main integration point for new features/fixes as they are developed.
<!--- * The CI system points to `develop` by default, with QA performing the bulk of their testing on builds created from this branch.--->

##### feature/*

* Represents a feature or fix actively in development (e.g. `feature/UserStorID`).
* Initially branched from `develop` to start feature work.
* As the feature is developed, `develop` should be merged into `feature/*` periodically to keep the feature branch up-to-date with the latest changes.
* Once the feature is complete, the `feature/*` branch is merged into `develop` (via pull request) and then **removed**.
* Prefix the branch title with the backlog item ID when using project management tools such as JIRA and Azure DevOps. 
    <!--- TODO: For branching sub tasks, firstly it will be discussed with the team. --->
    
    __Bad:__
    ```
    SPD-171/feature/request-payment
    ```
    __Good:__
    ```
    feature/SPD-171
    ```

##### release/*

* Represents a release candidate (e.g. `release/2.1.0`).
* Initially branched from `develop` to start a code freeze process.
    * Only **bugfixes** should be merged into the `release/*` branch (i.e. no merging from `feature/*` branches).
* Merged into `develop` periodically so that fixes get incorporated into new feature development.
* Merged into `master` and tagged using [semantic versioning](https://semver.org/) once a release is complete (i.e. the app/update is live).
* Merged into `develop` one last time before being removed.

##### hotfix/*

* Represents a "hotfix" update used to quickly address issues with the live app.
* Initially created from the corresponding version number tag on the `master` branch (e.g. `2.1.0` --> `hotfix/2.1.1`).
* Allows for production issues to be resolved quickly without interrupting active feature development or having to manually cherry-pick or re-apply fixes from `develop`.
* Follows the same process as a `release/*` branch to keep `develop` up-to-date with any fixes and finalize the hotfix release.

##### bugfix/*

* Represents a bug is found that has not been deployed on production yet.
* Initially branched from `release/*` to start bug-fix work.
* Allows for release issues to be resolved quickly without interrupting active feature development.
* Once the feature is complete, the `bugfix/*` branch is merged into `release/*` (via pull request) and then **removed**.

#### TL; DL

1. The repo is created with only a `master` branch, by default.
2. A `develop` branch is created from `master`.
3. `feature/*` branches are created from `develop`.
4. When a feature is complete, it's merged into `develop` (via PR) and then removed.
5. To initiate a release, a `release/*` branch is created from `develop`.
6. When a release is complete, `release/*` is merged into `develop` and `master`, tagged, and then removed.
7. If an issue in `master` needs to be resolved, a `hotfix/*` branch is created from `master`.
8. When the hotfix release is complete, `hotfix/*` is merged into `develop` and `master`, tagged, and then removed.

## Branch Naming

Branch naming is left mostly up to the discretion of the person creating the branch
with a few exceptions. `master` and `develop` are always named exactly that. Prefix the branch title with the backlog item ID when using project management tools such as JIRA and Azure DevOps. 

__Bad:__
```
SPD-171/feature/request-payment
feature-name-validating-job
listing-bug
```
__Good:__
```
feature/SPD-171
bugfix/VAL-35
hotfix/OD-122
```

<!--- TODO: Discuss for branching sub tasks with the team. --->
<!--- TODO: Discuss for version update branches with the team. --->

## Commits

**Commit early, commit often!** Try to remember to push any pending commits to the remote repo at the end of every day so that all in-progress work is backed up.

Commit messages should be detailed and helpful - avoid anything that's not a complete sentence. You should aim to tell a story in the commit message (i.e. what was broken and how it was fixed). A good rule of thumb to follow is to begin commit messages with a verb so that the message completes the phrase "This commit...".

## Merging

All merges into `develop`, `release/*`, and `hotfix/*` should happen via pull requests. This ensures that all code gets reviewed at some point before it's shipped. For more information, see [Code Review Standards](../code_review.md).

## Deleting Branches

Branches should be deleted after they've been merged into `develop` or `master`. This keeps the repository clean and makes it clear where active development is occurring.
