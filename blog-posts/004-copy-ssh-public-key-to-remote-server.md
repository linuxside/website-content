---
title: Copy the SSH public key to a remote server
date: 2021-09-25
updated: 2022-04-02
tags: cli, ssh, ssh-copy-id
url: copy-ssh-public-key-to-remote-server
---

This will allow you to connect to an SSH server passwordless by using only with the username and the private key.

---

By [generating private/public key]({{ route('blog_post', {'url': 'generate-ssh-publicprivate-key-pair'}) }}) and using it for authentication, it will improve the security of your SSH server.

By copying the SSH public key to the SSH remote server, it will allow you to connect to that server passwordless (by using only with the username and the private key).

After doing this, I advise you to change the SSH server configuration to disallow username/password logins for further security improvement.

The OS I chose to do this is Ubuntu, but these methods will probably work on most Linux distribution.

1. The ssh-copy-id method

The easiest way to copy the public key is to use the `ssh-copy-id` command.

```bash
ssh-copy-id <user>@<your-remote-host>
```

2. Copy over SSH method (alternative method)

If you do not have access to `ssh-copy-id` command, you can use this:

```bash
cat ~/.ssh/id_rsa.pub | ssh <user>@<your-remote-host> 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
```

3. Copy/paste method (alternative method)

Connect to the remote server:

```bash
ssh <user>@<your-remote-host>
```

Create the `~/.ssh` directory:

```bash
mkdir -p ~/.ssh
```

Open the `~/.ssh/authorized_keys` file:

```bash
nano ~/.ssh/authorized_keys
```

and paste the public that you copied in clipboard.

**Note:** The SSH server configuration must accept the authentication method via public/private key.

**Resources:**
- [Copy your Key to your Raspberry Pi](https://www.raspberrypi.org/documentation/computers/remote-access.html#copy-your-public-key-to-your-raspberry-pi)
- [ssh-copy-id manual](https://man.archlinux.org/man/core/openssh/ssh-copy-id.1.en)
