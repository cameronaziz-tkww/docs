# 🧑‍🚀 Releasing

## Release Steps
1. Navigate to [Github released](https://github.com/tkww/TKMarketplace/releases) and determine `LAST_RELEASE`
   1. Find release with label `Latest release`
   2. `LAST_RELEASE` is the value next to the tag emoji, presented as 🏷️
2. Run changelog generator from root of application
  ```bash
    # Replace LAST_RELEASE with value determined on step 1
    make generate_release_notes last_release=LAST_RELEASE  
  ```
3. Determine version number with the following syntax `MAJOR.MINOR.PATCH`
     - Previous release should be reference to determine new version number
     - `MAJOR` should be incremented at the discretion of the team
       - It is primarily used when large features are being released
       - `MINOR` and `PATCH` should be set to `0`
     - `MINOR` should be incremented when release contains any branches tagged with `feature` or `chore`
       - `MAJOR` should not be changed
       - `PATCH` should be set to `0`
     - `PATCH` should be incremented in all other cases
       - `MAJOR` and `MINOR` should not be changed
4. Draft a new release through Github web UI
   1. Navigate to [Draft Release Page](https://github.com/tkww/TKMarketplace/releases/new)
   2. Populate form
   
     | Field                 | Value                                                                                                                                                                           |
     | --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
     | Tag Version           | `vMAJOR.MINOR.PATCH`, ex: `v1.2.3`                                                                                                                                              |
     | Target                | `develop`                                                                                                                                                                       |
     | Release Title         | A one line description of all code being released                                                                                                                               |
     | Describe this release | The output of the changelog generator, excluding all but `New Features Added`, `Fixed bugs` and `Merged pull requests` (everything below line 6, not including final two lines) |

5. A release branch should be cut off the current HEAD of the `develop` branch and follow this flow to release to staging
   1. Checkout `develop` and pull latest HEAD locally
      ```bash
      git checkout develop
      git pull
        ```
   2. Checkout new branch with the following syntax
      ```bash
      git checkout -b release/marketplace-web-MAJOR.MINOR.PATCH
      ```
   3. Push branch to origin to trigger CI/CD deploy to staging
      ```bash
      git push --set-upstream origin release/marketplace-web-MAJOR.MINOR.PATCH
      ```
6. Notify team of changes to staging
   1. Ensure release is on staging through [Jenkins Activity Log](https://pipelines.eng.theknotww.com/blue/organizations/jenkins/tkww%2FTKMarketplace/activity)
   2. Create message Slack
      - Populate message using the following syntax
      - `Tag Version` is on staging`, where `Tag Version` is the value populated when drafting release
        - Copy value in `Describe this release` from drafting release and wrap in code block with three backticks `` ``` ``
      - Tag message with key stakeholders
        - Engineering Team: `@mktpl-fe-eng`
        - QA Engineer: `@rchandler`
        - Product Manager: `@Gian-mical (GM)`
      - Post message to [marketplace-internal](https://theknotww.slack.com/archives/GBLPF9KNU)
7. Deploy Release 
   1. Wait for both QA Engineer and Product Manager to sign off on release
      If issues are presented, administer hotfix, [see below](#hotfixes) 
   2. Post message to [marketplace-internal](https://theknotww.slack.com/archives/GBLPF9KNU) with the value of `Deploying to Production`. Samuel Jackson wishes you luck
   3. Checkout release branch and pull latest HEAD to ensure there are no local changes
      ```bash
      git checkout release/marketplace-web-MAJOR.MINOR.PATCH
      git pull
      ```
   4. Checkout `main` branch and pull latest HEAD
      ```bash
      git checkout main
      git pull
      ```
   5. Merge release branch into `main`
      ```bash
      git merge release/marketplace-web-MAJOR.MINOR.PATCH
      ```
   6. Do not modify commit message, simply `ESCAPE` → `w` → `q` → `ENTER`
   7. Push release to production 🙌
      ```bash
      git push
      ```
8. Merge release branch into `develop`
   1. Checkout release branch and pull latest HEAD to ensure there are no local changes
      ```bash
      git checkout release/marketplace-web-MAJOR.MINOR.PATCH
      git pull
      ```
    1. Checkout `develop` branch and pull latest HEAD
      ```bash
      git checkout develop
      git pull
      ```
    2. Merge release branch into `develop`
      ```bash
      git merge release/marketplace-web-MAJOR.MINOR.PATCH
      ```
    3.  Do not modify commit message, simply `ESCAPE` `w` `q` `ENTER`
    4.  Push updated `develop` branch
      ```bash
      git push
      ```

## Hotfixes
Releases on staging that is being reviewed may present issues to the QA engineer or product manager. This will require a hotfix to be created and deployed
1. Checkout release branch with issues and pull latest HEAD
2. Checkout new branch with the following syntax `hotfix/ISSUE_PRESENTED` where `ISSUE_PRESENTED` is a brief description of the problem being solved, separated by dashes
3. Complete fix
4. Checkout release branch with issues and pull latest HEAD
5. Merge hotfix branch into release branch
6. Push to origin
