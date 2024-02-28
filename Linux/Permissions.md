### [Source of this study material : The Linux Command Line Bootcamp by Colt Steele](https://www.udemy.com/course/the-linux-command-line-bootcamp)


## Play with Permissions in Cloud Shell 

- If I open the Cloud Shell, I'm logged in as yejinshin. I can verify it by running **pwd** or **whoiam**. But if I **cd ..** and go to the home directory, I can make a new user folder named gatsbyflight.


![make-new-user-folder](/GCP_pictures/Linux/Permissions/make-user-folder.PNG "Make a new user folder")


- But as yejinshin, I don't have a permission to write a new file. I tried to make a new file, but it didn't save because I don't have the permission.


- And if we **ls -l** to list items, it shows in the first column 10 digit **file attributes**.


![ls-l](/GCP_pictures/Linux/Permissions/ls-l.PNG "ls -l")


- These characters tell us the type of the file, the **read, write and execute permissions** for the file's owner, the file's group owner, and everyone else.


- The **first digit** tells us the **file type**.


- For example, **-rw-r--r--** tells us that it is a regular file.


**-** : regular file

**d** : directory

**c** : character special file

**l** : symbolic link


- And the other 9 characters tell us about the permissions. 


| Owner | Group | World |
| ------ | ----------- | ----------- |
| rw-   | rw- | r-- |


- So owner and group owner here have **rw-** permissions while the other people who are not the owner and part of the group have **r--** permissions.


- **r** : read permission

- **w** : write permission

- **-** or **x** : execute permission. If **x**, the person has execute permission. If **-**, the person has no execute permission.


- If a file is executable, it means it can be run as a program. If a directory is executable, it means the person can **Cd into** the directory.


- For example, when we run **date** in the shell, it shows the date and time. It is actually an **executable file** that is located in **/bin**. 


![bin-date-file](/GCP_pictures/Linux/Permissions/bin-date-file.PNG "bin date file")


- When you go to **/bin**, there's a ton of executable files.


![bin-folder](/GCP_pictures/Linux/Permissions/bin-folder.PNG "bin folder")


- To see the specific **date** file here, you can use the command:


```
ls -l | grep date -w
```


- List the files with the permissions. Also search the matching file that contains **date**. And specify that the **date** is a word.


![date-permission](/GCP_pictures/Linux/Permissions/date-permission.PNG "date permission")



### chmod Command Basics

- To change the **permission of a file or a directory**, we can use the **chmod** command.


- First, we need to specify the "who" using the following values:

**u** : user (the owner of the file)

**g** : group (members of the group the file belongs to)

**o** : others (the "world")

**a** : all of the above


- Then we tell chmod "what" we are doing using the following characters:

**-** : remove the permission

**+** : grant the permission

**=** : set a permission and remove others


- Finally, the "which" values are:

**r** : read permission

**w** : write permission

**x** : execute permission


- So **chmod u+x file.txt** means that the user(owner) is granted an execute permission with the file.txt.


- **chmod a=r file.txt** means that for all groupings (user, group, world), **read is the only permission for everyone** and all other permissions are removed. So it will become -r--r--r--.


- In the cloud shell, if I change the mode of a file by  **chmod a=r curl-pod.yaml**, it is possible for everyone to read the file but no one can write or edit the file.


![chomod-a-r](/GCP_pictures/Linux/Permissions/chomod-a-r.PNG "chmod a=r curl-pod.yaml")


![cannot-change](/GCP_pictures/Linux/Permissions/read-only-file.PNG "Read only file")


- The write permission is denied even for the owner.


![write-permission-denied](/GCP_pictures/Linux/Permissions/write-permission-denied.PNG "Write permission denied")


- But if I **chmod u+wx curl-pod.yaml**, it will give me (the owner) the permission to write and execute the file.


![chmod-plus](/GCP_pictures/Linux/Permissions/chmod-plus.PNG "chmod u+wx curl-pod.yaml")


- Now, if I try to write some text into the file, it is now granted and written to the file.


![permission-granted](/GCP_pictures/Linux/Permissions/permission-granted.PNG "Permission granted")


- There's also a octal notation to use binary numbers instead of characters we saw above. If you see **1** as "on (permission granted)" and **0** as "off (permission denied)" it comes much easier. 


| Octal | Binary | File Mide |
| ------:| -----------:| -----------:|
| 0   | 000 | --- |
| 1   | 001 | --x |
| 2 | 010  | -w- |
| 3    | 011 | -wx |
| 4    | 100 | r-- |
| 5    | 101 | r-x |
| 6    | 110 | rw- |
| 7    | 111 | rwx |


- If we **chmod 755 file.txt**, the file.txt permission is **-rwx r-x r-x**.


- If I **chmod 644 curl-pod.yaml**, only the owner has **read/write** and the others have **read** only permission.


![chmod-644](/GCP_pictures/Linux/Permissions/chmod-644.PNG "chmod 644")


