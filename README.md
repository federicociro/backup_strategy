# Backup Strategy
This repository contains documentation for the backup strategy used for my Linux systems. It includes information on the tools and processes used for creating and maintaining backups, as well as instructions for restoring from backups in case of a failure or data loss.

[![GitHub Super-Linter](https://github.com/<OWNER>/<REPOSITORY>/workflows/Lint%20Code%20Base/badge.svg)](https://github.com/marketplace/actions/super-linter)

## Tools
- [Borg Backup](https://borgbackup.readthedocs.io/) - A deduplicating backup program that supports compression and authenticated encryption. 
- [Rclone](https://rclone.org/) - A command line tool for synchronizing files and directories to and from various cloud storage providers.

## Installation
### Borg Backup
#### Debian/Ubuntu
```bash
sudo apt-get update
sudo apt-get install borgbackup
```

#### Fedora/CentOS
```bash
sudo dnf install borgbackup
```

#### Arch Linux
```bash
sudo pacman -S borgbackup
```

### Rclone
#### Debian/Ubuntu
```bash
curl https://rclone.org/install.sh | sudo bash
```

#### Fedora/CentOS
```bash
curl https://rclone.org/install.sh | sudo bash
```

#### Arch Linux
```bash
sudo pacman -S rclone
```

## Backup Process
The backup script is built in 3 parts:
1. Create a new archive using Borg Backup, with the `borg create` command.
2. Use rclone to transfer the archive to a remote storage location, with the `rclone copy` command.
3. Prune old backups, to keep a specified number of backups and to save space, with the `borg prune` command.
    
## Restoration
In case of a failure or data loss, backups can be restored using the `borg extract` command. Detailed instructions for restoring specific files or directories can be found in the Borg Backup documentation.
Alternatively, `borg mount` can be used for temporal restoration.

## Setting up Backup with Systemd
In order to run the backup script automatically using systemd, you will need to create two service files: one for the backup service and one for the timer service.

## Backup Service
Create a new file named `borg-backup.service` in the `/etc/systemd/system/` directory with the following contents:
```bash
[Unit]
Description=Create backup using Borg Backup

[Service]
Type=oneshot
User=root
ExecStart=/usr/local/bin/borg-backup.sh
StandardOutput=file:/var/log/borg-backup.log
StandardError=file:/var/log/borg-backup-error.log
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

- Make sure to adjust the paths and user according to your system setup.

Then, enable the service by running:
```bash
sudo systemctl enable borg-backup.service
```

## Timer Service
Create a new file named `borg-backup.timer` in the `/etc/systemd/system/` directory with the following contents:
```bash
[Unit]
Description=Create backup using Borg Backup

[Timer]
OnCalendar=daily
AccuracySec=1h
Persistent=true

[Install]
WantedBy=timers.target
```

- Make sure to adjust the timing of the backup by modifying the `OnCalendar` value to fit your needs.

Then, enable the timer by running:
```bash
sudo systemctl enable borg-backup.timer
```

You can check the status of the timer and the service by running:
```bash
sudo systemctl status borg-backup.timer
sudo systemctl status borg-backup.service
```

## Conclusion
This documentation is intended to serve as a guide for anyone responsible for maintaining and managing backups for our system. It is important to regularly test and verify the backups to ensure that they can be successfully restored in case of a failure or data loss.

## To Do
- [ ] Add more features to the script: dry-run option
- [ ] Improve performance of the code
- [X] Add more comments to the code for better readability
- [X] Write more detailed documentation
- [ ] Add test cases to ensure reliability
- [ ] Add error handling to the `mysqldump` command
