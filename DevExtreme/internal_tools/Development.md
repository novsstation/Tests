---
title: Development
description: 
published: true
date: 2022-04-21T11:01:33.966Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:46:41.260Z
---

# Pull Requests

At first PR should be merged to the `dev` branch. After that the commit is cherry-picked to release branches.

#### Title and Commit Messages
Follow DevExtreme's [Commit Message & Pull Request Title Guidelines](https://github.com/DevExpress/DevExtreme/blob/22_1/README_DEVELOPERS.md#commit-message--pull-request-title-guidelines).

#### SemVer Label
PR should have either `internal` or one and only one [SemVer](https://semver.org/) label: `patch`, `minor`, `major`.
- `internal` updates do not affect public functionality
- `patch` updates include backwards compatible bug fixes and **do not break anything**
- `minor` updates add new functionality in a backwards compatible manner and **do not break anything**
- `major` updates make incompatible API changes. All PRs that require changes in other repositories or CI tasks must be marked with `major` label

#### Area Label
If it is possible, add one of these labels to specify the area affected by the changes: `Discovering`, `Integration`, `Topics`

#### Main PR Description
Main PR should have detailed description:

```markdown
### Cherry-picks
<!-- List here PRs to release branches -->

### Practical Value
<!-- Describe practical value of the changes suggested -->

### Before
<!-- Describe current behavior -->

### After
<!-- Describe how the behavior changes after this PR is merged -->
```

#### Cherry-Pick Name
Do not include main PR's number in the cherry-pick PR name:
> Add some change ~(#123)~

#### Cherry-Pick Description
Specify main PR in the description:
```markdown
Cherry-pick of #123
```

#### Version Bump Description
Add GitHub's [comparing-commits](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/viewing-and-comparing-commits/comparing-commits) link:

```markdown
### What's Changed
https://github.com/DevExpress/devextreme-internal-tools/compare/<LATEST_RELEASE_TAG>...<RELEASE_BRANCH>
```

# Branches
#### Foldering
Use folder prefix for you branches:
```
your-name/branch-name
```