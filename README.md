gitlab-config-backup
====================

Script to backup your [GitLab](https://about.gitlab.com/) [Omnibus](https://about.gitlab.com/downloads/) configuration files to a local directory and to Amazon S3 (if installed).

##Setup##
1. Clone this repository
2. *(optional)* Install [s3cmd](https://github.com/s3tools/s3cmd/blob/master/INSTALL) and configure: ```s3cmd --configure```
3. Go to the cloned repository: ```cd gitlab-config-backup```
4. Link the script to a folder in your path, e.g. ```sudo ln -s $(pwd)/gitlab-config-backup /usr/local/sbin```
3. Run the script with sudo ```sudo gitlab-config-backup```
3. The script will by default attempt to upload to S3 bucket ```gitlab-config-backup``` to use a different bucket or path, run with the BUCKET/PATH as the argument, ```sudo gitlab-config-backup my-bucket/subfolder``` 

##Defaults##

```
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

  --s3cmd-config <file>
      s3cmd configuration file.

  --s3cmd-bin <file>
      s3cmd binary.

  --
      Do not interpret any more arguments as options.
```