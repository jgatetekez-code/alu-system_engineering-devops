 alu-system_engineering-devops

This is my work for the System Engineering & DevOps track at ALU. I'm using it to learn how servers actually work, starting with the basics of getting into one securely.

 ssh

This folder is about SSH, the tool that lets me log in to a remote server from my own terminal. Instead of typing a password every time, I use a private key, which is safer and a lot faster once it's set up.

 The server I'm working with

- **Name:** 7323-web-01
- **User:** ubuntu
- **IP:** 3.9.176.117

 What's inside

**`0-use_a_private_key`**: a short Bash script that logs me in to the server as `ubuntu` using my private key at `~/.ssh/school`. It only uses single-character ssh flags (`-i`), and it doesn't use `-l`, since the user is given directly in `ubuntu@3.9.176.117`.

 How to run it

Make the script executable once, then run it:


chmod +x ssh/0-use_a_private_key
./ssh/0-use_a_private_key


If it works, you'll land in a prompt like `ubuntu@server:~$`. Type `exit` to leave.

 If something goes wrong

- **"Permissions are too open":** ssh is strict about keys. Fix it with `chmod 600 ~/.ssh/school`.
- **Connection times out:** check that the server is running and that port 22 is open in the security group.
- **First-time fingerprint prompt:** this is normal, just type `yes`.

 Project rules I followed

- Tested on Ubuntu 20.04 LTS
- Written in vi/vim/emacs
- Every file ends with a new line
- Bash scripts are executable, start with `#!/usr/bin/env bash`, and have a comment on line 2 explaining what they do


