### [Source of this study material : GCP Associate Cloud Engineer by Ranga Karanam](https://www.udemy.com/course/google-cloud-certification-associate-cloud-engineer/)

## Implementing Compute Engine Instance

- When creating a VM, you can add labels to differentiate with other resources.


![vm-labels](/GCP_pictures/Study-logs/compute-instance/vm-labels.PNG "VM labels")


- After creating the VM, run the command to see the disks available:


```
lsblk
```


![lsblk](/GCP_pictures/Study-logs/compute-instance/lsblk.PNG "lsblk")


- Now, we are going to create an independent disk to attach to a VM.


- Go to Disks in Compute Engine menu bar and click Create Disks.


- When creating a disk, make sure that the disk region/zone is the same as the VM's region/zone. Otherwise, you won't be able to attach it to the VM.


![create-a-disk](/GCP_pictures/Study-logs/compute-instance/create-a-disk.PNG "Create a disk")


- Go to your VM instance and edit it. And attach your newly created disk as the existing disk.


![extra-disk](/GCP_pictures/Study-logs/compute-instance/extra-disk-attach.PNG "Extra disk")


- If we run the command again, we will see that the additional disk is now attached:


![additional-disk-attached](/GCP_pictures/Study-logs/compute-instance/additional-disk-attached.PNG "Additional disk attached")


- Now, we will see how to generate a custom SSH key for a VM and SSH into it by using the key.


- First, to generate a custom SSH key, you need to download PuTTY.


- After downloading it, first go to PuTTYGen. Actually this PuTTYGen is automatically installed in the moment you installed Google Cloud SDK. So you don't need to install this particular app.


- Click generate.


![putty-generate](/GCP_pictures/Study-logs/compute-instance/putty-generate.PNG "PuTTY Generate key")


- Now the blocked text is the public key.


![public-key-generated](/GCP_pictures/Study-logs/compute-instance/public-key-generated.PNG "Public key generated")


- Provide some comment here:


![yejin-from-ssh](/GCP_pictures/Study-logs/compute-instance/yejin-from-ssh.PNG "yejin from ssh")


- Then copy the public key and go to Google Cloud console.


- Click edit instance and then add SSH key and save.


![add-ssh-key](/GCP_pictures/Study-logs/compute-instance/add-ssh-key.PNG "Add SSH key")


- Now go back to your PuTTYGen window and click Save Private Key.


![save-private-key](/GCP_pictures/Study-logs/compute-instance/save-private-key.PNG "Save private key")


![key-saving](/GCP_pictures/Study-logs/compute-instance/key-saving.PNG "Key saving")


- This time, open your PuTTY and grab your VM's external IP.


- Here, provide your external IP to the PuTTY.


![external-ip](/GCP_pictures/Study-logs/compute-instance/external-ip.PNG "External IP provided")


- Also, save the session as below:


![save-session](/GCP_pictures/Study-logs/compute-instance/save-session.PNG "Save session")


- Earlier, I had error with this. And one of the reasons was this user name:


- Provide the **exact login name** you provided in Google Console:


![login-name](/GCP_pictures/Study-logs/compute-instance/login-name.PNG "Login name")


- When you run command like **lsblk**, it shows the VM's disk info accordingly.


![putty-lsblk](/GCP_pictures/Study-logs/compute-instance/putty-lsblk.PNG "Putty lsblk")











