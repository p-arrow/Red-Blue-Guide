**Credits to:** [Ivan](https://ivanitlearning.wordpress.com/2021/10/22/bash-configuration-files/)

- **/etc/profile**: This is a system-wide initialisation file that is executed during login. This file provides initial environment variables and initial “PATH” locations.
- **/etc/bashrc**: This again is a system-wide initialisation file. This file is executed each time a Bash shell is opened by a user. Here you can define your default prompt and add alias information. Values in this file can be overridden by their local ~/.bashrc entry
- **~/.bash_profile**: If this file exists, it is executed automatically after /etc/profile during the login process. This file can be used by each user to add individual entries. The file however is only executed once at login and normally then runs the users .bashrc file.
- **~/.bash_login**: If the .bash_profile does not exist, then this file will be executed automatically at login.
- **~/.profile**: If the .bash_profile or .bash_login do not exist, then this file is executed automatically at login.
- **~/.bashrc**: This file contains individual specific configurations. This file is read at login and also each time a new Bash shell is started. Ideally, this is where you should place any aliases.
- **~/.bash_logout**: This file is executed automatically during logout.
- **~/.inputrc**: This file is used to customize key bindings/key strokes.

<br />

To note: `/etc/profile` is executed for **interactive shells** while `/etc/bashrc` is loaded for both **interactive and non-interactive shells**
