# backup-prepare

## What is does?

You give it a directory and it will create a folder of name current date and time (`YYYYmmdd-HHMMSS`) inside and links `latest` to its location. When the script is executed next time, the whole content of `latest` is hard linked into the newly created folder, so that it does not take additional disk space.

Also, one can use `-b` param to take use of btrfs snapshots instead of hard-linking everything.

After this is done, you can run `rsync`, that will incrementally change only modified files and the rest is kept unchanged. The effect is that in the end you have multiple full backups which take only a fraction of space that it would if you were to copy all content.

## How to install (or update)

```bash
sudo wget 'https://raw.githubusercontent.com/esoadamo/backup-prepare/main/backup-prepare' -O /usr/bin/backup-prepare
sudo chown root:root /usr/bin/backup-prepare
sudo chmod 755 /usr/bin/backup-prepare
```

## How to use?

```
Usage: ./backup-prepare [-h] [-f] [-d] [-m NUM] action dir
-h      ... prints this message
-f      ... forces actions, does not ask for deletion confirmation
-m NUM  ... keep max last NUM of backups, delete older
-b DIR  ... use btrfs mode and save snapshots into given directory
action  ... prepare | finish | delete
            - prepare  ... creates new directory and in-progress link
            - finish   ... changes latest to in-progress and deletes old backups (in max backups is specified)
            - delete   ... deletes old backups (in max backups is specified)
dir     ... directory in which the backup will be created
```
