# BACKUP

Backup the LUKS header, this is extremely important and comes in handy when a passphrase is changed and forgotten or the header becomes corrupt:

cryptsetup luksHeaderBackup --header-backup-file {hostname_partition}_header.bin /dev/xvdb1

Backup the master key incase a passphrase is forgotten, this should be stored either on an encrypted USB or in a safe somewhere:

cryptsetup luksDump --dump-master-key /dev/xvdb1

# RESTORE
