Goal : `The password for the next level is stored in the file data.txt and is the only line of text that occurs only once`

Solution : 

```sh
sort data.txt | uniq -u
```

the `sort` command sorts the output based on identical lines. it is often used with `uniq` to filter for unique lines. and the `-u` switch filters for unique lines.
 

Password : EN632PlfYiZbn3PhVK3XOGSlNInNE00t
