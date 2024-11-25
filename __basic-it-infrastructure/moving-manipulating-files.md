# **Moving and Manipulating Files**

> **Note for Windows users**: Please use the VS Code terminal connected to Ubuntu via WSL (Windows Subsystem for Linux). The Windows Command Prompt uses PowerShell by default, which is not compatible with Unix-based commands that most software engineers rely on. Refer to the "Required Hardware and Software" under "Welcome to the Cloud" for instructions.
>
> **Note for Mac users**: You can access the terminal by searching for “Terminal” in Spotlight (Cmd + Space) or by navigating to **Applications > Utilities > Terminal**. Mac's terminal uses a Unix-based shell similar to Linux, so the commands covered here will work seamlessly on macOS.

---

Now that we have created a few files, it’s time to explore how to move, rename, and delete them using the command line. While most users perform these tasks using graphical interfaces for one or two files, the command line is incredibly useful for making bulk changes or working with files scattered across directories.

---

### **Moving Files**

To move the `combined.txt` file into the `dir1` directory, use the **`mv`** (move) command:

```bash
mv combined.txt dir1
```

To confirm the file has been moved, you can list the contents of `dir1` without changing directories:

```bash
ls dir1
```

If it turns out the file shouldn’t be in `dir1`, move it back to the current working directory. You can use the `*` wildcard to match the filename in `dir1` and move it back using `.` to represent the current directory:

```bash
mv dir1/* .
```

---

### **Moving Multiple Files**

The **`mv`** command allows you to move multiple files or directories at once. Let’s move `combined.txt`, the test files, and `dir3` into `dir2`:

```bash
mv combined.txt test_* dir3 dir2
```

You can check that the files have moved by listing the contents of `dir2`:

```bash
ls dir2
```

Now, if you want to move `combined.txt` further into the nested `dir6` directory (inside `dir5`, inside `dir4`), use:

```bash
mv dir2/combined.txt dir4/dir5/dir6
```

Even though the working directory remains the same, you can manipulate files in completely different directories, a key benefit of the command line.

---

### **Copying Files**

To make a copy of `combined.txt` back into the current directory, use **`cp`** (copy):

```bash
cp dir4/dir5/dir6/combined.txt .
```

You can also create another copy of `combined.txt` but with a new name:

```bash
cp combined.txt backup_combined.txt
```

---

### **Renaming Files**

Renaming in the command line is handled using the **`mv`** command, just like moving files. To rename `backup_combined.txt` to `combined_backup.txt`:

```bash
mv backup_combined.txt combined_backup.txt
```

This also works for directories, making it easy to rename any directory. Let’s rename the directories with spaces to use underscores instead:

```bash
mv "folder 1" folder_1
mv "folder 2" folder_2
mv "folder 3" folder_3
mv "folder 4" folder_4
mv "folder 5" folder_5
mv "folder 6" folder_6
```

---

### **Deleting Files and Directories**

> **Warning**: Always use the **`pwd`** command to ensure you're still in the `/tmp/tutorial` directory before deleting files to prevent accidental loss of important files.

To delete the `combined.txt` in `dir6` and `combined_backup.txt` in the working directory, use the **`rm`** (remove) command:

```bash
rm dir4/dir5/dir6/combined.txt combined_backup.txt
```

Next, let’s try deleting some of the excess directories:

```bash
rm folder_*
```

This will produce an error because **`rm`** cannot delete directories. Instead, you need to use **`rmdir`** for empty directories:

```bash
rmdir folder_*
```

If a directory contains subdirectories or files, **`rmdir`** will also fail. For example, `folder_6` still has content, so to delete it, use the **`rm -r`** (recursive) option:

```bash
rm -r folder_6
```

This command deletes the directory and everything inside it. Be cautious when using **`rm -r`**, as it can permanently remove entire directory trees.

---

### **Important Warning**

Unlike graphical interfaces, the **`rm`** command does **not** move files to a "trash" folder. Files are permanently deleted with no option for recovery. Be especially careful with wildcards, as they can unintentionally delete more files than intended. For safety, consider using the **`rm -i`** (interactive) option, which prompts for confirmation before deleting each file:

```bash
rm -i folder_*
```

This option provides an extra layer of security, ensuring you confirm the deletion of each file before it is removed.

By mastering these commands, you can efficiently move, copy, rename, and delete files and directories through the terminal, streamlining file management for both small and large tasks.