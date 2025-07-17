Cracking Passwords with John the Ripper on Ubuntu

Introduction
As part of my cybersecurity learning journey, I wanted to explore how password cracking works in real life — beyond theory. For this, I used a popular tool called John the Ripper.

In this blog, I’ll walk you through how I installed it on Ubuntu, hashed a few passwords (including my own name), and cracked them successfully. Let’s go!

 What I Used
Ubuntu 22.04 (in VirtualBox)

Terminal access

John the Ripper (installed via apt)

OpenSSL (to generate password hashes)


Step 1: Installing John the Ripper
I opened the terminal and ran:

```bash
sudo apt update
sudo apt install john -y
```
Here’s a snippet from the install logs:
```
kotlin
Get:1 http://gb.archive.ubuntu.com/ubuntu ... john-data ...
Get:2 http://gb.archive.ubuntu.com/ubuntu ... john ...
Unpacking john-data ...
Unpacking john ...
Setting up john ...
```
Everything installed smoothly 

Step 2: Hashing a Sample Password
To simulate a real password hash, I chose the password hello123 and hashed it using OpenSSL:

```bash

echo -n "hello123" | openssl passwd -1 -stdin
```
It returned this hash:


```
$1$oW46TBze$g7IZJSrLMUbkCTmUAnTnB.

```

Then I created a file called myhash.txt:

```bash
nano myhash.txt
```
And added:
```
testuser:$1$oW46TBze$g7IZJSrLMUbkCTmUAnTnB.

```
Saved and exited.

Step 3: Cracking the Hash
I tried running John:

```
john myhash.txt
```
At first, I saw:
```
No password hashes loaded (see FAQ)
```
Oops! Turns out I had a formatting mistake — fixed it, and ran again.

This time:

```
Loaded 1 password hash (md5crypt [MD5 32/64 X2])
Will run 5 OpenMP threads
hello123         (testuser)
Session completed
```
cracked!

To confirm, I ran:
```
john --show myhash.txt
```
Output:
```
testuser:hello123
```
Cracking My Own Name as a Password
Next, I wanted to see what would happen if someone used my name as their password.

So I hashed it:

```
echo -n "pruthviraj" | openssl passwd -1 -stdin

```
Hash returned:

```
$1$CZ8R2I2U$MZBiHlf6DAnkJ00eHijk7.
```
I created a new file:

```
nano mynamehash.txt
```
Added:
```
pruthviraj:$1$CZ8R2I2U$MZBiHlf6DAnkJ00eHijk7.
```
Then ran:
```
john mynamehash.txt
```
And got:
```
pruthviraj       (pruthviraj)
```
Confirmed with:
```
john --show mynamehash.txt
```
Result:
```
pruthviraj:pruthviraj
```
What I Learned

Hashes aren’t encrypted, just one-way obfuscations

Weak passwords like names are super easy to crack

Tools like John can simulate what real attackers do

It's important to use strong, unique passwords


🎯 Final Thoughts
This exercise made password security much more real to me. Cracking hello123 is one thing, but watching my own name get cracked instantly really drove the point home.

If you're learning cybersecurity — don't just read. Do. That's where real understanding happens.


here are some screenshot for exact understanding 
![WhatsApp Image 2025-07-17 at 03 45 59](https://github.com/user-attachments/assets/4c85464e-c2da-4e81-bb17-a8a1132d7054)
![WhatsApp Image 2025-07-17 at 03 45 59 (1)](https://github.com/user-attachments/assets/802ebd0f-ab94-44eb-9801-8c322dacfb6a)




Blog by pruthviraj patil
