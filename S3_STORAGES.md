# EBS: Elastic Block Storage

## AWS S3: Amazon Simple Storage Service
Amazon S3 is an object storage service that offers scalability, data availability, security, and performance. It allows you to store and retrieve any amount of data from anywhere.

### Key Features:
- **Unlimited Storage**: No limit to the amount of data you can store.
- **Storage Tiers**: Different types of storage classes for various use cases.

### Storage Tiers:
1. **S3 Standard**
   - **Availability**: 99.99%
     - **Definition**: The percentage of time that the service is operational and accessible.
   - **Durability**: 11 9's (99.999999999%) 
     - **Definition**: The likelihood that your data will remain intact and uncorrupted over a given year.
   - **Use Case**: Fulfills daily storage needs with unlimited storage.

2. **S3 Standard-IA (Infrequent Access)**
   - **Use Case**: For data that is accessed less frequently but requires rapid access when needed.

3. **S3 One Zone-IA**
   - **Use Case**: Stores data in a single Availability Zone, reducing costs.
   - **Availability**: Lower than S3 Standard-IA.

4. **S3 Glacier**
   - **Use Case**: For archival storage where data is accessed once every 6 months.
   - **Cost**: Less expensive with a minimum of 2 hours retrieval time.

5. **S3 Glacier Deep Archive**
   - **Use Case**: For long-term data archiving, with retrieval times of up to 5 hours.
   - **Cost**: Very cost-effective.
   - **Storage**: Data is stored offline on physical hard disks and uploaded to the cloud upon request.
   - **Example**: Apollo Hospitals uses S3 Glacier to create datasets.
     - **Dataset**: A collection of related sets of information composed of separate elements but can be manipulated as a unit by a computer.

## S3 Snow Family
AWS provides physical devices to transfer large amounts of data from on-premises environments to the cloud.

1. **S3 Snowball**
   - **Use Case**: For transferring terabytes to petabytes of data.
   - ![Snowball](https://github.com/karthikeya03/Drive-Ready/assets/120096427/e8928289-6867-4c05-b105-a02082082847)

2. **S3 Snowmobile**
   - **Use Case**: For transferring petabytes to exabytes of data.
   - **Status**: Discontinued.
   - ![Snowmobile](https://github.com/karthikeya03/Drive-Ready/assets/120096427/8bfe25f5-bfac-4b0a-b7fe-f4ae8f48459e)

## Creating a Bucket

### Steps:
1. **Sign in to the AWS Management Console**.
2. **Open the S3 Console**.
   ![image](https://github.com/karthikeya03/Drive-Ready/assets/120096427/28b4523a-716c-4c5f-b859-0edee4e586c8)
3. **Choose 'Create Bucket'**.
4. **Configure Bucket Settings**:
   ![image](https://github.com/karthikeya03/Drive-Ready/assets/120096427/a1df4956-2223-4f06-94dc-0f60599304b1)
   - **Name and Region**: Enter a unique bucket name and select the AWS Region.
    ![image](https://github.com/karthikeya03/Drive-Ready/assets/120096427/2c7af4bd-bc95-4926-916a-29b1241176ef)

   - **Object Ownership**: Select the appropriate settings.
   - **Block Public Access Settings**: Configure as needed.
     ![image](https://github.com/karthikeya03/Drive-Ready/assets/120096427/1f99f695-9b0d-4029-a242-fdbb1ec68e2e)
   - **Bucket Versioning**: Enable if needed.
5. **Upload Some files** :
![image](https://github.com/karthikeya03/Drive-Ready/assets/120096427/485292f7-d387-42e4-96fa-d60b94264293)

# Making an Object Public and Downloadable in AWS S3

## Prerequisites

- AWS account with appropriate permissions
- S3 bucket and object already created
- AWS CLI installed and configured (optional for CLI commands)

## Step 1: Set Permissions

1. **Navigate to the S3 Dashboard:**
   - Open the AWS Management Console.
   - Navigate to the S3 Dashboard.

2. **Select Your Bucket:**
   - Click on the name of the bucket containing the object you want to make public.

3. **Navigate to the Object:**
   - Find and click on the object you want to make public.

## Step 2: Go to Permissions

1. **Access the Object Permissions:**
   - In the **Object overview** section, click on the **Permissions** tab.

## Step 3: Enable ACL (Access Control List)

1. **Edit Object Permissions:**
   - Click on **Edit** under **Access control list (ACL)**.

2. **Grant Public Read Access:**
   - Check the box next to **Everyone (public access)** under the **Read** column.
   - This will allow everyone to view the object.
   - Click on the **Save changes** button.

   ![Screenshot showing how to enable ACL](https://github.com/karthikeya03/Drive-Ready/assets/120096427/a6369be7-7eb6-4143-9a52-1635efcb0944)
   
3. **Make Object Public using ACL:**
   - Confirm that the object is now publicly accessible by checking the **Public** tag.

   ![Screenshot showing the public status](https://github.com/karthikeya03/Drive-Ready/assets/120096427/7c08319a-78dd-4303-a6d8-a10b533fd59b)
   
4. **Make Public:**
   - Ensure the object's URL is now accessible without any authentication.
   - This URL can be shared with anyone who needs to download the object.

   ![Screenshot of the public URL](https://github.com/karthikeya03/Drive-Ready/assets/120096427/813c2e8b-b083-40c3-a3a6-0c6abce440b8)

# Deploy Static Website Using S3

## 1. Create a Bucket

- Go to the S3 service in the AWS Management Console.
- Click on “Create bucket”.
- Enter a unique bucket name.
- Select your preferred region.
- Click “Create bucket”.

## 2. Edit Object Permissions

- Navigate to your newly created bucket.
- Click on the “Permissions” tab.

## 3. Enable Public Access Using ACL

- In the “Permissions” tab, under “Block public access (bucket settings)”, click “Edit”.

- Uncheck “Block all public access”.

- Click “Save changes”.

  ![ACL Settings](https://github.com/karthikeya03/Drive-Ready/assets/120096427/4fb4fa87-57d4-4b5b-8e26-a708ba2463ad)

## 4. Grant Public Read Access

- Upload your website files to the bucket.
- After uploading, select the uploaded files.
- Click “Actions” and then “Make public using ACL”.

## 5. Upload Website Files

- Upload your website files (HTML, CSS, JavaScript, etc.).

- Optionally, you can upload a zip file and extract it in the S3 bucket.

  ![Upload Files](https://github.com/karthikeya03/Drive-Ready/assets/120096427/0419cd79-1eac-4b48-a909-d6f1e1d79ad6)

## 6. Configure Static Website Hosting

- Go to the “Properties” tab.

- Scroll down to “Static website hosting”.

- Click “Edit” and select “Enable”.

- Enter the index document (e.g., `index.html`).

- Optionally, enter the error document (e.g., `error.html`).

- Click “Save”.

  ![Static Website Hosting](https://github.com/karthikeya03/Drive-Ready/assets/120096427/08191cc6-875d-4271-bd22-db2081353eb1)

## 7. Access Your Website

- Go back to the “Properties” tab.
- Under “Static website hosting”, copy the “Bucket website endpoint” URL.
- Open this URL in your web browser to see your deployed static website.
