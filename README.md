# rds
Remote Distribution Service

A stupid simple, lightweight and secure file and script execution system.

It requires the use of SSH and SUDO (where SUDO is required).

Initially, all files are TAR archived and transferred to a target host, along with a dynamically created execution script.

The TAR archive must include at least one file, "cmds.txt", which will contain any commands required to complete distribution on the target host.

All commands will be executed inside the folder where the files were unarchived by the dynamically created execution script.

This system is could be optimized further, but is only a stop gap tool and I will likely delete it at some point.

Usage...

rds target-host cmds.txt file1 file2 ... filen

The user who runs the "rds" script will have his/her identity used to copy, execute and if needed, SUDO any commands.

Be sure if the user needs to SUDO, that the user can.

It is also best to use SSH keys instead of passwords and utilize shd-agent to reduce the typing of key passphrases.

Each initial connection to a remote host, will incur at least one request to add that host to the known_hosts file.

Inside "cmds.txt" it is best to use absolute pathes, any SUDO commands should be listed in this file.
