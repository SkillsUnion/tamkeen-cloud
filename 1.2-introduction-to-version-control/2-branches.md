# Branches

## **Learning Objectives: Git Branches**

1. Understand the purpose of Git branches and their role in enabling independent feature development without affecting production code.  
2. Learn how to create a new branch and switch between branches using Git commands.  
3. Gain proficiency in merging branches, including merging feature branches to `main` and vice versa, both locally and through GitHub.  
4. Develop strategies to handle and resolve merge conflicts effectively using tools like VS Code.  


## Introduction

A Git Branch is an independent series of commits. Every Git repo starts with a single branch, typically `main`, which we can imagine to be a linear series of commits.

![Every repo starts with the main branch by default](<../.gitbook/assets/0.2.1 - Branches - Single Branch.png>)

Using multiple branches allows software engineers to develop new features based on production code in `main` without affecting `main`, even after pushing to GitHub. We typically refer to non-`main` branches as "feature branches". Feature branches can be for changes as small as a typo and as large as new products.

Feature branches are independent series of commits that typically "branch" from `main` , and merge back into  `main` after we have completed and tested the new feature.

![Create and work on a feature branch when working on a new feature](<../.gitbook/assets/0.2.1 - Branches - Feature Branch.png>)

We can delete feature branches after merging them to `main`.

![Git state after merging feature branch to main. All commits from feature branch are copied to main, and Git adds an extra "merge commit" to resolve differences.](<../.gitbook/assets/0.2.1 - Branches - Merge Feature Branch.png>)

At large tech companies, 1000s of engineers can be working on independent feature branches that branch from `main` and merge back to `main` at different points in time.

## Create a branch

Create new branches with `git checkout -b`. `git checkout` is the command to switch, or "checkout" branches, and the `-b` flag creates a new branch and checks it out. Branch names use kebab-case (lowercase with hyphens between words) by default, and we will use `my-feature` as our example branch name.

```
git checkout -b my-feature
```

Verify we are on the new `my-feature` branch with `git branch`.

```
cloudengineering % git checkout -b my-feature
Switched to a new branch 'my-feature'
cloudengineering % git branch
  main
* my-feature
cloudengineering %
```

Now we can make commits on `my-feature` that build on the state of `main` when we created `my-feature`. Changes on `my-feature` will not affect any other branch in our repo.

## Change branch

While working on feature branches we may wish to periodically checkout other branches such as `main` to verify our changes are still compatible with theirs. To change back to the `main` branch, run `git checkout main`. We may also wish to `git pull` when on `main` to pull any new changes from GitHub to `main`. Run `git checkout my-feature` to go back to the `my-feature` branch.

## Merge feature branch to `main`

Once done with our feature on our feature branch, we can merge our changes to `main` for teammates and users to use. When working independently we can perform the merge locally, but when working in a team we typically perform the merge via GitHub to give teammates a chance to review our changes through a "pull request".

### Merge locally

1. Checkout the branch we want to merge into. For example, if we want to merge changes on our feature branch to `main`, checkout `main`.
2. Run `git merge` followed by the source branch name, e.g. `git merge my-feature`.
3. Git will combine commits from both branches and create a "merge commit" to resolve any differences. Run `git log` to view the merge commit and verify merge success.
4. Delete the feature branch locally with `git branch -d` followed by the feature branch name, e.g. `git branch -d my-feature`.
5. Once ready, push latest changes in `main` to GitHub.

### Merge on GitHub

1. Checkout and verify we are on our feature branch with `git branch`
2. Run `git push` to push latest commits from our feature branch to GitHub. If this is our first time pushing this feature branch to GitHub, we may have to run `git push --set-upstream origin` followed by our feature branch name, e.g. `git push --set-upstream origin my-feature`.
3. See instructions in [0.3.1: Pull Requests](../0.3-github/0.3.1-pull-requests.md) for how to create and merge a pull request in GitHub.

We may see the following output when pushing a feature branch to GitHub for the first time with `git push`. To resolve, enter the command Git suggests: `git push --set upstream origin my-feature`, where `my-feature` is the name of our feature branch.

