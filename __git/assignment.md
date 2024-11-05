## **Objective:**
Complete a personal project using the command line, Git, branching, and GitHub. This assignment will guide you through setting up a project, managing different features in branches, and utilizing GitHub for version control and history tracking.

---

### **Instructions:**

#### **Part 1: Repository Setup**
1. **Initialize a Git Repository:**
   - Open your terminal.
   - Create a new directory for your project (e.g., `my_project`).
   - Navigate into the directory and initialize it as a Git repository using `git init`.
   - Create a `README.md` file that describes the project.
   - Add and commit the `README.md` file to the repository using `git add README.md` and `git commit -m "Initial commit with README"`.

2. **Push to GitHub:**
   - Create a new repository on GitHub named `my_project`.
   - Connect your local repository to the GitHub repository using `git remote add origin <repository-url>`.
   - Push your initial commit to GitHub using `git push -u origin main`.

---

#### **Part 2: Feature Development in Branches**
1. **Create a New Feature Branch:**
   - Create a new branch called `feature-update` using `git checkout -b feature-update`.
   - In the `feature-update` branch, create a new file called `feature.txt` and add some content related to your project (e.g., a description of a new feature).
   - Add and commit your changes to the `feature-update` branch using `git add feature.txt` and `git commit -m "Add feature description"`.

2. **Switch and Merge Branches:**
   - Switch back to the `main` branch using `git checkout main`.
   - Merge the `feature-update` branch into the `main` branch using `git merge feature-update`.
   - Push the updated `main` branch to GitHub using `git push origin main`.

---

#### **Part 3: Exploring GitHub Features**
1. **View Commit History:**
   - On GitHub, navigate to your repository and view the commit history to see the changes made in each commit.
   - Explore the details of individual commits, such as the changes made and the commit messages.

---

#### **Part 4: Resolving Merge Conflicts**
1. **Simulate a Conflict:**
   - In the `main` branch, modify the `README.md` file by adding a new line (e.g., “Main branch update”).
   - Commit this change to the `main` branch using `git commit -am "Update README in main branch"`.
   - Create a new branch called `conflict-branch` using `git checkout -b conflict-branch`.
   - In `conflict-branch`, modify the same line in the `README.md` file (e.g., “Conflict branch update”).
   - Commit this change in the `conflict-branch` using `git commit -am "Update README in conflict branch"`.

2. **Merge and Resolve:**
   - Switch back to the `main` branch and attempt to merge `conflict-branch` using `git merge conflict-branch`.
   - Resolve the merge conflict that occurs by editing the `README.md` file to incorporate both changes or select the desired update.
   - After resolving the conflict, complete the merge with a commit and push the final result to GitHub using `git push origin main`.

---

### **Submission:**
- Ensure your GitHub repository reflects all the changes, branches, and commits made during this assignment.
- Provide a link to your GitHub repository in your submission.
- Provide screenshots of your terminal commands, GitHub repository (showing the commit history, branches, and pull requests), and any merge conflict resolutions.

---

### **Key Concepts Covered:**
- Command Line navigation and file operations
- Git basics, including add, commit, and log
- Branch creation, switching, and merging
- Using GitHub for repository management
- Resolving merge conflicts

---