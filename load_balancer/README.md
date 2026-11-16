# Load Balancer

This project is part of the ALU System Engineering & DevOps curriculum. It
covers placing web servers behind a load balancer and tracking which server
answers each HTTP request.

## Files

| File | Description |
|------|-------------|
| `0-custom_http_response_header` | Bash script that configures a brand new Ubuntu machine with Nginx and a custom HTTP response header |

## Task 0. Double the number of web servers

The goal is to configure `web-02` to be identical to `web-01`, then add a
custom Nginx response header on both servers so we can tell which one served
a request.

### Requirements

- The header name is `X-Served-By`.
- The header value is the hostname of the server Nginx is running on.
- The script must set up a fresh Ubuntu machine from scratch, so the whole
  process is automated and repeatable on both `web-01` and `web-02`.
- `shellcheck` warning SC2154 is ignored.

### Usage

Run the script on each web server (`web-01` and `web-02`):

    sudo ./0-custom_http_response_header

### Verification

    curl -sI <server-ip> | grep X-Served-By

Example output:

    X-Served-By: 03-web-01
    X-Served-By: 03-web-02
