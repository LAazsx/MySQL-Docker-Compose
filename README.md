# MySQL Container Installation for Ubuntu VM

1. Create a new VHDX via the Hyper-V Management Console to hold persistent data.

2. Attach the new VHDX to the VM.

3. In Ubuntu,

[Pre-work] Delete any existing paritions (if applicable)

[a] verify drive is detected using ```lsblk```. Drive should show up as "sdb".



[b] format the drive with ```gdisk```

``` sudo gdisk /dev/sdb ```

  
  For the first command, enter  ```n``` followed by ```1```.

  Accept all further prompts until you reach ```Command (? for help)``` .

  Next, enter ```w``` to write all the changes to the drive. ```Y``` to confirmation.

  Format the newly creating partition with ```sudo mkfs.ext4 /dev/sdb1```. Hit enter when promoted with "Writing superblocks and filesystem accounting information".

    
[c] mount the drive

Create a mount point. This will be path where the new drive can be accessed.

``` sudo mkdir /mnt/docker_data ```

Next, get the UUID of the  partition with 
  ``` sudo blkid ```. 

  Look for /dev/sdb1: UUID="<UUID>". Take note of the entire string (32 characters plus hypens).

To register the drive and the mount point, modify ```fstab```  via

```sudo nano /etc/fstab ```

On the last line, enter
``` /dev/disk/by-uuid/<uuid> /mnt/docker_data ext4 defaults 0 0```

Press ``` CTRL+X ``` then ```Y``` then ```ENTER``` to save and exit

Finally, enter ``` sudo mount -a ``` to mount the drive. 

If no error was thrown, type ``` cd /mnt/docker_data ``` to access the directory.

Return to the root directory by typing ``` cd .. ``` twice.

4. Clone the repository

  ``` sudo git clone https://github.com/LAazsx/MySQL_Container/ ```

  ``` cd ``` into the directory with ``` cd MySQL_Container ```

5. Change the root password with 

``` sudo nano docker-compose.yml ```
 
 and change the <password> in ``` MYSQL_ROOT_PASSWORD=<PASSWORD> ```
 

Press ``` CTRL+X ``` then ```Y``` then ```ENTER``` to save and exit

6. Create the container (finally!)

``` sudo docker compose up ```








       
