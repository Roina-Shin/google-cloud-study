## A simple way to schedule a back up for folders using a cron job

1. To do this, you first need to know what 'tar' is.

Tar command is to do an archiving job (e.g. create a tar zip file).
Tar folder is a compressed zip folder of multiple files.

To understand this, run the following command:

mkdir TarMe

touch TarMe/File{1..500}.txt 
-> This will create 500 files (numbered 1 to 500) inside of the TarMe folder.

tar -cvzf [filename].tar.gz TarMe/ 
-> c: create a new archive, v: verbose mode, z: compression algo called gzip
-> Use TarMe folder to create the new archiving folder. (Compress all the files of TarMe into the new folder)

tar -xvzf [filename].tar.gz
-> This upzips the archiving folder.


2. Now you know what tar is, but also beware of date command.

When you type date into your Linux shell, you get the present day, time, year, etc.

But to use only the yyyy-mm-dd format for your backup files, you need to extract the info from the command.

This command will do:

date +%Y-%m-%d (capital Y gives you the full year[yyyy] while small y means the shortened version[yy].)


3. Go to your home directory and make a new directory called backups.

cd backups

vim my-backups


4. This time, you will create a new script that automates the backup job for you.

Vim into my-backups and write these:

#!/usr/bin/bash

DATE=$(date +%Y-%m-%d)
BACKUP_DIR="/home/[your user name]/backups"

tar -cvzf BACKUP_DIR/backup_$DATE.tar.gz /home/[your user name]/[the folder you want to back up]

-> To give you a little explanation,
We will create a DATE variable and BACKUP_DIR to use in your script command.

Make a zip folder named backup_yyyy-mm-dd.tar.gz inside the backups folder as you defined as BACKUP_DIR,
and use the folder defined in the last argument of the command to create a zip folder.

This will create a backup folder for the existing folder that you would like to back up.


5. The last step is to make this command executable by users.

Run the following command:

chmod +x my-backup


6. cd into your backups folder and nothing will be there.

But when you run 'my-backup', you will have the zip file created in your backups folder.


7. To make this tedious job to a cron job, you need to edit your crontab file.

Run the following command:

crontab -e

Then set up a cron job by writing this at the end of the document:

0 0 * * * /home/[your user name]/backups/my-backup

-> The above 5 0 and * characters stand for in order:
minute on the clock / hour on the clock / day of the month / the month / day of the week

So it means that every day at midnight (00:00) run the following script nested in my-backup file.

This concludes our test backup cron job which can be very practical in real world.

Congratulations!





