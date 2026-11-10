# 0x0F. Load balancer / web_server

This directory is part of the `alu-system_engineering-devops` repository. It covers basic web server tasks: moving files from a local machine (client) to a remote server.

## Files

| File | Description |
|------|-------------|
| `0-transfer_file` | Bash script that transfers a file to a server's home directory using `scp` |

## 0-transfer_file

Transfers a file from the client to a server over SCP.

### Usage

```bash
./0-transfer_file PATH_TO_FILE IP USERNAME PATH_TO_SSH_KEY
```

| Parameter | Description |
|-----------|-------------|
| `PATH_TO_FILE` | Path to the file to transfer |
| `IP` | IP address of the server |
| `USERNAME` | Username `scp` connects with |
| `PATH_TO_SSH_KEY` | Path to the SSH private key `scp` uses |

If fewer than 4 parameters are passed, the script prints:

```
Usage: 0-transfer_file PATH_TO_FILE IP USERNAME PATH_TO_SSH_KEY
```

### Behavior

- The file is copied to the user's home directory (`~/`) on the server.
- Strict host key checking is disabled (`-o StrictHostKeyChecking=no`), so there is no fingerprint prompt.

### Example

```bash
$ ./0-transfer_file
Usage: 0-transfer_file PATH_TO_FILE IP USERNAME PATH_TO_SSH_KEY

$ touch some_page.html
$ ./0-transfer_file some_page.html 8.8.8.8 ubuntu /vagrant/private_key
some_page.html                                     100%   12     0.1KB/s   00:00

$ ssh ubuntu@8.8.8.8 -i /vagrant/private_key 'ls ~/'
afile
some_page.html
```

### Requirements

- Bash (run from WSL, Git Bash, or Linux/macOS)
- `scp` / OpenSSH client installed
- Private key with correct permissions: `chmod 600 /path/to/private_key`
- Script must be executable: `chmod +x 0-transfer_file`
- Unix (LF) line endings
