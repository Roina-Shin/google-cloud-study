### [Source of this study material : GCP Professional Cloud Architect by Ranga Karanam](https://www.udemy.com/course/google-cloud-professional-cloud-architect-certification/)


## Block Storage and File Storage

- What is the type of storage of your hard disk?

  - Block storage


- You've created a file share to share a set of files with your colleagues in an enterprise. What type of storage are you using?

  - File storage


### Block Storage

- Use case: hard disks attached to your computers.


- Typically, one block storage device can be connected to one virtual server.


- However, you can connect multiple different block storages to one virtual server.


- Used as:

  - **Direct attached storage (DAS)** : Similar to a hard disk

  - **Storage Area Network (SAN)** : High-speed network connecting a pool of storage devices

    - Used by databases: Oracle or Microsoft SQL servers



### File Storage

- Media workflows need huge shared storage for supporting processes like video editing.


- Enterprise users need a quick way to share files in a secure and organized way.


- These file shares are shared by several virtual servers.



## GCP Block Storage and File Storage

### Block Storage

- **Persistent Disks**: Network Block Storage

  - Zonal: Data replicated in one zone

  - Regional: Data replicated in multiple zones


- **Local SSDs**: Local Block Storage

  - The local SSD is present on the same host as your virtual machine.


### File Storage

- **Filestore**: High performance file storage



## Local SSDs and Persistent Disks

- **Local SSD** is physically attached to the host of the VM instance.

  - It can hold temporary data.

  - Lifecycle tied to VM instance.

  - Provides high IOPS and very low latency.

  - **Ephemeral storage**. Data persists only until instance is running.

  - You need to **enable live migration** to survive maintenance events.

  - Only a few machine types support local SSDs.


![local-ssd](/GCP_pictures/Study-logs/block-and-file-storge/local-ssd.PNG "Local SSD")


- **Persistent Disk** is network storage.

  - More durable.

  - Lifecyle **not tied** to VM instance.

  - Very flexible:

    - Increase the size when you need it - when attached to a VM instance.

  
  - Zonal persistent disk is in a single zone. Regional persistent disk is replicated in 2 zones in the same region.

  - Typically, regional persistent disks are 2x the cost of zonal persistent disks.



## Persistent Disk - Standard vs Balanced vs SSD


| Features | Standard | Balanced | Local SSD |
| ------ | ----------- | ----------- | ----------- |
| Underlying storage   | Hard Disk Drive | Solid State Drive | Solid State Drive |
| Referred to as | pd-standard | pd-balanced | pd-ssd |
| Performance - Sequential IOPS (Big data/Batch)    | Good | Good | Very good |
| Performance - Random IOPS (Transactional Apps)    | Bad | Good | Very good |
| Use case    | Big data (cost efficient) | Balance between cost and performance | High performance |



## Persistent Disk - Snapshots

- Take **point-in-time snapshots** of your persistent disks.


- You can also schedule snapshots:

  - You can also auto-delete your snapshots after x days.


- Snapshots can be multi-regional and regional.


- You can share snapshots across projects.


- You can create new disks and instances from snapshots.


- Snapshots are **incremental**.

  - The first snapshot contains all the data present in the persistent disk.

  - However, the second snapshot only contains the changes made in the first snapshot.


- It's a good practice to separate persistent disks based on their purposes:

  - Use boot disk only for your operating system.

  - Attach a new persistent disk for other purposes (e.g. volatile data or permanent data)


- (RECOMMENDED) If you are repeatedly creating **disks from a snapshot**:

  - Create an **image from a snapshot** and use the **image to create disks**.


- Snapshots are incremental but you don't lose data by deleting older snapshots.


- Deleting a snapshot **only deletes data which is NOT needed** by other snapshots.


- (RECOMMENDED) Don't hesitate to delete unnecessary snapshots. Because snapshots consume storage.



## Playing with Persistent Disks

- When you are creating a VM, you can opt for **keep boot disk** in Boot Disk section. The default option is to delete boot disk when deleting a VM.


![boot-disk-configuration](/GCP_pictures/Study-logs/block-and-file-storge/boot-disk-configuration.PNG "Boot disk configuration")


- Go back to Disks section and you can create a snapshot by clicking three dots.


![create-snapshot](/GCP_pictures/Study-logs/block-and-file-storge/create-snapshot.PNG "Create a snapshot")


- When creating a snapshot, you can choose to go **multi-regional**. In multi-regional option, 3 options (us, asia, eu) are available.


![multi-regional-snapshot](/GCP_pictures/Study-logs/block-and-file-storge/multi-regional-disk.PNG "Multi regional snapshot")


- If you regularly take a snapshot, then you can utilize a snapshot schedule. You can set snapshot frequency, start time, and autodelete features.


![snapshot-schedule](/GCP_pictures/Study-logs/block-and-file-storge/snapshot-schedule.PNG "Snapshot schedule")


- And you can attach the **snapshot schedule** to an existing persistent disk.


- Go to the Disks and click Edit Disks. And attach the snapshot schedule.


![attach-snashot-schedule-to-disk](/GCP_pictures/Study-logs/block-and-file-storge/attach-snapshot-schedule-to-disk.PNG "Attach snapshot schedule to persistent disk")


- You can also attach a newly created persistent disk to an already running VM:


```
gcloud compute instances attach-disk INSTANCE_NAME --disk DISK_NAME
```


- After that, you should format the disk. Format it to the file format of your choice (e.g. ext4 file system):


```
sudo lsblk

sud mkfs.ext4 -m 0 -E lazy_itable_init=0, lazy_journal_init=0, discard /dev/sdb
```


- **Linux Standard File System**


| File System | Description |
| ------:| -----------:|
| ext4   | Most popular standard file system for Linux. |
| btrfs | Relatively new and supports copy-on-write. |
| ext    | Standard file system and default for Red Hat 7. Supports metadata journaling so quicker crash recovery |


- And then, you can mount the disk. Create a directory to mount to and mount the disk there.


```
sudo mkdir -p /mnt/disks/MY_DIR

sudo mount -o discard,defaults /dev/sdb /mnt/disks/MY_DIR
```


- Once you mount the disk, you can provide permissions to that.


```
chmod a+w /mnt/disks/MY_DIR
```


