# GitHub

## Learning Objectives: GitHub

1. Understand the purpose of GitHub and its features for collaborative software development.  
2. Learn how to fork a repository to create an independent copy of a GitHub repo.  
3. Use `git clone` to download a local copy of a repository for editing.  
4. Gain proficiency in pushing local changes to GitHub using `git push` and pulling changes from GitHub using `git pull`.  
5. Learn how to view commit history on GitHub to track and analyze changes over time.  

## Introduction

GitHub is a code-hosting website that hosts Git repos for individuals or teams to review and collaborate on. Team members can easily review latest code changes and commit history, making software development more transparent and thorough.

---

{% include youtube.html id="HkdAHXoRtos" %}

---

## GitHub Workflow Summary

1. **Fork** repos we do not have edit access to to suggest changes or maintain our own copy
2. **Clone** repos to download local copies of GitHub repos
3. Once we have committed the changes we want locally, **push** our changes to GitHub to share them with others. Refresh the GitHub repo page to see those changes.
4. If we are working with teammates and wish to download their code while keeping local changes, **pull** their code from GitHub after committing our local changes.

## GitHub Fork

A GitHub "fork" is a copy of another GitHub repo. SWEs typically "fork" repos they do not have edit access to either to make improvements to merge back into original repos, or to create and maintain independent versions of repos. 

We can fork a repo by clicking the Fork button on a GitHub repo page. Once forked, we can change our copy of the repo without affecting the original.

![Click the Fork button to fork a repo](<../.gitbook/assets/0.3 - GitHub - 1) Fork.png>)

![Fork menu; We typically keep the same repo name for clarity](<../.gitbook/assets/0.3 - GitHub - Fork - 2) Fork menu.png>) ![Forked repo; Notice the repo is now under my account](<../.gitbook/assets/0.3 - GitHub - Fork - 3) Forked repo.png>)

## Git Clone

Once we have edit access to the repo we want to edit, either by forking an existing repo or <a href="https://docs.github.com/en/get-started/quickstart/create-a-repo" target="_blank">creating a new repo</a>, we can "clone" (i.e. download) that repo to our local machine to make changes to it.

Click the copy button in the Code dropdown menu on the GitHub page of the repo we wish to edit.

![Click the copy button in the Code dropdown to copy the repo link to use with git clone](<../.gitbook/assets/0.3 - GitHub - Clone.png>)

Then go to terminal, `cd` to the relevant folder and enter the command `git clone <repo-url>`, where `<repo-url>` is the URL we just copied from GitHub. This will create a new folder named after the repo with the repo's contents inside.

```
ce % git clone https://github.com/aws-samples/aws-cdk-examples.git
Cloning into 'react'...
remote: Enumerating objects: 203678, done.
remote: Total 203678 (delta 0), reused 0 (delta 0), pack-reused 203678
Receiving objects: 100% (203678/203678), 173.82 MiB | 5.85 MiB/s, done.
Resolving deltas: 100% (144768/144768), done.
ce %
```

Once we've cloned the repo we can make edits to it and track our changes with Git.

## Git Push

`git push` allows us to share local changes by "pushing" local commits to GitHub for others to view. Video demo below.

{% include youtube.html id="BJojbCFfOHU" %}
Demonstration of how to push local changes to GitHub

## Git Pull

`git pull` allows us to download new changes in a shared GitHub repo (e.g. by teammates) while keeping our local changes. Git will automatically merge downloaded and local changes, and let us know if there are "merge conflicts", for example if downloaded and local changes edit the same lines of code. We will work more with `git pull` once we start group projects.

## How to view commit history in GitHub

GitHub provides an easy way to view past changes to a repo. For example, if we are wondering which commit changed a line of code that caused a bug, we can easily find which commits changed that line, who made those commits and what other changes were in those commits.

![Click the number of commits on a repo's GitHub page to view a list of all its commits](<../.gitbook/assets/0.3 - GitHub - 1) View Commits.png>)

![Click on any commits in the repo's commit history to view the details of that commit](<../.gitbook/assets/0.3 - GitHub - 2) Commit List.png>)

![We can review complete details of each commit in GitHub](<../.gitbook/assets/0.3 - GitHub - 3) Commit Contents.png>)

## Additional Resources

1. <a href="https://blog.red-badger.com/2016/11/29/gitgithub-in-plain-english" target="_blank">Git and GitHub in Plain English</a> (blog post)
2. <a href="https://youtube.com/playlist?list=PLRqwX-V7Uu6ZF9C0YMKuns9sLDzK6zoiV" target="_blank">Git and GitHub by The Coding Train</a> (video playlist)
