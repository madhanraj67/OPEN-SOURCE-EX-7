# OPEN-SOURCE-EX-7

#### NAME : MADHANRAJ P
#### REGNO: 212223220052

## AIM:
To create a physical volume, volume group, and logical volume in RHEL, format it with EXT3, mount it to a directory, and make the mount persistent using /etc/fstab.

## PROCEDURE:
STEP 1:
Create a Physical Volume

sudo pvcreate /dev/sdb
STEP 2:
Create a Volume Group with PE size 8MB

sudo vgcreate -s 8M vg_backup /dev/sdb
STEP 3:
Check the PE size

vgdisplay vg_backup | grep "PE Size"
STEP 4:
Expected output
PE Size               8.00 MiB
STEP 5:
Create Logical Volume with 50 extents

sudo lvcreate -l 50 -n lv_app_logs vg_backup
STEP 6:
Format the Logical Volume with ext3

sudo mkfs.ext3 /dev/vg_backup/lv_app_logs
STEP 7:
Create mount point and mount the LV

sudo mkdir /production
sudo mount /dev/vg_backup/lv_app_logs /production
STEP 8:
Verify the mounted filesystem

df -h /production
STEP 9:
Make the mount persistent

echo "/dev/vg_backup/lv_app_logs /production ext3 defaults 0 0" | sudo tee -a /etc/fstab
## OUTPUT:

<img width="424" height="145" alt="image" src="https://github.com/user-attachments/assets/43919f2b-e192-46e2-9397-4b2dfbb73efd" />

## RESULT:
The physical volume, volume group, logical volume, and persistent mount were successfully created and verified in the Red Hat Linux environment.
