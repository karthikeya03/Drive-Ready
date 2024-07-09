
# Creating and Attaching an EBS Volume in AWS EC2

## Step 1: Create a Volume
1. **Navigate to EC2 Dashboard**:
   - Go to the AWS Management Console.
   - Open the EC2 Dashboard from the Services menu.

2. **Open Volumes**:
   - In the left-hand menu, under "Elastic Block Store", click on "Volumes".

3. **Create a New Volume**:
   - Click the "Create volume" button at the top right.

![Screenshot (389)](https://github.com/karthikeya03/Drive-Ready/assets/120096427/b2ccbc82-8430-4249-aa28-956ef41ee217)

   
   - **Volume type**: Select "General Purpose SSD (gp3)".
   - **Size (GiB)**: Set the size to 5 GiB.
   - **IOPS**: Set to 3000.
   - **Throughput (MiB/s)**: Set to 125.
   - **Availability Zone**: Select `us-east-1a` or your desired availability zone.
   - Leave other fields as default or adjust as needed.
   - Click "Create volume".

## Step 2: View the Created Volume
1. **Check Volume List**:
   - After creating the volume, you will see it listed under "Volumes".

![Screenshot (390)](https://github.com/karthikeya03/Drive-Ready/assets/120096427/ac8358e6-dfc2-49a4-8868-483c1e3efb81)

   - Ensure the volume state is "available".
   - Note the volume ID for reference.

## Step 3: Attach the Volume to an Instance
1. **Select the Volume**:
   - Select the volume you just created from the list.

2. **Attach Volume**:
   - Click on the "Actions" dropdown and select "Attach volume".

![Screenshot (391)](https://github.com/karthikeya03/Drive-Ready/assets/120096427/29135e54-c67e-437d-83cb-9ee6353de42b)

   
   - **Instance**: Select the instance you want to attach the volume to.
   - **Device name**: Use the default or specify a device name such as `/dev/xvdb`.
   - Click "Attach volume".

## Step 4: Verify the Volume in Disk Management
1. **Connect to the Instance via MobaXterm**:
   - Use MobaXterm as your RDP client to connect to the instance.

2. **Open Disk Management**:
   - Once connected, press `Windows + R` to open the Run dialog.
   - Type `diskmgmt.msc` and press Enter to open Disk Management.

     ![Screenshot (395)](https://github.com/karthikeya03/Drive-Ready/assets/120096427/a42621aa-32da-43a2-8eef-6b4d853e46ef)


3. **Check the Disk**:
   - In Disk Management, you should see the new volume listed.
   - Initialize and format the volume if necessary to start using it.
   - click on the offline button and turn it to online



