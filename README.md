# backup-prepare

## What is does?

You give it a directory and it will create a folder of name current date and time (`YYYYmmdd-HHMMSS`) inside and links `latest` to its location. When the script is executed next time, the whole content of `latest` is hard linked into the newly created folder, so that it does not take additional disk space.

After this is done, you can run `rsync`, that will incrementally change only modified files and the rest is kept unchanged. The effect is that in the end you have multiple full backups which take only a fraction of space that it would if you were to copy all content.

## How to use?

```
Usage: ./backup-prepare [-h] [-f] [-m NUM] dir
-h      ... prints this message
-f      ... forces actions, does not ask for deletion confirmation
-m NUM  ... keep max last NUM of backups, delete older
dir     ... directory in which the backup will be created
```



