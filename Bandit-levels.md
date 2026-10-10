
# OverTheWire Bandit – Linux Learning Journey

---
## Level 0 → Level 1

### Challenge
The password for the next level is stored in a file called **`readme`**, located in the home directory.

### Solution
```bash
cat readme
```
### Explanation
I used the **`cat`** command, which stands for *concatenate*. It allows me to read and display the contents of a file directly in the terminal.
As the password was stored in a file called **`readme`**, I used `cat` to retrieve its contents.

### Password
**`6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR`**


---
## Level 1 → Level 2

### Challenge
The password for the next level is stored in a file called **`-`**, located in the home directory.

### Solution
```bash
cat /home/bandit1/-
```
### Explanation
I used the `cat` command to read the contents of the file. I also used `pwd` to identify my current working directory so I could specify the absolute path.

### Challenges Faced
I initially tried using `cat -`, but it didn't work as `-` is interpreted as standard input rather than a filename. I then used the absolute path to make it clear that I wanted to read a file named `-`.

### Password
**`PK8fYLZg2hnHSz83plBL1iEPKdD3QToB`**


---
## Level 2 → Level 3

### Challenge
The password for the next level is stored in a file called **`--spaces in this filename--`**, located in the home directory.

### Solution
```bash
cat './--spaces in this filename--'
```
### Explanation
I used the `cat` command to read the contents of the file. As the filename contained spaces, I placed it within quotation marks so that it would be read as one filename rather than separate arguments.

### Challenges Faced
I initially struggled to read the file as I kept receiving a "No such file or directory" error message. After conducting some research, I found that placing quotation marks around filenames containing spaces would resolve the issue.

### Password
**`7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME`**


---
## Level 3 → Level 4

### Challenge
The password for the next level is stored in a hidden file in the **`inhere`** directory.

### Solution
```bash
cd inhere
ls -a
cat ...Hiding-From-You
```
### Explanation
I used the `cd` command to change into the `inhere` directory. I then used `ls -a` to list all the files, including hidden files that begin with a dot (`.`). Once I found the hidden file, I used `cat` to read its contents.

### Password
**`xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq`**


---
## Level 4 → Level 5

### Challenge
The password for the next level is stored in the only human-readable file in the **`inhere`** directory.

### Solution
```bash
cd inhere
file ./*
cat ./-file07
```
### Explanation
I used the `file` command to identify the type of each file within the directory. This allowed me to find which file contained human-readable text. Once I identified the correct file, I used `cat` to read its contents.

### Challenges Faced
I initially wasn't sure which command to use to identify the file type, so I had to conduct some research. I mistakenly tried using `ls -h`, but later found that this is used for displaying human-readable file sizes rather than identifying file types.

### Password
**`6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG`**



---
## Level 5 → Level 6

### Challenge
The password for the next level is stored in a file somewhere under the **`inhere`** directory and has all of the following properties:
- Human-readable
- 1033 bytes in size
- Not executable

### Solution
```bash
find . -type f -size 1033c ! -executable -exec file {} \; | grep text
cat ./maybehere07/.file2
```
### Explanation
I used the `find` command to search for files that matched the requirements. The `-type f` option searches for regular files, `-size 1033c` specifies the exact file size in bytes and `! -executable` excludes executable files. I then used `file` to identify the file types and piped the output into `grep text` to filter the results.

### Challenges Faced
I really struggled with finding the solution to this level. I initially tried using `file ./*`, but realised there were multiple folders to search through. My original approach would have been to check each folder individually and then use `ls -l` to check whether the file was executable. However, this would have taken quite some time, so I researched a more efficient way of finding the file using the `find` command.

### Password
*Not recorded in my original notes.*



---
## Level 6 → Level 7

### Challenge
The password for the next level is stored **somewhere on the server** and has all of the following properties:
- Owned by user `bandit7`
- Owned by group `bandit6`
- 33 bytes in size

### Solution
```bash
find / -type f -group bandit6 -user bandit7 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```
### Explanation
I used the `find` command to search the entire server for a file that matched the requirements. The `-type f` option searches for regular files, while `-user` and `-group` allowed me to specify the owner and group. I also used `-size 33c` to find files that were exactly 33 bytes in size.

