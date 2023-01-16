Goal : `To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.` 

Solution:
Very interesting challenge....
We have a binary that runs any command we give it as user 20.
We know that passwords are in /etc/bandit_pass from previous challenges.

So we do:
```sh
./bandit20-do cat /etc/bandit_pass/bandit20
```
Simple.

Password : GbKksEFF4yrVs6il55v6gwY5aVje5f0j
