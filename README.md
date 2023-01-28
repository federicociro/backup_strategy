# Backup Strategy
This repository contains documentation for the backup strategy used for my Linux systems. It includes information on the tools and processes used for creating and maintaining backups, as well as instructions for restoring from backups in case of a failure or data loss.

## Tools
- [Borg Backup](https://borgbackup.readthedocs.io/) - A deduplicating backup program that supports compression and authenticated encryption. 
- [Rclone](https://rclone.org/) - A command line tool for synchronizing files and directories to and from various cloud storage providers.

## Installation
### Borg Backup
#### Debian/Ubuntu
```bash
sudo apt-get update
sudo apt-get install borgbackup
```bash

#### Fedora/CentOS
```bash
sudo dnf install borgbackup
```bash

#### Arch Linux
```bash
sudo pacman -S borgbackup
```bash

### Rclone
#### Debian/Ubuntu
```bash
curl https://rclone.org/install.sh | sudo bash
```bash

#### Fedora/CentOS
```bash
curl https://rclone.org/install.sh | sudo bash
```bash

#### Arch Linux#### Arch Linux
```bash
sudo pacman -S rclone
```bash

## Backup Process
The backup script is built in 3 parts:
1- Create a new archive using Borg Backup, with the `borg create` command.
2- Use rclone to transfer the archive to a remote storage location, with the `rclone copy` command.
3- Prune old backups, to keep a specified number of backups and to save space, with the `borg prune` command.
    
## Restoration
In case of a failure or data loss, backups can be restored using the `borg extract` command. Detailed instructions for restoring specific files or directories can be found in the Borg Backup documentation.
Alternatively, `borg mount` can be used for temporal restoration.

## Conclusion
This documentation is intended to serve as a guide for anyone responsible for maintaining and managing backups for our system. It is important to regularly test and verify the backups to ensure that they can be successfully restored in case of a failure or data loss.