```
cloudengineering % git push
fatal: The current branch my-feature has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin my-feature

cloudengineering % git push --set-upstream origin my-feature
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'my-feature' on GitHub by visiting:
remote:      https://github.com/the-cloud-engineering-22992299/aws/pull/new/my-feature
remote:
To https://github.com/the-cloud-engineering-22992299/aws.git
 * [new branch]          my-feature -> my-feature
Branch 'my-feature' set up to track remote branch 'my-feature' from 'origin'.
cloudengineering %
```

`upstream` refers to where our code should be hosted. `origin` refers to our GitHub repo or where we cloned our repo from. `my-feature` tells Git to create a new branch called `my-feature` in GitHub and by default push changes from the local `my-feature` branch to the GitHub `my-feature` branch.

After setting upstream once for a branch, we can run `git push` without arguments for subsequent pushes from this branch.

## Merge `main` to feature branch

In addition to merging feature branches to `main`, another common workflow is to merge latest changes from `main` into our feature branch. This minimises chances of merge conflicts when we merge our feature branch to `main`, especially if there have been big changes to `main` since we started our feature.

1. Checkout `main` with `git checkout main` and pull latest changes from GitHub with `git pull`.
2. Checkout our feature branch, e.g. `git checkout my-feature`.
3. Run `git merge main` to merge `main` into our feature branch. If we're lucky Git will merge the changes automatically. If not we will need to resolve merge conflicts manually.

## Merge Conflicts

{% include youtube.html id="56B7MOgm_CE" %}
Demo of how merge conflicts happen and how to resolve them

### What are merge conflicts and why do they happen?

Merge conflicts are situations when Git cannot automatically merge changes from 2 branches, for example if 2 branches change the same line of code differently. We can minimise merge conflicts by actively communicating with teammates to work on different files or functions, but generally merge conflicts are a standard feature of software engineering.

VS Code highlights differences in files with conflicts. The lines surrounded by `<<<<<<< HEAD` and `=======` are changes from the branch we are on, and the lines surrounded by `=======` and `>>>>>>> main` are changes from the incoming branch.

![Git will tell us where we have merge conflicts when we enter git status after merging. Within those files, VS Code will tell us which lines are in conflict, and we can click buttons above the conflict to resolve the conflicts.](<../.gitbook/assets/0.2.1 - Branches - Merge - Intro.png>)

### How to resolve merge conflicts

Once we have a merge conflict we must resolve it before writing new code, such that each commit in our commit history continues to describe a specific change. If we are unable to resolve conflicts now or merged by accident, we can abort merge with `git merge --abort`, which will revert our repo state to just before we ran `git merge`.

After Git tells us we have merge conflicts, use `git status` to confirm which files have conflicts.

Open each file with conflicts and resolve conflicts in each file by removing lines starting with `<<<<<<<`, `=======` and `>>>>>>>` and updating the code to what it should be. We can use VS Code's Accept Current/Incoming/Both Changes buttons and/or manually edit the files.

![VS Code gives us buttons above each conflict to conveniently resolve each conflict.](<../.gitbook/assets/0.2.1 - Branches - Merge - Resolve Conflict.png>)

Once we have resolved all conflicts, verify our app still works as expected. Once satisfied with our changes, `git add` the resolved files to add them to staging area for commit.

![Once we have resolved the conflict in the file we can git add to stage the file with conflicts for commit. We need to make a new commit to mark the conflict resolved.](<../.gitbook/assets/0.2.1 - Branches - Merge - Resolve Conflict 2 (1).png>)

Commit changes to finalise Git's merge commit and complete merge.

![Entering git commit after adding resolved files to staging area will open a commit message window. Save and close the file to complete commit.](<../.gitbook/assets/0.2.1 - Branches - Merge - Resolve Conflict (1).png>)

After committing, `git status` should no longer mention conflicts.

![Once we save the commit message file, we should see the commit completed.](<../.gitbook/assets/0.2.1 - Branches - Merge - Resolve Conflict 2.png>)

We can verify merge success by checking commit history in Git Logs with `git log`.

![We can verify successful merge by looking at Git Logs.](<../.gitbook/assets/0.2.1 - Branches - Merge - Resolve Conflict 3.png>)