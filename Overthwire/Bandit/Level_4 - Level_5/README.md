Goal : `The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.` 

Solution:

To learn about all the files in the inhere directory we use :

```sh
file ./inhere/*
```
This shows us that file07 is the one with ASCII text. So we print it by:

```sh
cat ./-file07
```


Password : lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR