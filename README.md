# AWS-Task-4
- 1️⃣ Launch EC2 Instances (Linux & Windows)
- 2️⃣ Set Up a Web Server on Both Instances
- 3️⃣ Create and Attach a 5GB EBS Volume
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
   - Type the following command and press Enter: <b>diskpart</b>
   - List Available Disks
      - <i>list disk</i>
      - This will show a list of all available disks.
      - Identify the disk number of the 5GB volume (e.g., Disk 1).
   - Select the Disk
      - select disk 1
      - This selects the Disk 1 (5GB EBS Volume).
   - Bring the disk online by typing:
      - <i>online disk</i>
      - This will attempt to bring the disk online.
   - If it still doesn’t work, clear any read-only attributes:
      - attributes disk clear readonly
   - Now check if the disk is online by typing: <b>list disk</b>
      - If Disk 1 now shows as Online, proceed to the next steps.
   - Now, initialize the disk (if required) by typing: <b>convert gpt</b>
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










