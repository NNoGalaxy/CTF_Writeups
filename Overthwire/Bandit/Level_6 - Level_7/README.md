Goal : `The password for the next level is stored somewhere on the server and has all of the following properties:`

`owned by user bandit7`
`owned by group bandit6`
`33 bytes in size`

Solution : 

Just like the last challenge we'll be using the find command : 
 

 ```sh
find / -type f -user bandit7 -group bandit6 -size 33c 
```

Password : z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S