The `2>/dev/null` redirects error messages so they don't appear in the terminal.

### Challenges Faced
I had to look through the `man` page to find the appropriate options. Although I initially got the first part right, I kept getting a list of permission errors rather than just the file I needed. I then learned how to use `2>/dev/null` to redirect these error messages.

### Password
**`Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3`**



---
## Level 7 → Level 8

### Challenge
The password for the next level is stored in the file **`data.txt`** next to the word **`millionth`**.

### Solution
```bash
cat data.txt | grep millionth
```
### Explanation
I used the `cat` command to read the contents of the file and then piped (`|`) the output into `grep`, which searched specifically for the word `millionth`. This allowed me to find the line containing the password without having to go through the entire file.

### Password
**`VR1ljMayciFxbnUokuQmJFw6QC9VKtub`**



---
## Level 8 → Level 9

### Challenge
The password for the next level is stored in the file **`data.txt`** and is the only line of text that occurs only once.

### Solution
```bash
sort data.txt | uniq -u
```
### Explanation
I used the `sort` command to arrange the contents of the file so that any repeated lines were placed next to each other. I then piped the output into `uniq -u`, which identifies and displays only the lines that occur once.

Sorting the file first was important because the `uniq` command compares lines that are next to each other.

### Password
**`EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl`**



---
## Level 9 → Level 10

### Challenge
The password for the next level is stored in the file **`data.txt`**, in one of the few human-readable strings, preceded by several `=` characters.

### Solution
```bash
cat data.txt | strings -a | grep "="
```
### Explanation
I used the `cat` command to read the contents of the file and piped the output into `strings`, which extracts readable text from the file. The `-a` option scans the entire file. I then used `grep` to search specifically for the `=` character to find the password.

### Password
**`B0s2khmbT9u0geKuOoVGW3JZKhndE3BG`**



---
## Level 10 → Level 11

### Challenge
The password for the next level is stored in the file **`data.txt`**, which contains Base64 encoded data.

### Solution
```bash
base64 -d data.txt
```
### Explanation
I used the `base64` command with the `-d` option to decode the contents of `data.txt`, which revealed the password for the next level.

### Password
**`pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro`**



---
## Level 11 → Level 12

### Challenge
The password for the next level is stored in the file **`data.txt`**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

### Solution
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
### Explanation
I used the `cat` command to read the contents of the file and piped the output into `tr`, which translates each letter by 13 positions in the alphabet.
Since the text was encoded using ROT13, `'A-Za-z'` represents the original uppercase and lowercase letters, while `'N-ZA-Mn-za-m'` represents those letters shifted by 13 positions.

### Password
**`GROozWPO8QyN0mGrjUkID0WCYkZiQxrN`**




---
## Level 12 → Level 13

### Challenge
The password for the next level is stored in the file **`data.txt`**, which is a hexdump of a file that has been repeatedly compressed.

### Solution
```bash
mktemp -d
cd /tmp/<temporary-directory>
cp ~/data.txt .
xxd -r data.txt data.bin
file data.bin
```

Commands used repeatedly depending on the file type:

```bash
gzip -d filename.gz
bzip2 -d filename
tar -xf filename
file filename
cat data
```

### Explanation
I first used `mktemp -d` to create a temporary directory and copied `data.txt` into it. I then used `xxd -r` to reverse the hexdump and reconstruct the original binary file.

As the file had been compressed multiple times, I used `file` to identify each file type before using the appropriate command to decompress or extract it. I repeated this process until I reached the final ASCII text file and used `cat` to read its contents.

### Challenges Faced
I initially struggled with understanding that the hexdump wasn't simply text that needed the numbers removed. I had to use `xxd -r` to reconstruct the original file.

I also tried using `cat` on compressed files, which returned unreadable characters. I later realised it was better to check the file type first.

Another issue I came across was file extensions. For example, `gzip` wouldn't decompress a file with an unrecognised extension, so I had to rename it using `mv`.

I eventually found it easier to follow the same process each time: **identify the file type, decompress or extract it, then check again.**

### Password
**`qQYQiHOBPR8zR61qxYqX45quvihF2uzk`**




