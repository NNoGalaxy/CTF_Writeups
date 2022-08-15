# like1000

## Description
This [.tar file](https://jupiter.challenges.picoctf.org/static/52084b5ad360b25f9af83933114324e0/1000.tar) got tarred a lot.


## Hint(s)

1. Try and script this, it'll save you a lot of time

## Writeup 
This challenge is pretty straight forward, and with a little bit of shell programming (or python) you can easily solve it.
i used [this](https://zomry1.github.io/like1000/) script and got the flag.
```py

import tarfile #Moudle used to work with tar files

for i in range(999, 0, -1): #For loop from 999 to 0 going down by 1
	filename = str(i) + '.tar' #Get the name of the file
	#print(filename) - just for debug
	tar = tarfile.open(filename) #Open the file
	tar.extractall() #Extract what in the file
	tar.close() #Close the file


```

flag : `picoCTF{l0t5_0f_TAR5}`  