Goals : `There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new`

Solution:

There is a linux utility called diff, which is made for this exact purpose:
``` 
diff password.old password.new
```
The password after `>` is the one we need.

Password : kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
