smv
===

Secure mv. An equivalent to scp, for *moving* files. It uses `rsync` under the
hood, as an alias, so all the `rsync` options can be used with it.

Installation
------------

> [!NOTE]
>
> These instructions are mainly to restrict the `sshd` access to `smv` only,
> and to have the command `smv` available in your shell. If you just want to
> move files with `rsync`, you don't need all this (just the first step).

1. Install `rysnc` locally and remotely on your server.
2. After `sshd` is configured on the server (port, auth, etc), install
   `ssh-restrict` on the server.
3. Add the following line to your user's `.ssh/authorized_keys` on the server:
   ```
   command="/usr/local/bin/ssh-restrict /usr/bin/rsync",no-port-forwarding,no-agent-forwarding,no-X11-forwarding,no-pty ssh-ed25519 AAAA...
   ```
   With the proper (complete) ssh key for the machine you want to use `smv` on.
> [!IMPORTANT]
>
> The path of `/usr/bin/rsync` in the command has to reflect the one on your
> system, or `smv` won't work. Also, obviously, set the path of
> `ssh-restrict` to the right location.
4. Add the following alias to your `.${SHELL}rc`:
   ```sh
   alias smv='rsync --remove-source-files'
   ```

Usage
-----

```sh
$ smv -r some_dir some.remote.host:
```
