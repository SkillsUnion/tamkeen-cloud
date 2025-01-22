# Persistent SSH Key Setup in Bash to Avoid GitHub Credential Prompts

To avoid entering your GitHub username and password repeatedly, you can set up SSH key authentication permanently by adding configurations to your `~/.bashrc` (or `~/.bash_profile` on macOS) to ensure your SSH agent starts and loads your key automatically.

### Steps to Set Up SSH Key in `~/.bashrc`:

1. **Open the `~/.bashrc` file** (or `~/.bash_profile` for macOS users):

   ```bash
   nano ~/.bashrc
   ```

2. **Add the following lines to ensure the SSH agent runs and the key is added on startup:**

   ```bash
   # Start the SSH agent if not already running
   if [ -z "$SSH_AUTH_SOCK" ]; then
       eval "$(ssh-agent -s)"
       ssh-add ~/.ssh/id_rsa  # Change id_rsa if you have a different key name
   fi
   ```

   If you're using multiple SSH keys, add them as needed:

   ```bash
   ssh-add ~/.ssh/id_rsa
   ssh-add ~/.ssh/another_key
   ```

3. **Save and exit the file:**
   - Press `CTRL + X`, then `Y`, and hit `ENTER` to save.

4. **Reload the `~/.bashrc` to apply changes:**

   ```bash
   source ~/.bashrc
   ```

5. **Test the SSH connection:**

   ```bash
   ssh -T git@github.com
   ```

   If it's set up correctly, you should see:

   ```
   Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
   ```

---

### Additional Tips:

- If you're using **macOS**, modify `~/.bash_profile` or `~/.zshrc` (if using Zsh) instead of `~/.bashrc`.

- If you have a passphrase on your SSH key and want to avoid entering it every time, ensure you're using an SSH agent as shown above.

- If you use WSL (Windows Subsystem for Linux), similar steps apply, but ensure SSH is correctly set up on Windows as well.

---

Once you've set this up, your SSH key should load automatically when you start a new terminal session, and GitHub should no longer prompt for credentials.