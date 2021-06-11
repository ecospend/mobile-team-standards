
## Code Review

Code reviews are critical to ensuring quality and efficiency in our software development process. We aim for 100% code contribution review coverage by utilizing pre-merge pull requests (PRs) to review code as it is integrated into the main development branches of the repository.

## Goals

There are two main goals with respect to code reviews:

* Facilitate a shared understanding of the codebase and foster a collective ownership of the project.
* Improve the quality of the code as much as possible (i.e. 2/3/4 brains are better than 1).

As you probably know, software issues cost more to fix later in the software development lifecycle. Code reviews serve as the first line of defense, helping to find and correct problems as early as possible.

## Guidelines for authors
### Pre-PR Checklist

Before creating the pull request, make sure to do the following:

1. Review your own code. Ideally, you're doing this with each commit that you make in addition to a final look when previewing the PR.
2. Integrate the latest changes by merging `develop` into your `feature/*` branch.
3. Make sure to address any outstanding `TODO`s or commented out code that you intended to clean up.
4. Make sure there are no new compilation warnings or errors. Don't break the build!
5. Make sure all of the unit tests pass.

### Creating the PR

1. Author creates a PR from their `feature/*` branch into `develop`.
2. The repository should be configured to automatically add default reviewers to each PR, but if there is anyone missing, the author should make sure to add them manually.
3. The description of the pull request must abide by this [template](pull_request_template.md).
4. If not previewed during the PR creation process, the author should immediately perform a self-review after the PR is created to spot and fix any final details before others start reviewing.
5. The name of the pull request must contain both the user story ID and title: `<User Story ID> - User Story Title`
6. Do NOT wait to complete all requirements before opening a pull request. In theses cases, prepend the suffix WIP - to the pull request title: `[WIP] <User Story ID> - User Story Title`

### PR Feedback Process

1. Reviewers review the code, adding comments and suggestions for improvements.
2. The author implements the suggested feedback or starts a discussion in order to get clarification or provide an alternate opinion.
3. Once satisfied with the implemented improvements (if any), the reviewer "approves" the PR.

### Merging the PR

1. Once all required reviewers have approved the PR, the author merges the PR.
2. Once merged, the `feature/*` branch can be removed.
3. After merging, the author should build and run the app to verify functionality one last time. This is especially important if there were merge conflicts that had to be resolved before the merge.
4. After merging, the author is also responsible for updating the relevant ticket(s) in the sprint board as well.

## Guidelines for reviewers
### Processing a pull request

* Each PR should be reviewed within one day. But it’s ok for PR authors to ask for a speedier code review on Slack
* Each PR should be merged within 5 days i.e. during the current sprint or next sprint at most. Stale PRs are usually hard to merge past this time range and require difficult rebase.
* Approve the PR by using the review tool of version control service (Github, Bitbucket or Gitlab).
* Merge once you feel confident in the code and its impact on the project.
* Merging requires a minimum of two review approvals. On large squads with over two developers, the approvals must include at least the Team Lead and/or one senior team teammates to avoid merges with approvals from only junior teammates.

### Giving feedback

* Comment directly on the line of code in the web interface of the version control service (Github or Azure DevOps)
* Use an inquisitive tone, do not make an order:

__BAD__:
```
`@user_id` -> Change this variable name to "NEW_VARIABLE_NAME"
```
__GOOD__:
```
`@user_id` -> What do you think about naming this "NEW_VARIABLE_NAME"?
```
* Ask for clarification e.g. I didn't understand. Can you please explain?
* Avoid selective ownership of code. (mine, not mine, yours)
* Accept that many programming decisions are opinions. Engage a discussion and reach a resolution quickly.
* Seek to understand the author’s perspective.
* Identify ways to simplify the code while still solving the problem.
