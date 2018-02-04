## GRUB Password

You'll want to create the password using the following command, otherwise it will be stored in plaintext for all to see:
```
grub-mkpasswd-pbkdf2
```
Paste the encrypted long string into the file /etc/grub.d/40_custom together with the set superusers command. Remember to keep the commented lines at the beginning:
```
set superusers="root"
password_pbkdf2 root grub.pbkdf2.sha512.10000.9CA4611006FE96BC77A...
```


-----


## Encrypt Home Directory
```
# As root, install the packages needed
apt install ecryptfs-utils
 
# Add the appropriate kernel module
modprobe ecryptfs
 
# Then add 'ecryptfs' to this file to make it persistant through reboots
vim /etc/modules-load.d/modules.conf
 
# Encrypt the home folder
ecryptfs-migrate-home -u <username>
 
# And then log in as that user, BEFORE REBOOTING
# If you were using dropbox, you'll need to re-login
```
Once this is done, you should generate a key for recovery, by running  ```ecryptfs-unwrap-passphrase``` as the encrypted user.

For complete protection, if you can live without hibernate/resume capabilities, you can encrypt your swap space (you’ll still keep suspend/resume) by running  ```ecryptfs-setup-swap```.

Note: While you can set this up for the root user, do not do this, and make sure you only update software from the account that has had it’s files encrypted. Otherwise, when updates need to make changes to your .config directory, they won’t be able to, and you may be left with an unusable account. I learnt this the hard way. For safety, I also recommend adding the following to your root’s .bashrc:

```
alias apt="echo \"Are you about to break something? If you're SURE, use apt-unsafe\""
alias apt-unsafe="apt"
```


-----


## Firewall (UFW)
```
apt install ufw gufw
ufw enable
ufw default deny incoming
ufw default allow outgoing
ufw allow ssh

# Confirm it's all working
ufw status verbose
```

### Allow Port Ranges
Port ranges may also be specified, a simple example for tcp would be:
```
ufw allow 1000:2000/tcp

# and for udp:

ufw allow 1000:2000/udp

# An IP address may also be used:

ufw allow from 111.222.333.444
```

### Deleting Rules
Rules may be deleted with the following command:

```ufw delete allow ssh```

-----

