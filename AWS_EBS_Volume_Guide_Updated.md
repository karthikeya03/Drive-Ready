
# Creating and Attaching an EBS Volume in AWS EC2

This guide will walk you through the steps to create an EBS volume in AWS EC2, attach it to an instance, and verify it using Disk Management via MobaXterm.

## Step 1: Create a Volume
1. **Navigate to EC2 Dashboard**:
   - Go to the AWS Management Console.
   - Open the EC2 Dashboard from the Services menu.

2. **Open Volumes**:
   - In the left-hand menu, under "Elastic Block Store", click on "Volumes".

3. **Create a New Volume**:
   - Click the "Create volume" button at the top right.

   ![Create Volume](Screenshot%20(389).png)
   
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

   ![View Volume](Screenshot%20(390).png)
   
   - Ensure the volume state is "available".
   - Note the volume ID for reference.

## Step 3: Attach the Volume to an Instance
1. **Select the Volume**:
   - Select the volume you just created from the list.

2. **Attach Volume**:
   - Click on the "Actions" dropdown and select "Attach volume".

   ![Attach Volume](Screenshot%20(391).png)
   
   - **Instance**: Select the instance you want to attach the volume to.
   - **Device name**: Use the default or specify a device name such as `/dev/xvdb`.
   - Click "Attach volume".

## Step 4: Verify the Volume in Disk Management
1. **Connect to the Instance via MobaXterm**:
   - Use MobaXterm as your RDP client to connect to the instance.

2. **Open Disk Management**:
   - Once connected, press `Windows + R` to open the Run dialog.
   - Type `diskmgmt.msc` and press Enter to open Disk Management.

3. **Check the Disk**:
   - In Disk Management, you should see the new volume listed.
   - Initialize and format the volume if necessary to start using it.

## Conclusion
Your EBS volume is now attached to your EC2 instance and verified using Disk Management. You can now use this volume for your storage needs.

