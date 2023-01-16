Goal : `The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.`

Solution: 

Finally, `strings` comes into play.
```sh
strings data.txt | grep =
```
Essentially, `strings` prints out all the strings in a file. and then we use grep to filter the output by lines that contain the character '='.


Password : G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
