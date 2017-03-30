# BACKUP

Backup the LUKS header, this is extremely important and comes in handy when a passphrase is changed and forgotten or the header becomes corrupt:

`cryptsetup luksHeaderBackup --header-backup-file {hostname_partition}_header.bin /dev/xvdb1`

Backup the master key incase a passphrase is forgotten, this should be stored either on an encrypted USB or in a safe somewhere:

`cryptsetup luksDump --dump-master-key /dev/xvdb1`

# RESTORE
Restore a header from a backup file:

`cryptsetup luksHeaderRestore /dev/xvdb1 --header-backup-file=testServer1_home_header.bin`

If you do not have a header backup and have forgotten the passphrase but have a valid master key you can do the following:

Convert it to binary first
`echo "2fss..key..3fad" | xxd -r -p > key.bin`

Header is OK:
`cryptsetup luksAddKey --master-key-file key.bin /dev/xvdb1`
This will add a new key in one  of the 8 keyslots available, if they are all taken it will overwrite one.

Header is not OK:

`cryptsetup luksFormat --master-key-file key.bin /dev/xvdb1`
This should create a new header with the master key we had in backup

If none of the above work i.e. you didnt have a component in backup then it is very difficult at this time to get your data back. You would be in the same shoes as an attacker...
