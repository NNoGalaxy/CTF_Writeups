Goals : `The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.`

`Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…`





Solution:

I like these simple challenges. 

Just like the last level but with ssl.

We simply do :
```sh
openssl s_client -connect 127.0.0.1:30001
```
then input the password *jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt* and get the password to the next level.

Password : JQttfApK4SeyHwDlI9SXGR50qclOAil1
