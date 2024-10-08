# Command Line

## Learning Objectives

1. Use the command line as the text interface for manipulating our computers
2. Navigate folders and display folder contents in the command line
3. Create new folders and files in the command line
4. Rename or delete folders and files in the command line

## Introduction

The command line, also known as "terminal" is a text-based computer interface. We will use the command line to manage files, use Git version control and run Node applications. Using the command line is separate from writing application code, though we will need the command line to build apps effectively.

> If you are a Windows user, please use the VS Code terminal connected to Ubuntu in WSL. The Windows Command Prompt runs PowerShell by default which is not compatible with Unix-based commands that most software engineers use. See [Windows Command Line Setup](../logistics/required-software.md#install-and-setup-windows-subsystem-for-linux-wsl) for details.

## Common Commands

Below, we have listed some of the most commonly used terminal commands that software engineers use. To learn more about these commands, google "man" followed by the command name to get the "manual" page for the command (eg. to learn more about "pwd", simply enter "man pwd" into google).

> **Tab Complete**
> 
> The command line will autocomplete file and folder names if we press `tab` after starting to type their names. This can save us a lot of typing!

<table><thead><tr><th width="150">Command</th><th width="150">Meaning</th><th>Sample Usage</th><th>Explanation</th></tr></thead><tbody><tr><td><code>pwd</code></td><td>Present working directory</td><td><code>pwd</code></td><td>Retrieve the "absolute path" of the current folder (directory). <br><br>Absolute means relative to the root folder of your hard drive.</td></tr><tr><td><code>ls</code></td><td>List</td><td><code>ls</code></td><td>List the files and folders in the current folder</td></tr><tr><td><code>cd</code></td><td>Change directory</td><td><code>cd bootcamp/project1</code></td><td>Move to the specified folder. <br><br>If we do not specify a folder, <code>cd</code> will move us to the current user's home folder.<br><br>To move to the parent folder, use <code>cd ..</code>. The 2 dots are a special path referencing the parent folder.</td></tr><tr><td><code>mkdir</code></td><td>Create folder</td><td><code>mkdir components</code></td><td>Create a new folder at the specified path</td></tr><tr><td><code>cp</code></td><td>Copy</td><td>File: <code>cp App.js newComponent.js</code><br><br>Folder: <code>cp -r components components-new</code></td><td>Copy the contents of the first file to the second, overwriting contents of the second if any. <br><br>Use <code>cp -r</code> (recursive flag) to copy folders.</td></tr><tr><td><code>mv</code></td><td>Move</td><td><p>Move: <code>mv App.js components</code></p><p>Rename: <code>mv App.js index.js</code></p></td><td><p>Move the 1st argument to the 2nd argument. <br><br>If the 2nd argument is a folder, move the 1st argument inside the 2nd argument. </p><p></p><p>Otherwise, rename the 1st argument to be the 2nd argument.</p></td></tr><tr><td><code>rm</code></td><td>Remove</td><td>File: <code>rm unnecessary-file.txt</code><br><br>Folder: <code>rm -r unnecessary-folder</code></td><td><p>Delete a file or folder. This is irreversible and there is no trash folder. <br></p><p>Be very careful, and if you delete the root folder <code>/</code> you may have to reformat your computer.</p></td></tr></tbody></table>

## Common Special Paths

The following paths are shortcuts to common locations and are often used in folder navigation.

<table><thead><tr><th width="150">Path</th><th>Meaning</th><th>Sample Usage</th><th>Explanation</th></tr></thead><tbody><tr><td><code>/</code></td><td>Root, i.e. the highest-level folder on our computers</td><td><code>cd /Users/joe/bootcamp/project1</code></td><td>All absolute paths begin with the root folder <code>/</code></td></tr><tr><td><code>~</code></td><td>Home, i.e. the logged-in user's home folder</td><td><code>cd ~</code></td><td><code>~</code> is an alias for <code>/Users/username</code>, where <code>username</code> is the username of the logged-in user</td></tr><tr><td><code>..</code></td><td>Parent folder</td><td><code>cd ..</code></td><td>Every folder has a hidden link <code>..</code> that references the parent folder. <code>cd ..</code> changes directory to the parent folder without having to reference the name of the parent folder.</td></tr><tr><td>.</td><td>Current folder</td><td><code>mv components/App.js .</code></td><td><code>.</code> is most commonly used to move files or folders from elsewhere to the current folder</td></tr></tbody></table>


## Command Line Cheat Sheet
![](<../.gitbook/assets/command-line-cheatsheet.jpg>)