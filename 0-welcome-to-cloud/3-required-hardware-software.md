# 💻 Required Hardware and Software

To participate in this courses, the following hardware and software are necessary:

## Required Hardware

- **Computer:** A desktop or laptop running the latest version of Windows or macOS.
- **Webcam and Microphone:** A webcam and microphone capable of supporting video conferencing. Most laptops come with these built-in.
- **Internet Connection:** A stable internet connection that can handle Zoom calls without interruptions in audio or video. If you're uncertain about your connection, let us know, and we can schedule a chat to help you assess it!


# ☝️ Required Software

## Required GUI-Application Software

GUI-application software is software that operates with a graphical user interface (GUI) on your operating system.

### Zoom

Zoom is the video conferencing software used for this program classes. Each section has its own Zoom room, and the link to this room will be found at the top of each section's Disco channel.

- **Installation:**
  - Download the Zoom Client for Meetings [here](https://zoom.us/download).
  - Start a new meeting to test your webcam and microphone.

### Chrome

Chrome is the most popular web browser among software engineers due to its robust developer tools, which will be introduced in the course. Chrome also has an extensive library of browser extensions that assist developers in building and maintaining software.

- **Installation:**
  - Download Chrome for your operating system [here](https://www.google.com/chrome/).

### VSCode

VSCode is the most popular code editor globally. All code for SWE Fundamentals will be written using VSCode.

- **Installation:**
  - Download VSCode for your operating system [here](https://code.visualstudio.com/Download).


# Required Software

## Introduction

This document outlines required software for this program. Please install this software before starting the course unless instructed otherwise.

## \[Windows Only] Install Windows-specific software

### Install and setup Windows Subsystem for Linux (WSL)

WSL allows us to run the Linux operating system on Windows machines. We do this because most programming uses Unix-based operating systems, of which MacOS is a descendant. Most SWEs that use Windows do their work in WSL to maximise compatibility between their work and work done on Linux machines. Before installing WSL, update Windows to the latest version.

1. Install WSL <a href="https://docs.microsoft.com/en-us/windows/wsl/install-win10" target="_blank">here</a>.
2. Install the latest version of Ubuntu <a href="https://apps.microsoft.com/store/detail/ubuntu-22041-lts/9PN20MSR04DW?hl=en-sg\&gl=sg" target="_blank">here</a>. Ubuntu is a popular version of the Linux operating system.
3. Run `sudo apt install build-essential` in Ubuntu in WSL to install standard libraries Ubuntu needs to further install common packages.
4. Run `sudo apt-get install ca-certificates` in Ubuntu in WSL to get SSL verification certificates on Ubuntu for Ubuntu to communicate with VS Code on our computer.

### Integrate VS Code with WSL

1. Install the <a href="https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack" target="_blank">VS Code Remote Development extension</a> to enable VS Code to integrate with WSL.
2. Click the Remote Development extension icon in the bottom left corner of VS Code. A pop up will appear with a list of options. Click the first option "Remote-WSL: New Window" for the default distro.

You will see a notification "Starting VS Code in WSL...". This means VS Code is setting up a server inside WSL for the first time. Once installed, the VS Code of your Windows OS will sync automatically with the VS Code of your Ubuntu OS, and the VS Code terminal will show the Ubuntu terminal.

## \[Mac Only] Install Mac-specific software

### Install Homebrew

Follow instructions at <a href="https://brew.sh" target="_blank">https://brew.sh/</a> to install Homebrew.

Homebrew is a package manager for MacOS that provides a single source of truth for which packages and package versions are installed. This is typically only relevant to command line packages; We typically do not install GUI applications via Homebrew.

Homebrew typically manages OS-specific packages, e.g. `node`, and not application-specific packages, e.g. `aws`. Application-specific packages are typically managed by application-level package managers such as `npm` or `pip`. Application-specific packages are typically bundled and deployed together with an application, regardless of where those applications are running.

## Install and configure Git

### Install Git

### Windows
Open an Ubuntu terminal in VS Code and run the following commands separately.

```bash
sudo apt-get update
```

```bash
sudo apt-get install git
```

```bash
# Verify correct installation by checking Git version
git --version
```

### MacOS
1\. Download and install Git for MacOS

```
brew install git
```

2\. Verify Git is installed by running `git --version` in the <a href="https://code.visualstudio.com/docs/editor/integrated-terminal" target="_blank">VS Code terminal</a>. This should print out a version number on the next line, e.g., `git version 2.9.2`.

```
git --version
```

3\. Download and install the <a href="https://github.com/microsoft/Git-Credential-Manager-Core/releases/download/v2.0.498/gcmcore-osx-2.0.498.54650.pkg" target="_blank">Git Credential Manager</a>

>To install the Git Credential Manager you may need to allow "unidentified developer apps". Don't worry, Git Credential Manager is created by Microsoft. <a href="https://support.apple.com/en-sg/guide/mac-help/mh40616/mac" target="_blank">Instructions here</a>.
>
>If you are using a company computer for this course you may not be able to override the security settings. You may need to <a href="https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token" target="_blank">create a personal access token</a> instead.

### Personal Access Tokens&#x20;

### Configure Git and GitHub

When using the HTTPS protocol on GitHub to retrieve repository information you will need to develop a personal access token on your GitHub account, you will then be able to use this token to authenticate your request. To create a personal access token please follow this set of <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token" target="_blank">documentation</a>.

After you have created the personal access token be sure to save it in a safe spot as it will be required when authenticating requests to the GitHub servers. You will be prompted to pass your GitHub username and password when trying to push to repositories, use your Personal Access Token in place of your password.&#x20;

#### Configure Git default branch

Set the default Git branch to `main` as per GitHub's (and this program's) latest convention. Some older versions of Git may still use `master` as the default branch name.

```bash
git config --global init.defaultBranch main
```

#### Configure Git default editor

1. Follow instructions <a href="https://stackoverflow.com/a/39604469" target="_blank">here</a> to enable the `code` command in terminal to open VS Code.
2. Set the default Git code editor to VS Code to avoid Git's default command line editor Vim, which requires learning Vim-specific keyboard shortcuts. We may need to use Vim on remote servers as SWEs, but to keep things simple during the program we will stick to VS Code.

```shell
git config --global core.editor "code --wait"
```

#### Configure Git and GitHub Credentials

Set your GitHub account credentials on your computer through the command line. This will enable us to interact with GitHub via the command line, which we will do a lot. Please replace `<YOUR_GITHUB_USERNAME>` and `<YOUR_GITHUB_EMAIL>` with your GitHub username and email.

```bash
git config --global user.name "<YOUR_GITHUB_USERNAME>"
```

```bash
git config --global user.email "<YOUR_GITHUB_EMAIL>"
```

Type `git config -l` into the terminal to verify configuration success. If you see `user.name` and `user.email` in the output, we succeeded. If you see a `:` at the bottom of the output, you may need to press `Enter` until you see the lines starting with `user.name` and `user.email`.

After configuring your GitHub credentials you will be able to access GitHub repositories and make requests, however you will be prompted for your username and password every single request. While this level of security is brilliant for companies it can be frustrating for the developers. To make your lives a tad easier you can run these commands in your CLI in order to save your credentials into the environment.

```bash
git config --global credential.helper store
```

```bash
git config --global credential.helper cache
```

After doing these commands you may need to go through git flow once before it has saved your credentials (including your personal access token, which should be used as a password when prompted for username and password.



## Install Node.js

### Windows
Open an Ubuntu terminal in VS Code and run the following commands separately.

```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```

```bash
sudo apt-get install -y nodejs

```

### MacOS

Install Node.js using Homebrew using the following commands. `install` installs the package and `link` makes the `node` command accessible in our terminal. Run these commands separately.&#x20;

```
brew install node@18
```

```
brew link node@18
```

## Install Code Formatters

### Install Prettier

Prettier is a code formatter that will auto-format our code and make it more readable when we save our files.

1. Install the Prettier extension for VS Code <a href="https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode" target="_blank">here</a>.

### Install ESLint

ESLint is a JavaScript code linter that helps us detect functional errors in our code prior to running it.

1. Install ESLint on your computer by running `sudo npm i -g eslint` from the terminal in VS Code. Enter your computer's password if prompted.
2. Install the ESLint VS Code extension <a href="https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint" target="_blank">here</a>.

### Set VS Code formatting settings

1. Open VS Code and open the command prompt with `Ctrl+Shift+P` on Windows or `Cmd+Shift+P` on Mac
2. Start typing `Preferences: Open Settings (JSON)` and select this option when you see it in the search dropdown. VS Code should open a JSON settings file.
3. Replace the contents of the file with the code below
4. Save the settings file
5. Restart VS Code to apply settings


```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "editor.formatOnPaste": true,
  "editor.tabSize": 2,
}
```

## Recommendation folder structure for Cloud Engineering Program

We recommends the following folder structure to keep ourselves organised during the program.


>Name files and folders in kebab-case, e.g. `new-file.txt`, lowercase and hyphenated for ease of use on the command line. We do not recommend naming files and folders with spaces in names because we will need to enter special characters in the terminal to escape the space character when referring to these files.


>Please do not store code in folders synced to cloud storage such as Google Drive or Apple iCloud. This will cause issues during the program, such as package installations running slowly or unnecessary extra files committed to GitHub.


1. Store all the program code in a folder called `cloudengineering`.
2. Within `cloudengineering`, create a folder `m1` for Module 1 and store all Module 1 exercise code there in exercise-specific folders. Our Project 1 repo folder can also go inside `m1`.
3. Make 3 copies of `m1` within `cloudengineering` and rename them `m2`, `m3`, 1 folder for each module in the program.


## Extra Reading

#### GitHub and SSH

Another way developers are able to authenticate requests to GitHub is to create and use an SSH key on their personal machines. This SSH key acts as a unique signature that can be linked to your GitHub account online, essentially creating a connection between your machine and GitHub when used. SSH keys require a little more setup than using HTTPS but they will not prompt you for authentication every single request.

#### Setting up SSH&#x20;

1. &#x20;You will need to check for existing SSH keys on your machine, please follow these <a href="https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys" target="_blank">docs</a>.&#x20;
2. If you do not have you then you will need to generate a new SSH key please follow these <a href="https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent" target="_blank">docs</a>.
3. Following this you will need to add the new SSH key into your GitHub account online please follow these <a href="https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account" target="_blank">docs</a>.
