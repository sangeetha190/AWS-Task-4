# AWS-Task-4
- 1️⃣ Launch EC2 Instances (Linux & Windows)
- 2️⃣ Set Up a Web Server on Both Instances
- 3️⃣ Create and Attach a 5GB EBS Volume Windows and Linux Instance
- 4️⃣ Format & Mount the Volume on Linux & Windows
- 5️⃣ Take a Snapshot of the EBS Volume
- 6️⃣ Create a New EBS Volume from the Snapshot & Attach It

- 🛠 Step 1: Launch EC2 Instances (Linux & Windows)
- 📍 Where? AWS Console → EC2 → Launch Instance

- 🔹 For Linux Instance:
   - Go to AWS Console → EC2 → Launch Instance
   - Choose Amazon Linux 2 (Free Tier Eligible)
   - Select t2.micro instance type
   - Key Pair: Select or create a new key pair
   - Security Group:
   - Allow SSH (Port 22)
   - Allow HTTP (Port 80)
   - Click Launch ✅
- 🔹 For Windows Instance:
  - Follow the same steps but choose Windows Server 2019
  - Allow RDP (Port 3389) instead of SSH
  - Click Launch ✅
  - ✅ Now, you have two running instances!
****
![image](https://github.com/user-attachments/assets/6213c435-e0b1-4afd-bdb9-d2a63716c97a)
![image](https://github.com/user-attachments/assets/c3324453-5990-492d-a615-d13b9ecd1a8c)
![image](https://github.com/user-attachments/assets/dc4a9e50-ffe3-4d28-8c0f-91f91b289c39)

- 🛠 Step 2: Set Up Web Server on Both Instances
 🔹 For Windows:
   - Open Server Manager → Add Roles and Features
   - Install IIS Web Server
   - Edit the file at C:\inetpub\wwwroot\index.html:
   - <p>Welcome to My Windows Web Server</p>
   - Verify by opening the public IP in a browser ✅

VM connect with index.html output
![image](https://github.com/user-attachments/assets/d0c7b289-1b11-4633-99b0-c9cdad5efd9b)


![image](https://github.com/user-attachments/assets/0db2b50a-dcd5-481c-aa4d-b63f9b4cd9b7)
![image](https://github.com/user-attachments/assets/a1c18f1a-6a88-4926-85bd-f7e0f7c4a423)
 🔹 For Linux:
   - Open Putty using the username and password key
   - Install Apache (httpd)
       - sudo yum update -y
       - sudo yum install -y httpd
       - sudo systemctl start httpd
       - sudo systemctl enable httpd
   - Create a test webpage:
       - echo
       - <p>Welcome to My Linux Web Server</p>
       - | sudo tee /var/www/html/index.html
   - Verify by opening the public IP in a browser ✅
![image](https://github.com/user-attachments/assets/1eb5e079-6fd0-48a3-aa95-4b0b18c8886f)
🛠 Step 3: Create & Attach a 5GB EBS Volume
- 📍 Where? AWS Console → EC2 → Volumes → Create Volume
 - Click Create Volume
   - Size: 5GB
   - Type: gp3 (General Purpose SSD)
   - <b>Availability Zone: Same as EC2 instance</b>
 - Click Create
  ![image](https://github.com/user-attachments/assets/36657366-bff0-4111-bed0-7db9f2b5a74b)
 - Select the created volume → Click Actions → Attach Volume
 - ![image](https://github.com/user-attachments/assets/334e188a-7b81-4b1e-908e-6789b994ffa7)
 - Select your Linux or Windows EC2 instance
 - Click Attach ✅
   - ✅ The volume is now attached but needs to be formatted and mounted.
   ![image](https://github.com/user-attachments/assets/78c6081d-b908-4bcd-bcbd-16c79891c978)

![image](https://github.com/user-attachments/assets/e8d3d9bf-db78-498a-9840-d87e5cc8cbad)

- 🛠 Follow these steps:
- Open Command Prompt as Administrator

   - Click on the Start menu 🔎
   - Search for cmd
   - Right-click on Command Prompt and select Run as administrator.
   - Open DiskPart
   - Type the following command and press Enter:
   - <b>diskpart</b>  ![diskpart](https://img.shields.io/badge/diskpart-red)
   - List Available Disks
      - <b>list disk</b>
      - ![list disk](https://img.shields.io/badge/list%20disk-red)
      - This will show a list of all available disks.
      - Identify the disk number of the 5GB volume (e.g., Disk 1).
   - Select the Disk
      - <b>select disk 1</b> ![select disk 1](https://img.shields.io/badge/select%20disk%201-red)
      - This selects the Disk 1 (5GB EBS Volume).
   - Bring the disk online by typing:
      - <b>online disk</b> ![online disk](https://img.shields.io/badge/online%20disk-red)
      - This will attempt to bring the disk online.
   - If it still doesn’t work, clear any read-only attributes:
      - <b>attributes disk clear readonly</b> ![attributes disk clear readonly](https://img.shields.io/badge/attributes%20disk%20clear%20readonly-red)
   - Now check if the disk is online by typing: <b>list disk</b>
      - If Disk 1 now shows as Online, proceed to the next steps.
   - Now, initialize the disk (if required) by typing: <b>convert gpt</b> ![online disk](https://img.shields.io/badge/convert%20gpt-red)
   - Go back to Disk Management and try creating a New Simple Volume.
   - ✅ Expected Outcome:
      - Disk 1 should now be Online.
      - You should be able to right-click on the Unallocated 5GB and select "New Simple Volume" to format it.
   ![image](https://github.com/user-attachments/assets/6f17adb5-cf8a-4d75-8183-7b4b3b1d45e2)
   ![image](https://github.com/user-attachments/assets/68e2f12f-0c67-43fd-bc3a-3a5bb583f2b5)
   ![image](https://github.com/user-attachments/assets/05fb8159-5b20-46b9-9393-dfa381b023be)
   ![image](https://github.com/user-attachments/assets/e1cd7c6f-fe93-4905-b8f3-4a8a3132a630)
   ![image](https://github.com/user-attachments/assets/8c33422a-3cbc-4dde-9972-0d4b3ab6397c)
   
   ![image](https://github.com/user-attachments/assets/f15a373a-e2ed-43be-bee4-cf1083a00306)
   ![image](https://github.com/user-attachments/assets/bb876aa6-c277-4a52-8b98-de6bebd4fd26)

### Create a New EBS Volume for Linux
- Go to AWS Console → Open EC2 Dashboard
- In the left menu, click "Volumes" under Elastic Block Store (EBS).
- Click "Create Volume"
- Set the following values:
   - Volume Type → General Purpose SSD (gp3)
   - Size → 5 GiB
   - Availability Zone → Must match the Linux instance AZ
   - Example: If your Linux instance is in ap-south-1a, the volume should also be in ap-south-1a.
- Click "Create Volume" ✅
🎉 Now you have created the Linux EBS volume!
![image](https://github.com/user-attachments/assets/092cfd2d-2d23-4492-8d93-c5dc49a94417)
![image](https://github.com/user-attachments/assets/1523c947-b0ac-4b5f-8760-951f18c04df0)
### 🛠 Attach the EBS Volume to Linux Instance
- 🔹 For Linux:
  - 📍 Where? Connect via SSH
   - Check the attached volume:
   - <b>lsblk</b>
   - You will see something like /dev/xvdf
 - Format the volume
   - <b>sudo mkfs -t ext4 /dev/xvdf</b>
 - Create a mount point & mount it:
   - <b>sudo mkdir /mydata
   - sudo mount /dev/xvdf /mydata</b>
 - Make it permanent (optional):
   - <b>echo "/dev/xvdf /mydata ext4 defaults,nofail 0 2" | sudo tee -a /etc/fstab</b>
![image](https://github.com/user-attachments/assets/69b517f4-424c-422a-b034-0b99a3493e99)
- Next Steps: Format & Mount the EBS Volume
   - 1️⃣ Check if the Volume is Recognized
     - You already did this with: <b>lsblk</b>
   - 2️⃣ Format the Volume (EXT4)
     - Run this command to format the disk:
  - <b>sudo mkfs -t ext4 /dev/xvdf</b>
    - ⚠ Warning: This will erase any data on the disk.
  - 3️⃣ Create a Directory for Mounting
    - We need a directory where we can attach (mount) this volume:
    - <b>sudo mkdir /mnt/data</b>
  - 4️⃣ Mount the Volume
    - Now, attach the volume to the /mnt/data directory:
    - <b>sudo mount /dev/xvdf /mnt/data</b>
  - 5️⃣ Verify the Mount
    - Run this command: <b>df -h</b>
    - ✅ You should see /mnt/data listed with 5GB available.
![image](https://github.com/user-attachments/assets/22cd959e-3bb9-42de-b794-4aa2e84fcb1b)

- 🛠 Step 5: Take a Snapshot of EBS Volume
### How to Take a Snapshot in AWS
- Go to the AWS EC2 Console
   -🔗 EC2 Dashboard → Elastic Block Store → Volumes
- Select the EBS Volume You Want to Snapshot
  - Find the volume attached to your EC2 instance (Linux or Windows).
  - Right-click → Create Snapshot.
   ![image](https://github.com/user-attachments/assets/385af653-df4e-4de5-a7b1-b671c00fc17c)
- Configure Snapshot Details
  - Name & Description → Give a meaningful name like:
    - "Windows-Data-Snapshot"
    - "Linux-Data-Snapshot"
- Leave other settings default.
- Click Create Snapshot
   - It will take some time depending on the volume size.
   - Check progress in Snapshots tab under Elastic Block Store.
![image](https://github.com/user-attachments/assets/cba5d73e-ece3-4456-bc99-4f4c04852152)
### Linux
![image](https://github.com/user-attachments/assets/cde90301-0f79-430d-9ae8-33f7a5719a6b)
![image](https://github.com/user-attachments/assets/d01507d5-c11c-46d6-9863-0832c1f30861)


- 🛠 Step 6: Create a New EBS Volume from the Snapshot
 - 📍 Where? AWS Console → EC2 → Snapshots
 - Once the snapshot is ready, we will create a new EBS volume using this snapshot.
 ![image](https://github.com/user-attachments/assets/8b467122-25b9-46b4-b089-ed39103d867e) 
 - Go to Snapshots and select the one you created
 - Click Actions → Create <b>Volume from Snapshot</b>
![image](https://github.com/user-attachments/assets/39fc9329-9619-4d2e-833b-48cb94fa2683)
   - A new window will open.
 - Configure the Volume Settings
   - Volume Type: gp3 (General Purpose SSD)
   - Size: Keep 5GB (default from the snapshot)
   - Availability Zone: Same as your EC2 instance (Windows/Linux)
     - If your instance is in ap-south-1b, select the same
![image](https://github.com/user-attachments/assets/7f49de5c-f846-46ba-bcaa-6d677e4afc70)
 - Click Create Volume ✅
    - This will create a new EBS volume from the snapshot.
 - Attach New Volume to EC2
   - Go to EBS → Volumes
   - Select New Volume → Click Attach Volume
   - Choose EC2 Instance
   - Click Attach ✅
- ✅ The new volume is now attached!

![image](https://github.com/user-attachments/assets/5b5f598b-dfea-4f6d-b6cf-684f0f3c6c21)
![image](https://github.com/user-attachments/assets/f1415b80-614a-4b71-a41c-0ce87774d202)
![image](https://github.com/user-attachments/assets/11a243af-1798-4c66-a14a-0bd3e5b513c6)



After Attaching, Verify in Windows
- 1️⃣ Log into your Windows EC2 instance via Remote Desktop (RDP).
- 2️⃣ Open Disk Management:
   - Press Win + R, type diskmgmt.msc, and press Enter.
   - ![image](https://github.com/user-attachments/assets/4bea5ab4-c0f5-4a54-b977-ac8602a4b359)
- 3️⃣ Check if the new volume appears as "Unallocated".
- 4️⃣ If unallocated, right-click on it → Select "New Simple Volume" → Format as NTFS.
- Follow the "Open Command Prompt as Administrator to make Disk to Online" this steps
![image](https://github.com/user-attachments/assets/5798aec7-14d0-409d-bfde-2633add94048)


![image](https://github.com/user-attachments/assets/4fee2731-b29f-48d0-a480-4e1fba594f5a)
Step 7: Take a Snapshot of the New Volume
Since you have two new volumes (D: and S:), decide which one to snapshot.

📌 How to Take a Snapshot in AWS
1️⃣ Go to EC2 Dashboard → Elastic Block Store (EBS) → Volumes.
2️⃣ Select the volume you want to take a snapshot of (e.g., D: or S:).
3️⃣ Click "Actions" → "Create Snapshot".
4️⃣ Enter a name/description (e.g., "Windows-Snapshot").
5️⃣ Click "Create Snapshot" and wait for completion.

![image](https://github.com/user-attachments/assets/ab88f071-5695-4417-8f6a-20edf3e7b19f)


- Before Reboot (Windows Test):
![image](https://github.com/user-attachments/assets/ca589e87-9e24-4bde-9d4a-bdf240fa709c)
- Reboot the Windows VM:
   - This simulates a real-world scenario where an instance might be restarted.
- After Reboot (Windows Test):
  - You checked if the file is still present in Volume D.
  - ✅ Expected Outcome:
 - If the file exists after reboot, then the EBS volume is correctly attached and persistent.
 - If the file disappears after reboot, then the volume was not mounted correctly, or another issue needs troubleshooting.
![image](https://github.com/user-attachments/assets/db75ee7a-9c25-4f0d-a6c2-906bae3e8b05)

==============================================================================
- 🔹 Step 1: Verify If a Snapshot Exists for Volume S
- 1️⃣ Go to AWS Console → EC2 → Elastic Block Store (EBS) → Snapshots
- 2️⃣ Check if a snapshot for Volume S exists

   - If a snapshot exists before file creation, take a new snapshot.
   - If the snapshot was taken after file creation, proceed to the next step.
   - ✅ If no snapshot exists or an old one was taken, create a new snapshot now before rebooting.

- 🔹 Step 2: Take a New Snapshot of Volume S (if needed)
   - If the snapshot was taken before creating "Sangeetha_text_file.txt," take a new one:

- 1️⃣ Go to AWS Console → EC2 → Elastic Block Store (EBS) → Volumes
- 2️⃣ Find Volume S
- 3️⃣ Right-click → Create Snapshot
- 4️⃣ Enter a description (e.g., "Snapshot_after_file_creation")
- 5️⃣ Click Create Snapshot

- ✅ This ensures that the snapshot includes the latest files.


![image](https://github.com/user-attachments/assets/a6aadd8d-1e4a-4ed6-9907-9dca25dc2f53)

![image](https://github.com/user-attachments/assets/be65f80d-2132-4b00-97eb-8ddffa22429c)

![image](https://github.com/user-attachments/assets/d6e333bf-a49b-4bb6-8903-9090aa8e0771)


![image](https://github.com/user-attachments/assets/d903b129-f1ef-4d80-ae86-faeb71ba9062)


snapshot attach to the windows VM
![image](https://github.com/user-attachments/assets/3a6c5ea3-7994-4c2f-893c-edceae36eb82)
![image](https://github.com/user-attachments/assets/7cc18f9c-c8f9-424b-add7-fd1194e1ef97)
![image](https://github.com/user-attachments/assets/888fd85f-cf1d-40f9-899a-3e33399d0485)
![image](https://github.com/user-attachments/assets/51d3a831-8d35-458d-ab67-501689a3de1d)
![image](https://github.com/user-attachments/assets/85707840-3861-431f-b385-ef181e2d2def)




new instance 
![image](https://github.com/user-attachments/assets/7fe7eacd-3cfc-49a6-866b-eda0c2dc1397)

![image](https://github.com/user-attachments/assets/dfb62ac7-0b08-44da-ab76-9c2b31404487)


