# Practices: Git

## Description
This convention is applied for:
* Commiting on a branch: long-lived or short-lived branches,
* Pull Request: edit the commit message before validating the PR, especially in Azure DevOps where the default commit message is awful.

## Tools
- [Git](https://git-scm.com/)
- For commit signing: [Gpg4win](https://www.gpg4win.org/) that includes `Kleopatra` for managing certificates
```bash
git config commit.gpgsign false # disable signing in repository
git config --global commit.gpgsign true # enable signing globally
```
Note: Good practice -> Enable signing by default.
## Practice

### Commit Format
```
<type>[optional scope]: <description>

[optional body]

[optional footer]
```

Examples:
* Option 1: Add a blank between description, body and footer:
```bash
git commit -m "description
>
> Body
>
> Footer"
```
* Option 2: use `-m` option for each section
```bash
git commit -m "type(scope): description" -m "body" -m "Footer"
git commit -m "type: description" -m "body"
git commit -m "type!: description"
```

### Type

| Type | Description
|---|---|
| ! | Breaking change. The ! character is set after specifying the type/type(scope)<br /> "BREAKING CHANGE:" can be added into the commit footer to give more details.
| build | Commit that affects the build system or external dependencies (npm, NuGet packages, etc) |
| chore | No production code change: update current app version |
| ci | Changes to CI configuration files and scripts (Azure Pipeline files, GitHub actions, Circle, etc) |
| docs | Commit only affects documentation (readme, changelog,...) |
| feat | A new feature |
| fix | A bug fix |
| perf | Commit dedidicated to improve performance, without changing feature behavior |
| refactor | Improve code without fixing bug/adding feature/changing application behavior |
| revert | Used to indicate a reverse commit:
| style | Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc) |
| tech | Can be used to setup technical elements (services, database...) before working on a feature.<br />Normally the tech elements should be done at same time than a feature, but sometimes we have to split it for some team organizational reasons. |
| test | Add/update/fix tests |

### Scope
Can be used to define the scope of the commit. No specific rule, it will depend on the project I worked on.

Example:
```git commit -m "feat(notification): notify user his request has started processing"```
Indicates the commit is a feature related to notification service (scope) that will notify user the request is in progress.

### Body
Can be used to:
* Describe in more details what was done,
* Remind the related work item full name/description.

### Footer
Can be used to specify:
* `BREAKING CHANGE: <description>`: a breaking change,
* `Refs: #<Id>, #<Id2>`: declare the work item related to the commit,
* `Refs: SHA1, SHA2`: the commit SHAs reverted.

## Sources
The following sources were used to define my practice:
* [Angular - Commit Message Guidelines](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)
* [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)