# Command Line

## **Introduction**

The command line, commonly referred to as the "terminal," is a powerful text-based interface used to interact with your computer. It allows users to manage files, use Git for version control, and run applications such as Node.js. While the command line is distinct from writing application code, it is essential for efficiently building, deploying, and managing software.

> **Note for Windows users**: Use the VS Code terminal connected to Ubuntu in WSL (Windows Subsystem for Linux). This ensures compatibility with Unix-based commands, which are standard in most software engineering environments. For setup instructions, see [Windows Command Line Setup](../logistics/required-software.md#install-and-setup-windows-subsystem-for-linux-wsl).

---

## **A Brief History Lesson**

The command line's origins date back to the early days of computing, specifically with the creation of the Unix operating system. Unix, developed for multi-user systems running on mainframe computers, allowed users to connect remotely via simple terminals. These terminals, consisting of just a keyboard and screen, lacked the ability to run programs locally. Instead, they acted as intermediaries, sending keystrokes to the mainframe and displaying text-based outputs from it.

With no mouse, graphics, or even color, all interactions were entirely text-based. Programs running on the mainframe accepted and produced only text, making the system lightweight and efficient, even by today’s standards. This simplicity and resource efficiency contributed to the enduring use of the command line in modern computing.

In the 1970s, Unix users managed files entirely through text commands, handling tasks such as creating, renaming, and organizing files into directories. Every action, from changing directories with `cd` to listing files with `ls`, required its own dedicated command. To make these tasks easier to manage, the Unix shell was developed—a master program that could launch other programs and provide additional features such as piping data between commands or using wildcards to work with groups of files.

Users could also write "shell scripts"—simple programs composed of multiple shell commands—to automate complex tasks. The original Unix shell, `sh`, evolved over time, and today’s most widely used shell is `bash`, which is available on most modern Linux systems.

---

## **The Command Line in Modern Systems**

Linux, a descendant of Unix, retains much of the functionality and structure of its predecessor. Modern Linux systems continue to support the same text-based commands and shell programs originally designed for Unix. The difference today is that instead of using old hardware terminals, most users access the command line through software terminals that run in a window alongside graphical applications.

The terminal remains an indispensable tool for developers, system administrators, and engineers due to its efficiency, flexibility, and the degree of control it provides over the operating system. Now, let’s explore how you can start using the command line yourself!