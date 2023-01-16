Goal : `The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:`

`human-readable`

`1033 bytes in size`

`not executable`


Solution:

Heres a link that may help you : https://quickref.me/find

```sh
find . -readable ! -executable -size 1033c
```

Password : P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
