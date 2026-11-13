# 0-transfer_file

A Bash script that transfers a file from your local machine (the client) to a remote server using `scp`.

## Description

`0-transfer_file` copies a file to the home directory (`~/`) of a user on a remote server. It authenticates with an SSH private key and has strict host key checking disabled, so it won't stop to ask you to confirm the server's fingerprint.

## Requirements

- Bash
- `scp` (part of OpenSSH)
- An SSH private key that has access to the server
- The server's IP address and a valid username

## Usage

```bash
./0-transfer_file PATH_TO_FILE IP USERNAME PATH_TO_SSH_KEY
```

### Parameters

| # | Parameter         | Description                                  |
|---|-------------------|----------------------------------------------|
| 1 | `PATH_TO_FILE`    | Path to the file you want to transfer        |
| 2 | `IP`              | IP address of the server                     |
| 3 | `USERNAME`        | Username that `scp` connects with            |
| 4 | `PATH_TO_SSH_KEY` | Path to the SSH private key `scp` uses       |

If fewer than 4 parameters are given, the script prints:

```
Usage: 0-transfer_file PATH_TO_FILE IP USERNAME PATH_TO_SSH_KEY
```

## Example

```bash
$ ./0-transfer_file
Usage: 0-transfer_file PATH_TO_FILE IP USERNAME PATH_TO_SSH_KEY

$ touch some_page.html
$ ./0-transfer_file some_page.html 8.8.8.8 sylvain /vagrant/private_key
some_page.html                                     100%   12     0.1KB/s   00:00

$ ssh ubuntu@8.8.8.8 -i /vagrant/private_key 'ls ~/'
afile
some_page.html
```

## How it works

The script runs:

```bash
scp -o StrictHostKeyChecking=no -i PATH_TO_SSH_KEY PATH_TO_FILE USERNAME@IP:~/
```

- `-o StrictHostKeyChecking=no` disables the host key confirmation prompt
- `-i` selects the private key
- `USERNAME@IP:~/` sends the file to the user's home directory on the server

