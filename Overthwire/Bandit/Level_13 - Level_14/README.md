Goal : `The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on`

Solution:

This level is fairly simple. 
We save the ssh private key on our local system and call it `sshkey.private` and then use this command to log in to bandit14 :
```sh
sudo ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

Well done.
