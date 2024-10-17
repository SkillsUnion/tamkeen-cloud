### **The Command Line and the Superuser**

> **Note for Windows users**: Please use the VS Code terminal connected to Ubuntu via WSL (Windows Subsystem for Linux). The Windows Command Prompt uses PowerShell by default, which is not compatible with Unix-based commands that most software engineers rely on. Refer to the [Windows Command Line Setup](../logistics/required-software.md#install-and-setup-windows-subsystem-for-linux-wsl) for instructions.
>
> **Note for Mac users**: You can access the terminal by searching for “Terminal” in Spotlight (Cmd + Space) or by navigating to **Applications > Utilities > Terminal**. Mac's terminal uses a Unix-based shell similar to Linux, so the commands covered here will work seamlessly on macOS.

---

When using the command line, you will occasionally come across instructions that require **superuser** or **administrator** privileges. Understanding the implications of running commands as the superuser is critical to maintaining system security and stability. The superuser (often referred to as "root" in Unix-based systems) has unrestricted access to modify or delete any files, override security measures, and perform administrative tasks that could significantly impact the system.

---

### **What is the Superuser?**

The **superuser** is a user account with special privileges, allowing full control over the system. Historically, the superuser account was known as **root** and could modify any part of the system, including:

- Deleting or modifying system-critical files.
- Changing network and firewall settings.
- Shutting down the system, even if other users are logged in.

While the root account provides necessary administrative control, it also comes with risks. A mistyped command can accidentally delete essential files or crash the system. Worse, if someone with malicious intent gains access to a root session, they can compromise the entire machine.

---

### **Avoid Using the Root Account Directly**

It is best practice **not to use the root account directly**. Many modern Linux distributions, including Ubuntu, disable the root account by default. Instead of logging in as root, you can use a safer method to perform administrative tasks: the **`sudo`** command.

---

### **What is `sudo`?**

The **`sudo`** command stands for "superuser do." It allows regular users to execute commands with superuser privileges on a per-command basis. This method significantly reduces the risk of accidental system damage, as users only invoke administrative privileges when absolutely necessary.

When you run a command with `sudo`, the system prompts for your user password (not the root password). Once entered, your credentials are cached for a short period (usually 15 minutes), allowing you to run multiple commands without having to re-enter your password each time.

Here’s an example of using `sudo` to access a system file that requires superuser privileges:

```bash
cat /etc/shadow
sudo cat /etc/shadow
```

The second command runs successfully with **`sudo`**, as it grants you temporary superuser privileges. The cached password allows you to run another `sudo` command within the time limit without needing to enter the password again.

---

### **Be Careful When Using `sudo`**

While `sudo` is safer than logging in as root, it still carries significant responsibility. A command run with `sudo` has the same power as the root user and can execute destructive actions. Always review commands before running them with `sudo`, especially those found online. If you're unsure what a command does, research it before proceeding.

For example, a malicious command combined with `sudo` could install malware or make your system vulnerable. Commands that manipulate critical system files, start new services, or download software from unverified sources should be treated with extra caution.

---

### **Common Uses of `sudo`**

One of the most common scenarios where you'll use `sudo` is when installing new software. On Ubuntu, software can be installed from the system’s repositories using the **`apt`** or **`apt-get`** commands. Here’s an example:

```bash
sudo apt install tree
```

This command installs the **`tree`** program, a small utility that displays directory structures. You’ll see several lines of text as the system downloads and installs the package. Once completed, you can run the newly installed program:

```bash
cd /tmp/tutorial
tree
```

The **`tree`** command shows the structure of your current directory, providing a clear overview of your files and folders.

---

### **Installing Software from Non-Standard Sources**

While installing software from the official Ubuntu repositories is generally safe, be cautious when using commands like **`curl`**, **`wget`**, **`pip`**, or **`npm`** to install software from external sources. These methods often bypass the security measures in place for repository-based installations and can introduce vulnerabilities.

For example, you might find instructions asking you to change file permissions using `chmod` and run an unknown script with `sudo`. Always verify the source and purpose of the script before executing it, as this could open a security hole in your system.

---

### **Disabling `root` and Avoiding `su`**

Some instructions may encourage you to use **`su`** to switch to the root user. While `su` can switch between user accounts, it should be avoided in favor of `sudo`. The **`sudo`** approach ensures that superuser privileges are granted only on a per-command basis, minimizing risk.

In Ubuntu, the root account is disabled by default, meaning that `su` with no arguments will not work unless root has been explicitly enabled, which is not recommended. If a guide asks you to use **`sudo su`**, be aware that you are essentially switching to a root shell, giving you full superuser privileges until you log out of the session. This can be risky, as all subsequent commands will run as root without requiring `sudo`.

---

### **Conclusion**

In summary, using **`sudo`** gives you the ability to perform administrative tasks without the need to fully switch to the root user. It is a safer approach for managing system-level operations on Unix-based systems like Linux and macOS.

When following instructions, always take extra care with commands requiring `sudo`. Be especially cautious with any steps that involve adding software repositories, changing file permissions, or running scripts downloaded from the internet. Stick to official repositories and trusted sources whenever possible, and always make sure you understand what a command is doing before running it.

By using **`sudo`** responsibly, you can protect your system from accidental damage while ensuring that you still have the control needed to perform critical administrative tasks.