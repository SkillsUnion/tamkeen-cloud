# **Hidden Files**

## **Learning Objectives: Hidden Files**
1. Understand the purpose of hidden files and directories in Unix-based systems and their naming convention (starting with a dot `.`).  
2. Learn how to create, view, and manage hidden files and directories using commands like `mv`, `mkdir`, and `ls -a`.  
3. Use the `tree -a` command to explore hidden files within directory structures.  
4. Recognize the role of hidden files in storing user and system configurations, especially in the home directory.  
5. Develop good practices for cleaning up experimental directories and closing the terminal session properly.  


> **Note for Windows users**: Please use the VS Code terminal connected to Ubuntu via WSL (Windows Subsystem for Linux). The Windows Command Prompt uses PowerShell by default, which is not compatible with Unix-based commands that most software engineers rely on. Refer to the [Windows Command Line Setup](../logistics/required-software.md#install-and-setup-windows-subsystem-for-linux-wsl) for instructions.
>
> **Note for Mac users**: You can access the terminal by searching for “Terminal” in Spotlight (Cmd + Space) or by navigating to **Applications > Utilities > Terminal**. Mac's terminal uses a Unix-based shell similar to Linux, so the commands covered here will work seamlessly on macOS.

---

Before concluding, it’s important to understand **hidden files** and **folders** in Unix-based systems. These are often used to store system settings or configuration files. Hidden files aren’t inherently special; they’re hidden simply because their names start with a dot (`.`). This prevents them from cluttering up your file views.

Let’s explore hidden files in practice.

---

### **Creating and Working with Hidden Files**

First, navigate to your tutorial directory:

```bash
cd /tmp/tutorial
ls
```

Let’s hide the `combined.txt` file by renaming it with a dot in front of the name:

```bash
mv combined.txt .combined.txt
ls
```

The file has now disappeared from the regular **`ls`** output, but it still exists. You can interact with it by including the dot in the file name:

```bash
cat .combined.txt
```

Now let’s create a hidden directory and move the hidden file into it:

```bash
mkdir .hidden
mv .combined.txt .hidden
less .hidden/.combined.txt
```

The directory **`.hidden`** is also hidden, but you can still access its contents by specifying the directory name:

```bash
ls .hidden
```

If you want to see all files, including hidden ones, use the **`-a`** option with **`ls`** to display everything in a directory:

```bash
ls -a
ls -a .hidden
```

The **`-a`** option reveals hidden files and directories, including the special entries `.` (current directory) and `..` (parent directory). These appear as real directories but serve as shortcuts.

---

### **Using `tree` with Hidden Files**

The **`tree`** command can also display hidden files when used with the `-a` option:

```bash
tree
tree -a
```

---

### **Exploring Hidden Files in Your Home Directory**

Hidden files are common in your home directory, where they store personal configurations. Let’s switch to the home directory and see how many hidden files are present:

```bash
cd
ls
ls -a
```

You can use **`wc -l`** to count the number of files, including hidden ones:

```bash
ls -a | wc -l
```

Hidden files in your home directory often contain user-specific settings that override system-level configurations. While you may not frequently need to interact with these files, you now understand their purpose and how to reveal them in both the terminal and graphical tools.

---

### **Cleaning Up**

Before concluding this tutorial, let’s tidy up by removing the test directory we created earlier. First, check that you’re in your home directory:

```bash
pwd
cd
```

Now, remove the experimental directory:

```bash
rm -r /tmp/tutorial
ls /tmp
```

---

### **Closing the Terminal**

To properly close the terminal, it’s good practice to log out of the shell rather than just closing the window. You can do this with the **`logout`** command or by pressing **Ctrl-D**:

```bash
logout
```

By mastering the **Ctrl-Alt-T** shortcut to open the terminal and **Ctrl-D** to close it, you can seamlessly integrate the command line into your workflow, making it a powerful tool at your fingertips.