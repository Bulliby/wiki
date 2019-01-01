<!-- TITLE: Duplicity -->
<!-- SUBTITLE: Some information on the duplicity configuration -->

# Duplicity

## GPG

### Create gpg key pair

* `gpg --full-gen-key`

The default are good except for expiration...

### Get gpg key  list

* `gpg --list-keys`

The ID of the key often needed is on the second line of each key's list block.

### Export your public key

* `gpg --output public.key --armor --export Key-ID`

### Save your private key

* `gpg --export-secret-keys --armor Key-ID > privkey.rsa`

> keep it safe

## Duplicity

### Protocol

Choose the protocol you want to use (e.g *file* or *sftp*). For a local backup (e.g on an hard drive) choose **file**.

Here is a sample of the script i use for my local backup :

```sh
#!/bin/zsh

export PASSPHRASE='Ma passphrase'

duplicity --encrypt-key Key-ID --full-if-older-than 1M --include-filelist /home/bulliby/backup/files / file:///mnt/backup
duplicity remove-all-but-n-full --encrypt-key Key-ID --force 2 file:///mnt/backup

unset PASSPHRASE
```


For details on how this works check : [duplicity_doc](http://duplicity.nongnu.org/duplicity.1.html)

I used this tutorial : [digital](https://www.digitalocean.com/community/tutorials/how-to-use-duplicity-with-gpg-to-securely-automate-backups-on-ubuntu)
