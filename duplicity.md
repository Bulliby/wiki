# Duplicity

## Configure a file system crypted backup
> There is a good tutoiral on digitalocean:
[here](https://www.digitalocean.com/community/tutorials/how-to-use-duplicity-with-gpg-to-securely-automate-backups-on-ubuntu)

### Gnu Privacy Guard (GPG)

To crypt the backup we use *Gpg*.

* First we create a key pair : `gpg --full-gen-key`
> The default configuration are good for standard use.

* You can now get the list of created gpg key pairs :
`gpg --list-keys --keyid-format short`
  * `--keyid-format short` : print the short keyID. By default list-keys don't
  show keyID because (default is none on arch-linux).

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

```sh

export PASSPHRASE='Ma passphrase'

duplicity --encrypt-key Key-ID --full-if-older-than 1M \
--include-filelist /home/bulliby/backup/files / file:///mnt/backup

duplicity remove-all-but-n-full --encrypt-key Key-ID \
--force 2 file:///mnt/backup

unset PASSPHRASE
```

Enter the keyID and configure the backup as your need with the duplicity
[reference](http://duplicity.nongnu.org/duplicity.1.html).

## Restore a file system backup

* If your are not on the host where the key-pair is saved. You have to restore
your gpg key-pair (this one was created in GPG part of this tutorial):
 `gpg --import privkey`

* You can now launch the following command :

 ```sh
 duplicity --file-to-restore "path/du/fichier" -t 4D \
file:///home/save /home/target
```
  * `--file-to-restore` : Permit to specify a specific file to restore. The path
  is relative the first mandatory argument of the duplicity's backup command.
  In our case root : `/`. That's why we don't use a path starting with `/`.

* `-t 4D` : Say to restore the backup like it was 4 days ago.

### Suppress imported key-pair on backup device

If you restored the backup from the backup device :

* Don't forget to suppress the key-pair you imported earlier :
`gpg -delete-secret-and-public-key KeyId`