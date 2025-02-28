# SSH Connection & Key Management Tutorial

Secure Shell (SSH) is a fundamental component for managing remote servers securely, especially when using Ansible. This guide covers SSH key management, including generating, copying, and managing keys for secure authentication.

---

## Why Use SSH Keys?
By default, SSH connections require a password, which can be susceptible to brute-force attacks. Using SSH keys enhances security by eliminating password-based authentication and enabling encrypted connections.

## Prerequisites
**Ensure SSH is activated and enabled** on both your workstation and the target servers.

### Normal SSH Scenario
1. **Connect to a server for the first time:**
   ```sh
   ssh 192.168.100.2
   ```
   - You will receive a prompt asking if you want to connect. Type `yes` and press `Enter`.

2. **Create an SSH key pair (with a passphrase) for your normal user account:**
   ```sh
   ssh-keygen -t ed25519 -C "Your comment"
   ```
   - `-t ed25519`: Specifies the type of key (more secure than RSA).
   - `-C`: Adds a comment (useful for identification).
   - You will be prompted to specify a storage path. Press `Enter` to accept the default (`~/.ssh/id_ed25519`).
   - You will also be asked to set a passphrase for added security.

3. **Copy the public key to the server:**
   ```sh
   ssh-copy-id -i ~/.ssh/id_ed25519.pub 192.168.100.4
   ```
   - This ensures passwordless authentication for future connections.

4. **Verify the key on the remote server:**
   ```sh
   cat ~/.ssh/authorized_keys
   ```

### SSH Scenario with Ansible
1. **Create an SSH key pair specifically for Ansible (without a passphrase):**
   ```sh
   ssh-keygen -t ed25519 -C "ansible key" -f ~/.ssh/ansible
   ```
   - The `-f` flag specifies the filename (`~/.ssh/ansible`).
   - No passphrase is set for seamless automation.

2. **Copy the key to each server:**
   ```sh
   ssh-copy-id -i ~/.ssh/ansible.pub 192.168.100.4
   ```

3. **Verify the key on the server:**
   ```sh
   cat ~/.ssh/authorized_keys
   ```

---

## SSH Key Management
### Listing Existing SSH Keys
```sh
ls -la ~/.ssh
```
- This command lists all stored SSH keys.

### Managing Passphrase-Protected Keys
If you use a passphrase, you can cache it using `ssh-agent` to avoid re-entering it:

1. **Start the SSH agent:**
   ```sh
   eval $(ssh-agent)
   ```
   - This runs a background process that caches passphrases.

2. **Add your key to the agent:**
   ```sh
   ssh-add ~/.ssh/id_ed25519
   ```
   - Enter the passphrase when prompted.
   - The key is now stored for the session.

3. **Make it permanent by creating an alias:**
   ```sh
   alias ssha='eval $(ssh-agent) && ssh-add'
   ```
   - Now, simply typing `ssha` will start `ssh-agent` and add your key automatically.

---

## Summary
| Command | Description |
|---------|-------------|
| `ssh 192.168.100.2` | Connect to a server via SSH |
| `ssh-keygen -t ed25519 -C "Your comment"` | Generate a secure SSH key pair |
| `ssh-copy-id -i ~/.ssh/id_ed25519.pub <server_ip>` | Copy your public key to a server |
| `ls -la ~/.ssh` | List stored SSH keys |
| `eval $(ssh-agent)` | Start the SSH authentication agent |
| `ssh-add ~/.ssh/id_ed25519` | Add your key to the agent for automatic authentication |
| `alias ssha='eval $(ssh-agent) && ssh-add'` | Create an alias for automatic key authentication |

With these steps, you can securely manage SSH connections for both manual administration and Ansible automation.

