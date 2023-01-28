# Backup Strategy
This repository contains documentation for the backup strategy used for our system. It includes information on the tools and processes used for creating and maintaining backups, as well as instructions for restoring from backups in case of a failure or data loss.

## Tools
- [Borg Backup](https://borgbackup.readthedocs.io/) - A deduplicating backup program that supports compression and authenticated encryption. 
- [Rclone](https://rclone.org/) - A command line tool for synchronizing files and directories to and from various cloud storage providers.

## Installation
### Borg Backup
#### Debian/Ubuntu
```bash
sudo apt-get update
sudo apt-get install borgbackup

#### Fedora/CentOS

#### Arch Linux

### Rclone
#### Debian/Ubuntu

#### Fedora/CentOS

#### Arch Linux

## Backup Process
The backup process follows these steps:
1- Create a new archive using Borg Backup, with the borg create command.
2- Use rclone to transfer the archive to a remote storage location, with the rclone copy command.
3- Prune old backups, to keep a specified number of backups and to save space, with the borg prune command.
    
## Restoration

## Conclusion
