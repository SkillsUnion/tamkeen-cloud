## Exercise: Git Poetry

The following exercises should help familiarise you with Git. We use text instead of code, but the Git functionality is the same. You may wish to have 3 windows open on your screen: VS Code, the Git Commands table above, and the following instructions.

1. Open today's folder in terminal and create a folder with the command `mkdir`
2. `cd` into the folder, and initialise it as a git repo using the command `git init`
3. Create a text file in the command line using `touch spring-poem.txt` and open it in VS Code with `code spring-poem.txt`
4. Write a poem about spring (or anything) in `spring-poem.txt` and save the file
5. Stage and commit `spring-poem.txt` with `git add .` and `git commit -m`
6. Edit our poem to reference leaves (or anything). Stage and commit the edits
7. Add a 2nd poem about winter (or anything) in a new file `winter-poem.txt`
8. Add a title to our spring poem above the poem in the file
9. Commit the latest changes to `winter-poem.txt` and `spring-poem.txt` in 2 commits by adding 1 of them to the staging area and committing before adding the other
10. Use `git log` to review commits in our repo