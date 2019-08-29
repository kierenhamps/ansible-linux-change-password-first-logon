# ANSIBLE-LINUX-CHANGE-PASSWORD-FIRST-LOGON

Demo playbook to show the posibility of using expect within ansible to change a remote systems password.

## Scenario

 - you have a remote system that is set with a default password
 - when you login for the first time it prompts you for a change of password (i.e. the account has expired)
 - if you manage to log on with the old password and are not prompted change the password anyway.

## Requires

- expect & tcl from base

## Flow

1. Log in using **ansible_user** and **ansible_password** and check you are given a command prompt.
   Save results in variable **rhel_logon_check**

2. If **rhel_logon_check.failed** == True (i.e. you were not able to log in using new creds in 1st step)

   Log in using **ansible_user** and **ansible_old_password** and check for either a password prompt or command prompt.
   - If a password prompt, then re-enter **ansible_old_password** and continue to change using **ansible_password**
   - If a command prompt, then issue the "passwd" command and continue to change using the **ansible_password**
