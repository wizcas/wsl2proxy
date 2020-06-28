# WSL2Proxy

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

Once Microsft addresses the issue, there should be no more use of these scripts.

# How To Use

## Installation

### One-liner Installation

You can run this command to download and install the latest script:

```bash
# The English Version
wget -O w2p.sh -q https://git.io/JJvv5 && sudo bash w2p.sh install

# Or the Chinese Version
wget -O w2p.sh -q https://git.io/JJvv7 && sudo bash w2p.sh install
```

### Manually Installation

You can also clone the repo and install a script manually:

```bash

$ git clone https://github.com/wizcas/wsl2proxy.git
$ cd wsl2proxy

# The English Version
$ sudo bash ./wsl2proxy-en install
# Or The Chinese Version
$ sudo bash ./wsl2proxy-zh install

```

### Setup Proxy Settings

Before activating the WSL2Proxy you'll have to provide proxy settings first,
including:

-   Proxy protocol
-   Proxy port

No need to provide the proxy IP here because WSL2Proxy takes care of it automatically!

Run this command and follow the instructions to setup:

```bash
$ wsl2proxy setup
```

> The settings are saved at `~/.wsl2proxy.conf`, if you concern.

## Enable/Disable WSL2Proxy

### Manually Enabling

Run this command (**don't miss the leading `.`, or environment variables will be set only in forked child process**):

```bash
. wsl2proxy on
```

### Manually Disabling

Run this command (**don't miss the leading `.`, or environment variables will be set only in forked child process**):

```bash
. wsl2proxy off
```

### Auto Enabling on WSL2 Startup

And add this line to your shell startup script (`.bashrc`, `.zshrc`, etc.):

```
. wsl2proxy on
```

### SSH Proxying

The script generates a helper script named `socksproxy` in your home directory. It is used
for easy SSH proxying.

Say, I want all the ssh connections with `github.com` are through my proxy server,
so to enable my proxy server for `git@github.com:...`.
Just edit the `~/.ssh/config` file and add lines like this:

```
Host github.com
    User git
    ProxyCommand ~/socksproxy '%h %p'
```

**Note that** the script is not responsible for modifying `.ssh/config` automatically. You'll
have to set the correct permission for this file after any modification. And you'll need to remove
the proxy settings within manually for disabling SSH proxying.

## Uninstall

1. Remove the `. wsl2proxy on` line from your shell startup script if ever added.
2. Remove the proxy settings from `~/.ssh/config` if the changes are ever made.
3. Delete `/usr/local/bin/wsl2proxy`.
