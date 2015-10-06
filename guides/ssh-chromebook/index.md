---
title: Using SSH on a Chromebook to connect to your Koding VM
author: Team Koding, Gregory Dillon edit to Secure Shell method
categories: [koding features, ssh]
---

In this guide, we will cover how to set up ssh on your Chromebook. Install [Google's SSH
Chrome extention](https://chrome.google.com/webstore/detail/secure-shell/pnhechapfaindjhompbnflcldabbghjo)

### Step 1a: Install Secure Shell or Check its installed

### Step 1b: Choose your editor  (suggestion Caret)

https://chrome.google.com/webstore/detail/caret/fljalecfjciodhpcledpamjachpmelml?utm_source=chrome-app-launcher-search

Verify you have Secure Shell and Caret installed

The Secure Shell looks like


Caret looks like




### Step 2: Generate the required ssh private and public keys on your VM
> type:tip
> If you already have a private and public key generated, you can
skip the section below

Open up Terminal on your Koding VM and type in the following command:
```
ssh-keygen
(no spaces)
```
You will be presented with a few choices, accept all defaults until
you end up with something like this:
```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/your_username/.ssh/id_rsa):
Created directory '/home/your_username/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/your_username/.ssh/id_rsa.
Your public key has been saved in /home/your_username/.ssh/id_rsa.pub.
The key fingerprint is:
7a:36:29:6d:9d:5c:45:5a:8b:53:c0:1a:61:29:3f:ce your_username@your_username
The key's randomart image is:
+--[ RSA 2048]----+
|          o+..+  |
|        ..o .* . |
|         o o+ o  |
|          +  o   |
|        So ..    |
|       o +Eo     |
|      o B +      |
|       = .       |
|                 |
+-----------------+
```

### Step 3: Copy the contents of id_rsa.pub into an authorized_keys file.


Create an `authorized_keys` file (if it does not exist)
```
touch ~/.ssh/authorized_keys
```

Copy the public key into it.

```
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

### Step 4: Moving the generated private key to your Chromebook
To achieve this, we will open the file id_rsa.pub in the Koding VM
select all the file Ctrl-A
Copy all the file Ctrl-C
open a new document in Caret
paste into the Caret Document
Using Caret, save file as id_rsa.pub

Do the same steps for id_rsa
Copy all the file Ctrl-C
open a new document in Caret
paste into the Caret Document
Using Caret, save file as id_rsa

## Step 5
back in Koding, get the web url of your VM by
click here

It will open the below, and copy
copy this



yourusername.koding.io/id_rsa
```
![save-as](save-as.png)

Make sure you have the file without the .txt extension. You can check/rename
the file by using the `Files` app on your Chromebook (as seen in the screenshot
below).
![finder](finder.png)

As soon as the file is downloaded on your Chromebook, delete it from
the Web folder of your VM
```
rm ~/Web/id_rsa
```

At this point, you now have the generated private key on your Chromebook
and are ready to connect.

Press `ctrl-alt-T` to bring up `crosh` and then on the crosh shell, type `ssh`
Use the following commands to set up ssh:
```
host = your_koding_username.koding.io
user = your_koding_username
key = id_rsa
```
![connect](connect.png)

Once you press enter, you should be dropped into your Koding VM!
![connect](connected.png)
