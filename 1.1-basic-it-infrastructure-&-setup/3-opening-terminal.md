# **Opening a Terminal**

## **Learning Objectives: Opening a Terminal**
1. Understand how to open the terminal on Ubuntu, macOS, and Windows (via VS Code and WSL).  
2. Learn to identify and interpret the terminal prompt, including the current working directory.  
3. Gain proficiency in navigating the file system using `pwd` and `cd` commands.  
4. Differentiate between relative and absolute file paths and apply them effectively.  
5. Recognize the case sensitivity of commands and file paths in Unix-based systems.  

> **Note for Windows users**: Please use the VS Code terminal connected to Ubuntu via WSL (Windows Subsystem for Linux). The Windows Command Prompt uses PowerShell by default, which is not compatible with Unix-based commands that most software engineers rely on. Refer to the [Windows Command Line Setup](../logistics/required-software.md#install-and-setup-windows-subsystem-for-linux-wsl) for instructions.
>
> **Note for Mac users**: You can access the terminal by searching for “Terminal” in Spotlight (Cmd + Space) or by navigating to **Applications > Utilities > Terminal**. Mac's terminal uses a Unix-based shell similar to Linux, so the commands covered here will work seamlessly on macOS.

---

### **Introduction**

The command line, often referred to as the "terminal," is a text-based interface that allows users to interact with their computer by typing commands. It is a crucial tool for managing files, using Git for version control, and running applications like Node.js. While separate from writing application code, mastering the command line is essential for building and managing software effectively.

---

### **Opening a Terminal**

#### **For Ubuntu Users**  
On **Ubuntu 18.04**, you can open the terminal by clicking on the **Activities** button in the top-left corner and typing “terminal,” “command,” “prompt,” or “shell.” The launcher will quickly locate the terminal. Alternatively, use the keyboard shortcut **Ctrl + Alt + T** to open it instantly.

#### **For Mac Users**  
On macOS, you can find the terminal by:
- Pressing **Cmd + Space** to open Spotlight, then typing "Terminal" and pressing **Enter**.
- Alternatively, go to **Applications > Utilities > Terminal**.

#### **For Windows Users**  
Windows users should access the terminal via **VS Code** connected to Ubuntu using **WSL** (Windows Subsystem for Linux) for a compatible Unix-like shell. PowerShell, the default terminal on Windows, does not support most Unix commands, which are essential for development workflows.

---

### **Launching and Navigating the Terminal**

Once you launch the terminal, you'll see a window displaying a prompt. The **prompt** is an indicator that the terminal is ready to accept commands. Depending on your system, this prompt might include your username, computer name, and current working directory.

To start, let’s run a simple command. In the terminal, type:

```bash
pwd
```

This command prints the **current working directory**, which shows where in the file system the terminal is currently operating. Typically, this will be something like `/home/YOUR_USERNAME` or `/Users/YOUR_USERNAME` on a Mac. After running the command, the terminal will output the directory path and return to the prompt, ready for your next command.

---

### **Understanding Command Line Basics**

When typing a command, it appears next to the prompt, and any output will be displayed directly below. After the command finishes, the prompt reappears, indicating the terminal is ready for further input. Some commands may produce extensive output, while others might execute silently and return immediately to the prompt.

---

### **Case Sensitivity in the Terminal**

The terminal is **case-sensitive**, meaning that commands must be entered exactly as shown. For instance, typing `PWD` instead of `pwd` will result in an error. This applies to both commands and file paths, so always ensure that the correct case is used when entering commands.

---

### **Exploring the File System**

To view your current location in the file system, use the `pwd` (print working directory) command. This tells you where the shell is currently operating. The shell has a "working directory," which is the default location where all file operations, like creating or deleting files, will occur unless you specify otherwise.

To navigate between directories, the **`cd`** command (change directory) is used. For example, to move to the root directory, you can type:

```bash
cd /
pwd
```

In Linux and macOS, the root directory (`/`) is the starting point of the entire file system. Unlike Windows, which separates drives (e.g., `C:`), Linux and macOS use a unified file system where everything is mounted under the root directory.

---

### **Navigating Directories**

To navigate through directories, use the **`cd`** command:

```bash
cd home
pwd
```

This command moves you into the **home** directory. To move back to the parent directory, use the following command:

```bash
cd ..
pwd
```

Typing `cd` without any additional arguments returns you to your home directory:

```bash
cd
pwd
```

You can also move up multiple levels using `..` more than once:

```bash
cd ../..
pwd
```

---

### **Relative vs. Absolute Paths**

Paths can be **relative** or **absolute**:

- **Relative paths** are based on your current location in the file system. For instance, if you're in `/home/your_username`, the command `cd Documents` will take you to `/home/your_username/Documents`.
  
- **Absolute paths** start from the root directory and provide the full path to the location, regardless of your current directory. For example:

```bash
cd /etc
pwd
```

No matter where you are in the file system, this command will always take you to the `/etc` directory.

Additionally, to return to your home directory:

```bash
cd /home/YOUR_USERNAME
pwd
```

You can also use the tilde (`~`) as a shortcut for your home directory:

```bash
cd ~
pwd
```

You can even combine it to navigate to specific folders inside your home directory:

```bash
cd ~/Desktop
pwd
```

---

### **Conclusion**

The ability to navigate the file system using both relative and absolute paths is essential when working in the terminal. With this knowledge, you’ll be able to move efficiently through directories and begin working with files and directories directly from the command line. Next, we will explore how to create and manage files in the terminal.