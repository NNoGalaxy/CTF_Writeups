Goal : `The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)`

Solution:
I think we all hate this level.
First we do what the goal says, 
```sh
mkdir /tmp/datafile
cp data.txt /tmp/datafile
cd /tmp/datafile
```
Remember, our file is a hexdump. there is a script called `xxd` which makes hex dumps or reverse. we use it to turn our `.txt` file into a `bin` file.
```sh
xxd -r data.txt > data.bin
```
Now if we do `file data.bin` it says that our file is *gzip compressed*.
we decompress this with `zcat` :

```sh
zcat data.bin > data2
```

Using the `file` command again, it tells us that its a *bzip2 compressed file*.
We can use `bzcat` to decompress it.

```sh
bzcat data2 > data3
```
Now our file is a gzip file again, so we use `zcat`
```sh
zcat data3 > data4
```
Data4 is a *POSIX tar archive*
we use `tar` to decompress it.
```sh
tar -xvf data4
```
options x is used to extract an archive, f is used to specify name of the tar archive and v is used for more detailed listing.

Now that gives us `data5.bin` which is again a *tar archive*. so we use tar again.
That gives us data6.bin which is *bzip2 compressed*.
```sh
bzcat data6.bin > data5
```

Decompressing it gives us a tar file.
And then from here its a *tar archive*, to a *gzip compressed file*, and last, to what we're looking for.
I know. frustrating. I was aswell. 

Password : wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
