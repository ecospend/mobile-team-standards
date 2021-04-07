## Commit Messages

Every commit message should start with User Story(US) ID that is created in Jira or Azure Devops. After US ID, commit message should continue, commit messages' subject line should be imperative mood. Capitalize the first word as commit message must be read like a sentence. A dash should be placed between US ID and commit message like:

```
<User Story ID> - Commit message
```

For more information that is about commit message standards, please read [this](https://chris.beams.io/posts/git-commit/)

### Capitalized Words
Every commit message should start with words
__BAD:__
```
<User Story ID> - add capitalized commit messages
```

__GOOD:__
```
<User Story ID> - Add capitalized commit messages
```

### Imperative Mood
Start commit messages with a verb, so there is a clear expectation of what action has been taken. This must be specified in the present tense.

__BAD:__
```
<User Story ID> - Removed ...
<User Story ID> - I fixed ...
```
__GOOD:__
```
<User Story ID> - Remove ...
<User Story ID> - Fix ...
```

### When Using Periods
Periods are only acceptable when commit messages span over multiple sentences.

__BAD:__
```
<User Story ID> - Remove unused dependencies.
```

__GOOD:__
```
<User Story ID> - Remove unused dependencies. These used to break the staging server.
```

### No Colons
Colons are verbose and break the sentence principle, so don’t use them.

__BAD:__
```
<User Story ID> - Remove unused dependencies: Ruby and JavaScript
```

__GOOD:__
```
<User Story ID> - Remove unused Ruby and JavaScript dependencies 
```
### 72 Characters Limit
The recommendation is to do this at 72 characters for the commit message body. By the way, GitKraken helps you for counting characters, keep it in mind, please. 

If you need more character for your commit message, please use the description area. No limit to the length of maximum allowed characters, as commit messages' `description` should be as detailed as possible for a better understanding.

## Message Structure

Include the User Story ID between brackets   - at the beginning of each commit message:

```
<User Story ID> - Commit message
```

This serves two main purposes:
1. Traceability of each commit which is very useful when rebasing, cherry-picking and merging.
2. Integration with our project management tool as commits will be displayed in the user story card.

* Commits of incomplete features must be appended with the suffix wip at the end of the commit message.

```
<User Story ID> - Commit message wip
```

## Best Practices

* Write clear, precise and meaningful commit messages. Think that there is a high chance that you or someone else will be reading this commit message a few years from now. What would you like to communicate to your future self or developer about?

```
<User Story ID> - Implement change because ...
<User Story ID> - Fix the error triggered by ... in the following situation ...
<User Story ID> - Set up the build process so that ...
```

* Stage file changes in a meaningful way i.e. commit changes for a group of files together with a good commit message. All staged files must correspond to the same change. If the commit message uses the word “and”, then this probably is a good indicator that the commit might need to be split it up into separate commits.

* Commit regularly to avoid losing any massive amount of changes while working continuously on a large task.
