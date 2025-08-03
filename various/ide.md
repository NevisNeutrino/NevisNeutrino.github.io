---
layout: page
title: IDEs
subtitle: Setting up ide configurations
description: All about IDEs
hero_height: is-medium
toc: true
toc_title: IDEs
---




Integrated Development Environment (IDE) Guide
========================================================================

As someone who is used to working in a GUI environment, it can be difficult to do everything using the terminal. IDEs offer a GUI-like solution, where one can easily navigate through the remote machine for code editing and execution.

1 - Virtual Studio Code (VS Code)
-----------------------------------------------------------------------------

[VS Code](https://code.visualstudio.com/) is offered on all three platforms and offers many useful features.

It automatically reads the `.ssh/config` when used with the *Remote - SSH* extension. It also manages port forwarding, an useful feature when using Jupyter. git support makes version control easy as well.

### Setting up VS Code for Windows

VS Code works out of the box for MacOS and Linux. If you are mainly working with WSL in Windows, VS Code has the issue of recognizing your Windows machine as the 'main' machine. 

Therefore, you can copy the `.ssh/config` from your WSL to `C:User/Username/.ssh/config`, or you can let VS Code know to look for the WSL configuration by doing `ctrl+shift+p`, `Remote-SSH: Open SSH Configuration File`, and selecting the [path to your WSL environment](https://superuser.com/questions/1185033/what-is-the-home-directory-on-windows-subsystem-for-linux).

#### Using VS Code with FNAL Machines

Again, this works out of the box for MacOS and Linux. For Windows, you need to make Putty manage your ssh connectiong for FNAL machines using kerberos.

https://stackoverflow.com/questions/56030686/is-it-possible-to-use-kerberos-authentication-with-visual-studio-code-remote


### Copilot

Copilot is GitHub's AI assistant, using different AI models from ChatGPT, Gemini, Claude. [You get a free pro account if you verify that you are a student with github](https://docs.github.com/en/copilot/how-tos/manage-your-account/get-free-access-to-copilot-pro)

2 - Cursor
-----------------------------------------------------------------------------------

I still need to explore [Cursor](https://cursor.com/home). For now it feels like VS Code + Copilot. [You get a year for free](https://cursor.com/students) if you verify that you are a student.