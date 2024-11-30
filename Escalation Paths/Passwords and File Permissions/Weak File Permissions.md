When we're looking for weak file permissions, what we're looking for is do we have access to a file that we shouldn't. Do we have rights to execute a file that we should not be able to. Can we do anything malicious with files that we shouldn't be able to access?

To see what permissions you have as a user to a specific file, you run the following command:

```shell
ls -la <path_of_file>
```

In this case, we will be looking into /etc/passwd and /etc/shadow

The /etc/shadow file should not have any read access to a low level user. The read write access should only be restricted to the root user.

/etc/passwd being called password does not actually contain any passwords. This file tells us what users are there on the machine, what groups the user is a part of and ids. This file is world readable. The reason why its called the password file, is because earlier it used to actually store passwords. Now, its stored in the shadow file.

Now why is this important?

In the /etc/passwd file, there is a placeholder x for the root user that is used for the password which is stored as a hash in the /etc/shadow file. If we have write access to the /etc/passwd file, we can just remove the X and then become the root without any password.

Now this is important, if you have read access to the passwd and shadow file, you can use a tool called unshadow(built into kali) which basically requires your passwd file and your shadow file and it replaces the hashes in the shadow file into the password file. 

Then, you can use a tool called hashcat to de-hash those hashes using a word-list like rockyou.txt

To find the mode of the hash, you can google hashcat hash types and find the one most similar to the hash you have with you





