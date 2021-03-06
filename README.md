# rds
Remote Distribution Service

A stupid simple, lightweight and secure file and script execution system.

It requires the use of SSH and SUDO (where SUDO is required).

Initially, all files are TAR archived and transferred to a target host, along with a dynamically created execution script.

The TAR archive must include at least one file, "cmds.txt", which will contain any commands required to complete distribution on the target host.

All commands will be executed inside the folder where the files were unarchived by the dynamically created execution script. The files are transferred and unarchived in /tmp into a dynamically created session folder that consists of the time/date, host it came from and a random number to prevent conflicts.

This script could be optimized further, but is only a stop gap tool and I will likely delete it at some point.

Usage...

rds target-host cmds.txt file1 file2 ... filen

The user who runs the "rds" script will have his/her identity used to copy, execute and if needed, SUDO any commands.

Be sure if the user needs to SUDO, that the user can elevate without having to type in credentials (see NOPASSWD option for SUDOERS). 

Since NOPASSWD is a very risky, if almost irresposible setting in SUDO, you will want to supplement your security posture with restrictions on commands that can be executed in either SUDOERS or sshd_config, or both.

At the very least, a Match statement in sshd_config should be used to match the user and source address of the distribution point where the user will be coming from, "Match Address [source] User [user]" to
restrict where the distribution user can come from.

Better yet, require no SUDO capability, drop files in a specific location of your choosing on the target host and have a cron job with the right priveleges complete the distribution.

It is also best to use SSH keys instead of passwords and utilize shd-agent to reduce the typing of key passphrases.

Each initial connection to a remote host, will incur at least one request to add that host to the known_hosts file.

Inside "cmds.txt" it is best to use absolute pathes, any SUDO commands should be listed in this file.

When using the targets list command line arg, the list can be any text file that lists a host on each line, at the beginning of the line, followed by zero or more fields. The fields must be seperated by spaces. The fields following the host specification are all ignored.
