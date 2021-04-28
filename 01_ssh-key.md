# SSH key
When connecting to a server, `ssh key` is submitted instead of a password.
* more secure
* can connect without logging in
  
## How to generate
Generate `private key` and `public key`, and need to register(copy) to a server.  
```
# ssh-keygen -t rsa (encryption scheme, default value : rsa)
[abc@abc]$ ssh-keygen

Generating public/private rsa key pair.
Enter file in which to save the key (/home/abc/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/abc/.ssh/id_rsa.
Your public key has been saved in /home/abc/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The key's randomart image is:
+---[RSA 2048]----+
|                 |
|                 |
|                 |
|                 |
|                 |
+----[SHA256]-----+
```
## (SSH connect) Copy the public key
```bash
[abc@abc]$ scp /home/abc/.ssh/id_rsa.pub server@server_id:~/.ssh/authorized_keys_tmp
# change permission in the server (chmod 600)
# If it doesn't work, 
# debug :
# ssh -p 12345 abc@abc_ip -v
# ssh -p 12345 abc@abc_ip -vv
# ssh -p 12345 abc@abc_ip -vvv
```
### And then, in the server,
```bash
[abc@abc]$ cat ~/.ssh/authorized_keys_tmp >> ~/.ssh/authorized_keys
# >> : append
# > : replace
[abc@abc]$ chmod 600 ~/.ssh/authorized_keys
[abc@abc]$ rm ~/.ssh/authorized_keys_tmp
```
## Github
Go to `setting - SSH and GPG keys - New SSH key`  
You can add your public rsa key.
