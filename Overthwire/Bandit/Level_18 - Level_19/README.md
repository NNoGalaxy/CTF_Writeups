Goals : `the password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.`

Solution:
So the bash shell has blocks us from logging in. why no just use a different shell?

```sh
cat /etc/shells
```

This shows us all our available shells.
And we can use one of them like this :

```sh
ssh bandit18@bandit.labs.overthewire.org -p 2220 -t "/bin/sh"
```
And put our password in and boom. we're logged in. `cat readme` ftw!!


Password : IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x


