## Exercises

### Create feature branch and merge to `main` without merge conflicts

1.  Create a new repo.

    ```
    mkdir poems
    cd poems
    git init
    ```
2. Create a poem about water in `water-poem.txt`. Commit this file to the repo.
3.  Create and checkout a new branch to edit the water poem.

    ```
    git checkout -b water-poem-edits
    ```
4. Edit the water poem and commit it to the new branch you just created.
5.  List all branches.

    ```
    git branch
    ```
6.  Checkout `main`.

    ```
    git checkout main
    ```
7. Verify `water-poem.txt` has reverted to the version on `main`.
8. Create a new poem about sandwiches in a new file and commit it.
9.  Checkout the water poem branch.

    ```
    git checkout water-poem-edits
    ```
10. Verify the sandwich poem does not exist in the water poem branch.
11. Checkout `main` and merge the water poem edits from the water poem branch.
12. Verify `water-poem.txt` contains changes from the water poem branch.
13. Delete the water poem branch with `git branch -d water-poem-edits`.

### Resolve Merge Conflicts

1. Start from the same repo as the previous exercise.
2.  Make a new branch for edits to the sandwich poem.

    ```
    git checkout -b sandwich-poem-edits
    ```
3. While on the sandwich branch, add a line to the poem and change the line that's currently there.
4. Commit the changes on the sandwich branch.
5. Checkout `main`. To create a merge conflict we will commit new changes to the same lines on the `main` branch.
6. Make a change to the sandwich poem and commit it.
7. Merge the sandwich branch into `main`.
8. We should observe a merge conflict.
9. Open the sandwich poem file to see merge conflict symbols from Git.
10. Resolve the merge conflict as per instructions above.