---
## Level 13 → Level 14

### Challenge
The password for the next level is stored in **`/etc/bandit_pass/bandit14`** and can only be read by user `bandit14`. Instead of being given the password directly, I was provided with a private SSH key to log in as bandit14.

### Solution
```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
chmod 600 sshkey.private
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
cat /etc/bandit_pass/bandit14
```

### Explanation
I first used `scp` to securely copy the private SSH key from the Bandit server to my computer. I then used `chmod 600` to change the file permissions so that only the owner could read and write it.

I used `ssh -i` to specify the private key when logging in as bandit14. Once logged in, I used `cat` to read the password file.

### Challenges Faced
I initially struggled with understanding that the private SSH key wasn't the password itself but was used to authenticate me as bandit14.

I also had issues with the file permissions. I first tried using `chmod +x`, but this made the key executable rather than restricting its permissions. SSH continued to reject the key until I used `chmod 600`.

Another issue I came across was understanding that `/etc/bandit_pass/bandit14` was a file rather than a directory. I initially tried using `cd` before realising I needed `cat` to read its contents.

### Password
**`aaWecNkG4FhxJQxz07uiwzVP6bJiYS65`**



---
## Level 14 → Level 15

### Challenge
The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.

### Solution
```bash
nc localhost 30000
```

### Explanation
I used the `nc` command, which stands for *Netcat*, to connect to localhost on port 30000. Once connected, I entered my current password, which returned the password for the next level.

`localhost` refers to the machine I was currently connected to, which in this case was the Bandit server.

### Challenges Faced
I initially struggled with understanding how to use the `nc` command from the man page. I first tried `nc localhost -p 30000` because I thought `-p` was used to specify the destination port.

I later found that `-p` specifies the source port, whereas the destination port is simply placed after the hostname.

I also learned how to read the synopsis in a man page, which shows the command syntax and uses square brackets to indicate optional arguments.

### Password
**`pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7`**





---
## Level 15 → Level 16

### Challenge
The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost using SSL/TLS encryption**.

### Solution
```bash
openssl s_client -connect localhost:30001
```

### Explanation
I used `openssl`, which is a toolkit used for cryptography and secure connections such as TLS. The `s_client` command allows me to act as a client and connect to a server using SSL/TLS.

The `-connect` option specifies where I want to connect, while `localhost:30001` specifies the hostname and port number.

Once connected, I entered my current password to retrieve the password for the next level.

### Challenges Faced
I initially struggled with understanding the syntax of this command. At first, I didn't realise that `openssl` and `s_client` had to be used together. I later understood that OpenSSL is the overall toolkit, while `s_client` is one of its commands used to establish SSL/TLS connections.

I also forgot to place a colon between `localhost` and `30001`. Unlike Netcat, where I used `nc localhost 30000`, OpenSSL expects the hostname and port in the format `host:port`.

### Password
**`kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V`**




---
## Level 16 → Level 17

### Challenge
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range **31000 to 32000**. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don't. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

### Solution
```bash
nmap -p 31000-32000 localhost
openssl s_client -connect localhost:31790 -quiet
```

### Explanation
I used the `nmap` command to scan the specified range of ports and find which ones were open. The `-p` option allowed me to specify the range I wanted to scan, while `localhost` referred to the machine I was currently connected to.

Once I identified the open ports, I used `openssl s_client` to establish an SSL/TLS connection. The `-connect` option specifies the hostname and port, while `-quiet` reduces the amount of information displayed in the terminal.

### Challenges Faced
I initially struggled with understanding how to specify a range of ports using `nmap`, so I looked through the `man` page and tried a few different commands.

For example, I initially tried `nmap -p 31000 32000`, but this didn't work because I hadn't specified the range correctly. I later realised I needed to place a hyphen between the two port numbers and include `localhost`.

I also had some difficulty with the OpenSSL syntax. I initially entered the hostname and port separately, which returned an error message. I corrected this by placing a colon between `localhost` and the port number.

### Password
**This level provided a private SSH key rather than a password.**




---
## Level 17 → Level 18

### Challenge
There are 2 files in the homedirectory: **`passwords.old`** and **`passwords.new`**. The password for the next level is in `passwords.new` and is the only line that has been changed between `passwords.old` and `passwords.new`.

