# **Creating Folders and Files**

> **Note for Windows users**: Please use the VS Code terminal connected to Ubuntu via WSL (Windows Subsystem for Linux). The Windows Command Prompt uses PowerShell by default, which is not compatible with Unix-based commands that most software engineers rely on. Refer to the "Required Hardware and Software" under "Welcome to the Cloud" for instructions.
>
> **Note for Mac users**: You can access the terminal by searching for “Terminal” in Spotlight (Cmd + Space) or by navigating to **Applications > Utilities > Terminal**. Mac's terminal uses a Unix-based shell similar to Linux, so the commands covered here will work seamlessly on macOS.

---

In this section, we will create some directories and files to work with. To avoid altering any real files, we will start by creating a new directory in the **/tmp** folder, a safer location for experimentation:

```bash
mkdir /tmp/tutorial
cd /tmp/tutorial
```

Here, the **`mkdir`** command (make directory) creates a new directory named "tutorial" inside **/tmp**, using an absolute path. The leading `/` ensures that the directory is created in the root-level **/tmp** folder. If you omit the `/`, the command will attempt to create the directory inside the current working directory, which may cause it to fail if no such directory exists.

Now, let's create a few subdirectories:

```bash
mkdir dir1 dir2 dir3
```

This command creates three new subdirectories: `dir1`, `dir2`, and `dir3`. Notice that multiple directory names are provided as arguments to the **`mkdir`** command. Not all commands accept multiple arguments, but **`mkdir`** does, while others like **`cd`** accept only one or none.

---

### **Viewing the Created Directories**

To see the new directories, use the **`ls`** command (list):

```bash
ls
```

You will notice that all three directories are created in the current directory. If you want to create nested directories (directories within directories), you can use the **`-p`** option with **`mkdir`**:

```bash
mkdir -p dir4/dir5/dir6
ls
```

Now, only `dir4` will appear in the list because `dir5` is inside `dir4`, and `dir6` is inside `dir5`. To confirm this, you can navigate into the directories:

```bash
cd dir4
ls
cd dir5
ls
cd ../..
```

The **`-p`** option stands for "parents" and allows you to create parent directories if they do not already exist. Options (or switches) modify how a command operates, and in this case, `-p` tells **`mkdir`** to create any missing parent directories.

---

### **Creating Directories with Spaces in Their Names**

If you need to create directories with spaces in their names, you must **escape** the spaces to prevent the command line from interpreting them as separate arguments:

```bash
mkdir "folder 1"
mkdir 'folder 2'
mkdir folder\ 3
mkdir "folder 4" "folder 5"
mkdir -p "folder 6"/"folder 7"
ls
```

Escaping can be done using quotes (`" "` or `' '`) or backslashes (`\`). While the command line supports spaces, it's generally a good practice to avoid them and instead use underscores (`_`) or hyphens (`-`) to make working with files easier.

---

### **Creating Files Using Redirection**

To create files, we can use **redirection**, which takes the output of a command and sends it to a file instead of displaying it in the terminal. First, let’s see the output of the **`ls`** command:

```bash
ls
```

Now, redirect that output into a new file:

```bash
ls > output.txt
```

This creates a file named `output.txt` with the result of the **`ls`** command. You can view the file's content with the **`cat`** command:

```bash
cat output.txt
```

---

### **Using `echo` to Create Files**

The **`echo`** command prints text to the terminal, but it can also be used to create small text files:

```bash
echo "This is a test" > test_1.txt
echo "This is a second test" > test_2.txt
echo "This is a third test" > test_3.txt
ls
```

Each file contains the text you provided. You can view the content of the files using **`cat`**:

```bash
cat test_1.txt test_2.txt test_3.txt
```

---

### **Using Wildcards to Work with Multiple Files**

Wildcards like `*` (zero or more characters) and `?` (any single character) allow you to work with multiple files easily. For example, to concatenate all the `test_` files into one file, you can use:

```bash
cat test_* > combined.txt
cat combined.txt
```

If you want to **append** instead of overwrite the content of a file, use double greater-than signs (`>>`):

```bash
cat test_* >> combined.txt
echo "I've appended a line!" >> combined.txt
cat combined.txt
```

---

### **Viewing Files with `less`**

When files are too large to view in one screen, use the **`less`** command, a pager that allows you to scroll through the content:

```bash
less combined.txt
```

Use the arrow keys or **Page Up/Down** to navigate, and press **q** to quit.

---

### **Good Naming Practices**

In Unix-based systems like Linux and macOS, the file system is **case-sensitive**, meaning that `file.txt` and `File.txt` are treated as different files. This can lead to confusion and potential data loss when working on case-insensitive systems like Windows.

For simplicity and to avoid issues, it is good practice to:
- Use **lowercase letters** in file and directory names.
- Avoid spaces by using **underscores** (`_`) or **hyphens** (`-`).
- Use **extensions** to indicate file types (e.g., `.txt`, `.log`).

By following these naming conventions, you can avoid common pitfalls when managing files from the command line.