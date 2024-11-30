This exploit uses the Payloads all the things website. Under looting for Passwords, there will be a section called SSH key that can be utilized by us.

The first payload that we will be using is:

```bash
find / -name authorized_keys 2> /dev/null
```

This checks if we have any authorized keys in the machine. 

The other payload that we will use is:

```shell
find / -name id_rsa 2> /dev/null
```

Now, why is this relevant? 

With SSH we can do something like:

```shell
ssh-keygen
```

To generate some keys. And these keys come in pairs. One is the Public Key and the other is a Private Key. The public key will be copied to an authorized keys folder and thats how it knows who we are. The private key is something that we store with ourselves.

So, by the 2 payloads, we are seeing if there are any authorized keys that have ssh access or we have a private key stored here. 

So, when you get a private key like that you can ssh as a root 

```shell
ssh -i id_rsa root@<ip>
```