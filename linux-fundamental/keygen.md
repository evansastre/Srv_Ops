# Keygen

Generate a new key:

```text
ssh-keygen -t rsa -C "youremail@test.com"
```

The command below can be used to convert an SSH2 private key into the OpenSSH format:

```text
ssh-keygen -i -f path/to/private.key > path/to/new/opensshprivate.key 
```

The command below can be used to convert an SSH2 public key into the OpenSSH format:

```text
ssh-keygen -i -f path/to/publicsshkey.pub >> path/to/publickey.pub 
```

This can also be done in reverse to convert an OpenSSH key into the SSH2 format in the event that a client application requires the other format. This can be done using the following command:  
Private key conversion:

```text
ssh-keygen -e -f path/to/opensshprivatekey/file > path/to/ssh2privatekey/file
```

Public key conversion:

```text
ssh-keygen -e -f path/to/opensshprivatekey/file > path/to/ssh2privatekey/file
```

The most important thing to remember when using these commands are the flags. The -i tells SSH to read an SSH2 key and convert it into the OpenSSH format. The -e parameter tells SSH to read an OpenSSH key file and convert it to SSH2. With these commands you should be able to successfully covert SSH keys between the different formats required by MessageWay as well as other file transfer 

