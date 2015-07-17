gitlab-config-backup
====================

Script to backup your [GitLab](https://about.gitlab.com/) [Omnibus](https://about.gitlab.com/downloads/) configuration files to a local directory and to Amazon S3 (if installed).

##Setup##
1. Clone this repository: `git@github.com:iNtergrated/gitlab-config-backup.git`
2. Go to the cloned repository: ```cd gitlab-config-backup```
3. Link the script to a folder in your path, e.g. ```sudo ln -s $(pwd)/gitlab-config-backup /usr/local/sbin```
4. *(optional)* Install [s3cmd](https://github.com/s3tools/s3cmd/blob/master/INSTALL) and configure: ```s3cmd --configure```
5. Run the script with sudo ```sudo gitlab-config-backup```
6. The script will by default attempt to upload to S3 bucket ```gitlab-config-backup``` to use a different bucket or path, run with the BUCKET/PATH as the argument, ```sudo gitlab-config-backup my-bucket/subfolder```

##Defaults##

```
GITLAB_CONFIG_PATH="/etc/gitlab"
GITLAB_BACKUP_PATH="/var/backups/gitlab-config"
S3CMD_BIN_PATH="/usr/local/bin/s3cmd"
S3CMD_CONFIG_PATH="$USER/.s3cmd"
```


##Options##

```
Backup and (optionally) upload your GitLab Omnibus configuration.

Usage: gitlab-config-backup <S3 BUCKET_NAME/FOLDER> [options]...

Options:

  -h, --help
      This help text.

  -V, --version
      Display version.

  -q, --quiet
      Hide all output.

  -c, --color
      Colorize output.

  -p, --plain
      Plain output, no formatting or color.

  -C, --gitlab-config <folder>
      Path to the GitLab Omnibus config folder
      default: /etc/gitlab

  -b, --backup-path <folder>
      Path to folder where you want to store backups.
      default: /var/backups/gitlab-config

  --s3cmd-config <file>
      s3cmd configuration file.

  --s3cmd-bin <file>
      s3cmd binary.

  --no-s3
      Do not upload to AWS S3.

  --
      Do not interpret any more arguments as options.
```

##Exit Codes##

> ```
0   No Errors
-1  Not run as root (use sudo)
```

### 1-10 Parameter/Option Errors###
> ```
 1    Could not find the GitLab config source directory (-C, --gitlab-config)
 2    You must provide a path for: -b, --backup-path (-b, --backup-path)
 3    Could not find the S3 configuration file (--s3cmd-config)
 4    Could not find the S3 binary (--s3cmd-bin)
 5    Invalid option...
```

### 11-20 Errors Running Script###
> ```
11    GitLab config folder could not be found...
12    Local backup of GitLab configuration FAILED
13    s3cmd NOT installed
14    s3cmd configuration could NOT be found
15    Upload to S3 FAILED... S3 path does not exist
16    Upload failed, other S3 error
```