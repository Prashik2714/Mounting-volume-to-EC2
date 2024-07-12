Mounting volume to ec2,unmounting it and after mounting this volume to another ec2

Step1 :- create a two instances

![image](https://github.com/Prashik2714/My-first-repo/assets/157954545/68bbaf10-1c47-4976-ba28-46e6f7eb19f2)

Step2 : ssh 1st instance into gitbash
       
       • Now use lsblk command to see list of block devices (i.e., volume attach to our instance)
       • We will see 8 gb storage only with which we launch our instance ( as we not attach any additional volume to our instance yet)

![image](https://github.com/Prashik2714/My-first-repo/assets/157954545/0a996798-1b7e-48f4-9ee3-0f5906b53861)

Step 3:- creating additional volume
     
     • Click on volumes in elastic block store option
     • In volume dashboard click on create volume
     • Fill in all details about volume which requires
         We choose gp3 type volume and storage 10 gb
     • Next select this volume and attach to our instance from action tab

![image](https://github.com/Prashik2714/My-first-repo/assets/157954545/ae346fb1-68d7-491f-8bf5-8c90865f819d)

![image](https://github.com/Prashik2714/My-first-repo/assets/157954545/2edbb2ce-5db6-44a0-93d3-dbef127ecf0b)

    •	Now if use lsblk command we can see it attach to our instance
    •	But if use df -h command (which show total space, use and available space of disk mounted on instance) , we don’t see any information about our new attach volume
    •	To use this new attach volume we have to mount it first to our instance

Step 4 :- Mounting volume to our instance

   • First we have to create filesystem on our new volume
     Use following command to create file system
     mkfs -t xfs /dev/volumename
     note:- in place of ‘volumename’ correctly put a name of volume
   • To verify if filesystem is created successfully we can use following command
     Lsblk -f (which will show filesystem type of all volumes attach to our ec2)

![image](https://github.com/Prashik2714/My-first-repo/assets/157954545/75feeb18-3edd-4e2c-9935-68b2615748ac)

   •	Now to mount volume first create directory where volume is to be mounted
      mkdir directoryname
   •	Use following command to mount volume to our instance
      mount dev/volumename /directory name
      note:- type full directory path in ‘directory name’
   •	Now to confirm if our volume mount successfully or not 
      use df -h command and we will see details of our new volume mounted

![image](https://github.com/Prashik2714/My-first-repo/assets/157954545/52fc5815-7283-45ae-a923-a2b96c1c877e)

Step 5 :- Now add some file in our newly mounted volume

   •	Any file add in directory where our volume is mounted will add into volume
      this directory is our mountpoint(meaning anything add here will add to new volume mounted), we can also verify it by using
      mountpoint directory_name command 
   •	Ues touch filename command to create files
      Note :- we will have to be in the mountpoint directory and create file

![image](https://github.com/Prashik2714/My-first-repo/assets/157954545/a209ba63-40d4-48f4-9001-eb32415224a1)

![image](https://github.com/Prashik2714/My-first-repo/assets/157954545/b5e1a1e4-1254-40f9-95e8-1bd01b931bf6)

Step 6:- Unmounting and detaching volume

   •	Use umount mountpoint_name command to unmount volume
      Note:- type directory name where we mount our volume in place of mountpoint name.
   •	Our volume will unmount successfully. We can verify using df -h command
   •	Now detach this volume from our instance by going in volume tab in aws portal  and clicking on action tab and then clicking on detach volume.

![image](https://github.com/Prashik2714/My-first-repo/assets/157954545/c49b5c22-f287-4159-8f71-2f27eca3272c)

Step 7:- Attaching and mounting volume to 2nd instance

  • Now select volume which we just detach again and attach it to the 2nd instance
  • Now ssh our 2nd instance in gitbash and mount this volume to it
    First, create directory using mkdir directory_name command
  • Using mount dev/volume_name /directory_name
    Note:- enter complete path of directory in ‘directory_name’

![image](https://github.com/Prashik2714/My-first-repo/assets/157954545/284a5c51-0bd5-4a22-8734-510810e0c2ba)

Step 8:- Looking for files created in volume when it was mount on 1st instance

  • Go to directory where we mount our volume in 2nd instance
    Use cd directory_name command
  • Use ‘ ls ’ command to see list of files on mounted volume

![image](https://github.com/Prashik2714/My-first-repo/assets/157954545/041a05e4-847d-4a17-90fa-c31ca7c0a53a)

  • Now unmount volume using umount directory_name command.
    Note:- directory_name is mountpoint (which is directory where we mount volume).
  • Next detach volume from 2nd instance by going into aws portal

   We have successfully mount volume to instance, unmount it and again mount it to other instance. 