### Solution
```bash
diff passwords.new passwords.old
```

### Explanation
I used the `diff` command to compare the contents of both files and identify the line that had changed. The `<` symbol represents the line from the first file, which in this case was `passwords.new`, while `>` represents the line from the second file.

### Challenges Faced
This level was straightforward. I used the `man` page to check how the `diff` command worked before comparing the two files.

### Password
**`0QxXZjELndr90zuh0TDYBEomI0SZITXI`**




---
## Level 18 → Level 19

### Challenge
The password for the next level is stored in a file **`readme`** in the homedirectory. Unfortunately, someone has modified **`.bashrc`** to log you out when you log in with SSH.

### Solution
```bash
ssh -t bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```

### Explanation
I used the `ssh` command to connect to the Bandit server. Rather than logging in first and then using `cat`, I placed the command directly at the end of SSH so it would execute on the remote server.

The `-t` option requests a terminal, while `-p 2220` specifies the port number. This allowed me to read the contents of `readme` without needing to remain logged into an interactive shell.

### Challenges Faced
I initially tried logging into bandit18 as I normally would, but every time I logged in, the connection immediately closed and displayed a goodbye message.

I wasn't too sure how I was meant to access the file if I couldn't stay logged in, so I looked through the SSH manual to find another way. I then tried placing `cat readme` directly at the end of the SSH command, which allowed me to retrieve the password.

### What I Learned
I learned that SSH can also be used to execute a command directly on a remote server rather than having to log in first and enter the command separately.

### Password
**`qOg5pVOjPx9x9VccyYBADiT4xxyoUB8D`**



---
## Level 19 → Level 20

### Challenge
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (`/etc/bandit_pass`), after you have used the setuid binary.

### Solution
```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

### Explanation
The `bandit20-do` file is a setuid binary which allows me to execute a command with the permissions of its owner, in this case `bandit20`.

I used `./bandit20-do` followed by the `cat` command and the absolute path to the password file. This allowed me to read the password, which I wouldn't normally have permission to access as `bandit19`.

### Challenges Faced
I initially struggled with understanding how to use the setuid binary. I first executed it without any arguments and then tried `./bandit20-do whoami`, which returned `bandit20`.

Although this showed me that the binary was running with bandit20's permissions, I wasn't too sure how to use it to retrieve the password.

I initially tried changing the permissions using `chmod +x`, but received an operation not permitted error. I also tried accessing the password file directly but kept receiving permission errors.

I eventually realised I needed to use the setuid binary itself to execute `cat`, rather than trying to access the password file directly.

### What I Learned
I learned that a setuid binary can allow a program to run with its owner's permissions rather than those of the user executing it.

### Password
**`4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA`**


---
## Level 20 → Level 21

### Challenge
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

**NOTE:** Try connecting to your own network daemon to see if it works as you think.

### Solution
```bash
nc -l 5002
```
I suspended Netcat using `Ctrl + Z` and then ran:

```bash
./suconnect 5002
```
I suspended this as well and used:

```bash
jobs
bg %2
fg %1
```
I entered my current password into Netcat. Once it matched, I used `fg %1` to retrieve the next password.

### Explanation
I used `nc -l` to listen for an incoming connection on port 5002 and then used `suconnect` to connect to the same port.

I also made use of Unix job control to manage both processes within the same terminal. `Ctrl + Z` suspends a process, `bg` resumes it in the background, while `fg` brings it back into the foreground.

### Challenges Faced
I really struggled with understanding how to get both commands working together. Whenever I ran Netcat, it occupied my terminal, so I wasn't sure how to execute `suconnect` at the same time.

I had to look into Unix job control and experimented with `Ctrl + Z`, `bg` and `fg`. I initially ended up with several suspended jobs and had to clear them using `kill` before starting again.

Another thing that confused me was how the programs could connect if one was suspended. I later understood that suspending a process pauses it rather than terminating it.

### What I Learned
I learned how to manage multiple processes within the same terminal using Unix job control. I also learned how to use Netcat to listen for incoming connections rather than connecting to an existing port.

### Password
**`bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY`**






