---
layout: page
title: SSH
subtitle: Setting up ssh connection configurations
description: All about SSH
hero_height: is-medium
toc: true
toc_title: SSH
---




SSH Configuration Guide
========================================================================

Log in to a remote machine from terminal by:
```bash
    ssh $USER@$MachineName
```


1 - Setup Nevis SSH Configuration
-----------------------------------------------------------------------------

Each time you will have to enter a password to log in.

Some machines won't be able to access unless you set up a proxy or Nevis VPN.

In your `.ssh/config`, add these lines:

```bash
    Host $MAIN_ALIAS$
        HostName $MAIN$.nevis.columbia.edu
        User $USERNAME$

    Host $OTHER_ALIAS$
        HostName $OTHER$.nevis.columbia.edu
        User $USERNAME$
        ProxyJump $MAIN_ALIAS$
```
This allows you to connect to a Nevis machine with the following command:

```bash
    ssh $OTHER_ALIAS$
```

To log in each time without re-entering your password, you can use `ssh-keygen`.

```bash
    ssh-keygen
    ssh-copy-id -i $KEY_PATH $REMOTE_ALIAS # Where the $KEY_PATH is generated from the above line, $REMOTE_ALIAS is what is set in .ssh/config
```

Repeat this for any remote server you want to login to without password.

## Setup ssh for Windows

To do terminal-based operations on Windows, one can use Windows Subsystem for Linux (WSL), which offers a native linux kernel besides the Windows environment.

One can also work entirely using Powershell or Putty, using it only as means for remote connection, as most of the bash commands are not compatible.

Note that WSL and the native Windows shell are treated as different machines. You need to repeat the process of configuring your ssh for both.

The only difference is that Powershell does not support `ssh-copy-id`, [instead do](https://superuser.com/questions/1747549/alternative-to-ssh-copy-id-on-windows):

```bash
    ssh-keygen
    C:\> type %USERPROFILE%\.ssh\id_rsa.pub | ssh user@host "cat >> .ssh/authorized_keys"
```


2 - Setup FNAL SSH Configuration
-----------------------------------------------------------------------------------

The same principle applies to setting up ssh for FNAL machines.

Note that for Windows, it is hard to get the Windows shell working with kerberos, FNAL's version of password identification.

The [offical recommendation](https://fermi.servicenowservices.com/kb_view.do?sysparm_article=KB0011316) is to use Putty.

Note that this is needed to use VS Code with FNAL machines in Windows.

Refer to the [SBN Young Guide](https://sbnsoftware.github.io/SBNYoung/Basic_Computing.html) as well.
