# wsl2proxy

The repo contains bash scripts to configure your WSL2 environment,
so to utilize the proxy server running on local Windows for http, https & git
connections.

# Why This Repo

The WSL2 is currently unable to access ports listened by Windows programs via
`localhost`. Instead, programs in WSL2 have to connect to a dynamic IP address
assigned automatically and changes everytime your compute reboots.

This is quite annoying.

The scripts here fetches the latest Windows IP on WSL2's startup (or anytime you
prefer) once properly setup, and assign the IP & port to:

-   `http_proxy` environment variable
-   `https_proxy` environment variable
-   `http.proxy` in `.gitconfig`
-   `https.proxy` in `.gitconfig`
-   `core.gitproxy` in `.gitconfig`
-   a helper executable script named `socksproxy`, which essentially calls the `nc`
    command for proxying SSH connections.

# How To Use

You can run this command to download and install the latest script:

```bash
# English Version

sudo bash -c ''

# Chinese Version
```
