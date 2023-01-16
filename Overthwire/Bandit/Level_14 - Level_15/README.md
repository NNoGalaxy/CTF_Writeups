Goal : `The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.`

Solution:
Pretty straightforward. From previous levels we can tell that the password of the current level can be found in `/etc/band_pass/bandit14` 
```sh
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
```
And then we can use nc to do the job:

```sh
nc localhost 3000 
...
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
```

I personally did:

```sh
echo "fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq" | nc localhost 30000
```

Password : jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

