# Setup SSH login with private key instead using password everytime.

Everytime, Password has been used to login to linux server, which is sometime hectic to type every single time we login. Using SSH pub/private key pair, password
can be skipped.

## create SSH key pair
Be on your localhost/computer and create SSH key pair. Type following command and follow the instructions.

```sh
# Change directory to `.ssh`
cd ~/.ssh

# 
ssh-keygen
```
**Example:**
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/username/.ssh/id_ed25519): `my_ssh_key`

It creates both private key and public key visible in folder `~/.ssh`

Now, Copy public key ex: `my_ssh_key.pub` to destination server which is remote linux server. `ssh-copy-id` can do this.

```sh
ssh-copy-id -i ~/.ssh/my_ssh_key.pub -p 5522 username@1.1.1.1
```

> Note: -p 5522 is port of the server

`ssh-copy-id` will copy the specified public key (my_ssh_key.pub) to the remote server's `authorized_keys` file and set you up for key-based authentication.

Now, Login without entering password 

```sh
ssh username@1.1.1.1 -p 5522
```

