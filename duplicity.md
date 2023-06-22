---
title: duplicity
description: 
published: true
date: 2023-06-22T17:19:00.744Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:58:10.993Z
---

# Duplicity

## Configure a file system crypted backup
> There is a good tutoiral on digitalocean: [here](https://www.digitalocean.com/community/tutorials/how-to-use-duplicity-with-gpg-to-securely-automate-backups-on-ubuntu)

>You can find the documentation [here](http://duplicity.nongnu.org/docs.html)

### Gnu Privacy Guard (GPG)

To crypt the backup we use *Gpg*.

* First we create a key pair : `gpg --full-gen-key`
> The default configuration are good for standard use.

* You can now get the list of created gpg key pairs :

`gpg --list-keys --keyid-format short`

`--keyid-format short` : print the short keyID. By default list-keys don't show keyID because (default is none on arch-linux).

* Export the secret key : `gpg --export-secret-keys --armor <user-id> > privkey`
and save it in safe external device.

> This will be used on the device where is your backup, to restore it directly.


### Duplicity file to save

With the option `--include-filelist` we can give to duplicity the directory or
field he must backup in the form of a file like this :

```raw
- /home/toto/notneeded
+ /home/toto
* /root
- **
```

> The repository must be listed form the more specific to the more general.

Here we save the home of Toto without the "notneeded" file, the home of root user
and that's all because the `- **` exclude all the rest.


### Launch a System backup with duplicity

```shell

export PASSPHRASE='Ma passphrase'

duplicity --encrypt-key Key-ID --full-if-older-than 1M --include-filelist /home/bulliby/backup/files / file:///mnt/backup

duplicity remove-all-but-n-full --encrypt-key Key-ID --force 2 file:///mnt/backup

unset PASSPHRASE
```

Enter the keyID and configure the backup as your need with the duplicity
[reference](http://duplicity.nongnu.org/duplicity.1.html).

### Restore a file system backup

If your are not on the host where the key-pair is saved. You have to restore
your gpg key-pair (this one was created in GPG part of this tutorial):

 `gpg --import privkey`

You can now launch the following command :

 ```shell
 duplicity --file-to-restore "path/du/fichier" -t 4D file:///home/save /home/target
```

* `--file-to-restore` : Permit to specify a specific file to restore. This file must be to the root of the backup.

* The first parameter is the folder of duplicity backup.

* The second parameter 	is where to restore.

* `-t 4D` : Say to restore the backup like it was 4 days ago.

#### Suppress imported key-pair on backup device

If you restored the backup from the backup device :

Don't forget to suppress the key-pair you imported earlier :

`gpg -delete-secret-and-public-key KeyId`

## Home save on external HDD

### Backup

```bash
#!/bin/bash

if [[ ! -d /root/mymount/save ]]
then
    echo "Ton disque n'est pas monté"
    exit 1
fi

echo "Open keepass to save Hancock files  ? (Yes/No)"
read answer

if [[ $answer == "Yes" ]]; then
    rsync -e "ssh -i ~/.ssh/id_hancock_root -p 14498" root@wellsguillaume.fr:/root/bkp-han.tar /home/bulliby/Documents/
    if [[ $? -ne 0 ]] 
    then
        echo "Hancock havent been save"
    fi
fi

echo "################## The save is starting ################################"

duplicity --full-if-older-than 6M --include-filelist /home/bulliby/.files-save --progress --no-encryption / file:///root/mymount/save
duplicity remove-all-but-n-full 2 --force --progress file:///root/mymount/save

echo "################# The save is done ####################################"

```

### Restore

```bash
 duplicity --file-to-restore "/home/bulliby/Documents/bkp-han.tar" --no-encryption --tempdir=/root/mymount/tmp file:///root/mymount/save /home/bulliby/restore/bkp-han.tar
```

> Set `tempdir` to a folder with large space for large files.
