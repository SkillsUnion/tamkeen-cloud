# Troubleshooting SSH Key Authentication Issues with GitHub

If Git is still asking for your username and password despite adding your SSH public key to your GitHub account, here are a few things you can check and resolve the issue:

### 1. **Ensure You're Using the SSH URL**
Make sure you're cloning the repository using the SSH URL rather than the HTTPS one. The SSH URL format should look like:

```bash
git@github.com:your-username/repository.git
```

To check the current remote URL:

```bash
git remote -v
```

If it's using HTTPS, update it to SSH:

```bash
git remote set-url origin git@github.com:your-username/repository.git
```

---

### 2. **Verify SSH Authentication**
Test if your SSH key is working by running:

```bash
ssh -T git@github.com
```

If successful, you should see a message like:

```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

If not, troubleshoot SSH with:

- Ensure your SSH agent is running and has the key loaded:

  ```bash
  eval $(ssh-agent -s)
  ssh-add ~/.ssh/id_rsa  # or your key name if different
  ```

- Check that the correct private key is being used:

  ```bash
  ssh -i ~/.ssh/id_rsa -T git@github.com
  ```

---

### 3. **Check Git Config for Credentials**
Ensure Git isn't storing old HTTPS credentials by running:

```bash
git config --global --unset credential.helper
```

Alternatively, configure Git to use SSH:

```bash
git config --global user.name "your-username"
git config --global user.email "your-email@example.com"
git config --global core.sshCommand "ssh -i ~/.ssh/id_rsa"
```

---

### 4. **Check SSH Key Permissions**
Ensure the private key has the correct permissions:

```bash
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
```

Also, verify the SSH config file:

```bash
cat ~/.ssh/config
```

If it doesn't exist, create one and add:

```plaintext
Host github.com
  IdentityFile ~/.ssh/id_rsa
  User git
  AddKeysToAgent yes
```

---

### 5. **Clear Cached Credentials**
If you've previously used HTTPS authentication, clear any cached credentials:

```bash
git credential reject https://github.com
```

---

### 6. **Try a Fresh Clone**
If you've modified a lot of settings, sometimes it's easier to re-clone the repository with the SSH URL:

```bash
git clone git@github.com:your-username/repository.git
```