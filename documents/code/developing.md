# 🛠️ Developing
## Branches
- Each unit of work should be on its own branch
- Branch names use the following syntax: `TYPE/DESCRIPTION-ISSUE`

  | Variable      | Description                                                          |
  | ------------- | -------------------------------------------------------------------- |
  | `TYPE`        | The type of change that is being committed, see below                |
  | `DESCRIPTION` | A short description of the change, each word separated by a dash `-` |
  | `ISSUE`       | The associated Jira issue number in lowercase, as `tkmp-1234`        |

  | Type      | Description                                                                                                                              |
  | --------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
  | `bug`     | A code change that resolves a bug that has no new user facing features                                                                   |
  | `feature` | A code change that implements, removes or changes a user facing feature                                                                  |
  | `chore`   | A code change that implements, removes or changes that has no user facing feature                                                        |
  | `revert`  | A code change that reverts a previously merged branch                                                                                    |
  | `release` | A code change that is to be deployed to staging, `DESCRIPTION-ISSUE` syntax is not followed, [see Releasing](./releasing.md)             |
  | `hotfix`  | A code change that is merged directly into a release branch, `DESCRIPTION-ISSUE` syntax is not followed, [see Releasing](./releasing.md) |
- Branch names should be in all lowercase
- Commits within branch should be informative but no syntax is required
## Pull Requests
- Pull requests should use the following syntax: `[ISSUE] DESCRIPTION`

  | Variable      | Description                                                   |
  | ------------- | ------------------------------------------------------------- |
  | `ISSUE`       | The associated Jira issue number in uppercase, as `TKMP-1234` |
  | `DESCRIPTION` | A short description of the change                             |
- Each pull request should reference one Jira
  - No code should be merged without an associated Jira issue
  - A single pull request should not reference multiple Jira issues
- If build is successful and all tests pass, a PR instance of the branch's code will be deployed
  - The URL has the following syntax, where `1234` is the PR number.\
    `https://mp-web-pr-1234.k8s.localsolutions.theknot.com/marketplace`
- Pull request should be tagged with the proper label
  | Type            | Description                                                              |
  | --------------- | ------------------------------------------------------------------------ |
  | `bug`           | A pull request that that is merging a branch with type `bug` or `revert` |
  | `feature`       | A pull request that that is merging a branch with type `feature`         |
  | `chore`         | A pull request that that is merging a branch with type `chore`           |
  | `hotfix`        | A pull request that that is merging a branch with type `hotfix`          |
  | `do not merge`  | A pull request that should not be merged in its current state            |
  | `do not review` | A pull request that should not be reviewed in its current state          |
## Approvals
- Two reviews are required before merging
- A message requesting reviews can be submitted to [mkpl-engineers-sloth](https://theknotww.slack.com/archives/G474PGVKP) to request
  - Tag `@mktpl-fe-eng` to notify engineers
  - Provide link to pull request
- Pull requests should be tested by the QA engineer before merging
  - Moving the associated Jira issue into the `Ready for QA` status will notify the QA engineer
  - If successful, the QA engineer should move the associated Jira issue to the `Ready to Merge into QA-Beta` status
  - An engineering QA can be requested if no feature is testable by QA Engineer
## Merging
- Pull request should be merged into `develop` branch to deploy on QA
- Once merged, work should be tested by the QA engineer
  - Moving the associated Jira issue into the `Ready for Regression` status will notify the QA engineer
  - If successful, the QA engineer should move the associated Jira issue to the `Verified on QA-Beta` status
  - If unsuccessful, the QA engineer should move the associated Jira issue to the `Rejected on QA-Beta` status, [see below](#rejected-on-qa-beta)
  - An engineering QA can be requested if no feature is testable by QA Engineer
## Rejected on QA Beta
- If work is rejected on QA Beta, it is the engineer who merged the code responsibility to resolve the issues
- There are two options to resolve the issues
  As code in QA Beta that has been rejected blocks any release of code, the engineer has the responsibility to assess which solution is ideal without slowing down releases 
  - **Revert Code** - *Faster to fix QA Beta*\
     Code that is merged into QA Beta is reverted with a new revert commit. This will then allow current code in the `develop` branch to be released. This relies on git logic and may not be successful if merge with issues is not the most recent merge
    1. Checkout `develop` and pull latest HEAD locally
        ```bash
        git checkout develop
        git pull
          ```
    2. Checkout new branch with the same [branch name](#branches) with the `type` changed to `revert`
        ```bash
        git checkout -b revert/short-description-tkmp-1234
        ```
    3. Push branch to origin and open new pull request and follow [approvals](#approvals) and [merging](#merging) flow
    4. Checkout new branch to resolve issues presented by QA engineer and follow normal [approvals](#approvals) and [merging](#merging) flow
  - **Fix Code** - *Faster to fix issues*\
    A new branch to resolve issues is checked out and issues are resolved. This option should only be chosen if the solution is apparent and time required is reasonable to not prevent a release
    1. Checkout new branch to resolve issues presented by QA engineer and follow normal [approvals](#approvals) and [merging](#merging) flow
   
