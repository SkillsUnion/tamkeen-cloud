# Pull Requests

## Learning Objectives

1. Know what Pull Requests are for Github
2. Know how to create pull requests in GitHub
3. Know how to leave comments on and merge pull requests in GitHub

## Introduction

A GitHub <a href="https://docs.github.com/en/free-pro-team@latest/github/collaborating-with-issues-and-pull-requests/about-pull-requests" target="_blank">**pull request**</a> (PR) is a request to merge or "pull" changes from 1 branch on GitHub to another. PRs are most commonly used for code review, where SWEs share PRs for peer review before merging that code to a `main` branch. Reviewers can comment on individual lines in the PR and request changes before the code is merged. We use PRs for student code submission and review.

![A pull request on Facebook's React repo](<../.gitbook/assets/0.3.1 - Pull Requests - 2 - Sample PR.png>) ![Reviewers can leave comments on pull requests to acknowledge good work and request changes](<../.gitbook/assets/0.3.1 - Pull Requests - 2 - Sample PR Comment.png>)

## How to create, comment on and merge pull requests

Below is a demo video for how to create, comment on and merge pull requests.

{% include youtube.html id="-m5ShISXdg8" %}
Demo video on how to create, comment on and merge pull requests

To create a pull request to merge a change from a feature branch to `main` (or any other branch), first push the latest changes from that feature branch from our local repo to GitHub.

Once the latest changes on that feature branch are in GitHub, we can navigate to the "Pull requests" tab in our repo's GitHub page and click "New pull request".

![Navigate to Pull requests tab and click New pull request to initiate new PR](<../.gitbook/assets/0.3.1 - Pull Requests - 1 - New PR.png>)

Verify we are merging the correct source and target branch, and correct commits and code changes. Once verified, click "Create pull request".

![Verify we have the correct branches and commits before creating pull request](<../.gitbook/assets/0.3.1 - Pull Requests - 1 - New PR 2.png>)

Leave a descriptive title and description for reviewers, then click "Create pull request".

![Leave descriptive title and description for each PR](<../.gitbook/assets/0.3.1 - Pull Requests - 1 - New PR 3.png>)

If you are a reviewer or want to leave comments for your reviewer, hover over the relevant line of code and click the "+" icon to leave a comment on that line. To comment on multiple lines, click and drag the "+" icon over the relevant lines.

![Click "+" icon to comment on 1 or more lines in the PR](<../.gitbook/assets/0.3.1 - Pull Requests - 1 - New PR 4.png>)

Once reviewers have approved the PR, click "Merge pull request" in the PR's Conversation tab to merge the relevant branches and close the PR.

![Once reviewers have approved, merge the PR to merge relevant branches and close the PR](<../.gitbook/assets/0.3.1 - Pull Requests - 1 - New PR 5.png>)

After merging the PR, we should see the merged code in the target branch, in this case `main`.

![Merged PRs have a "Merged" status](<../.gitbook/assets/0.3.1 - Pull Requests - 1 - New PR 6.png>) ![After merging, target branch should contain the latest changes](<../.gitbook/assets/0.3.1 - Pull Requests - 1 - New PR 7.png>)
