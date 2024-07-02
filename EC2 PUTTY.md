# SESSION 10: CREATION OF EC2 INSTANCE THROUGH PUTTY SOFTWARE

**Virtual Machines:** Virtual servers that can be used for various tasks.

**Key Terms:**
- **EC2 (Elastic Compute Cloud):** Virtual servers in AWS.
- **AMI (Amazon Machine Image):** A template used to create an instance.

---

## Steps to Create an EC2 Instance

### 1. Login to AWS Academy
- Go to AWS Academy.
- Navigate to **Modules → Sandbox Environment**.
- Open the link in a new tab.
- Click **Start Lab**. This opens another page; close this tab and return to the previous page.
- Click on the **AWS** button.

### 2. Access EC2
- Open **EC2** from the recently viewed tabs.
- Click the **Launch Instance** button.

### 3. Configure Your Instance
- **Instance Name:** Give a name and tags to your instance.
- **Application and OS Images (Amazon Machine Image):** Select your Linux distribution (e.g., Redhat, Ubuntu, AWS Linux, Windows).
- **Instance Type:** Leave this as the default.
- **Key Pair Login:**
  - Click on **Create a new key pair**.
  - Enter a name for the key pair.
  - Select **.ppk** as the file format.
  - Ensure **RSA** is selected as the key pair type.
  - Click **Create key pair** and download the **.ppk** file.

### 4. Launch the Instance
- Click on the hyperlink (e.g., `(i-08f7b1a434c34c127)`) in the message indicating a successful instance launch.
- Copy your instance's IP address.
- Note your platform provider (e.g., Ubuntu).

### 5. Connect to Your Instance Using PuTTY
- **Download PuTTY:**
  - If not installed, download PuTTY from [PuTTY Download Page](https://www.putty.org/).
  - Choose **64-bit x86 in MSI (Windows Installer)** and install it.
- **Open PuTTY:**
  - Enter the copied IP address in the **Host Name** field.
  - In the left-hand category, navigate to **SSH → Auth**.
  - In **Private key file for authentication**, click **Browse** and select the downloaded **.ppk** file.
  - Click **Open**.
- **Login:**
  - When prompted, enter the username (e.g., `ubuntu`).
  - You should now be logged into your EC2 instance.
  - **Login as:** `ubuntu` for Ubuntu, `ec2-user` for Amazon Linux.

---

## Four Ways to Access a Virtual Machine (VM) in Microsoft Azure

1. **MobaXterm:** Select **RDP**.
2. **PuTTY:** Select **Administrator**.
3. **In Browser**.
4. **CMD:**
   - Open CMD in the folder that contains the **.pem** file.
   - Enter the command: `ssh -i (keypairname.pem) ubuntu@ (public ip address)`: **Port 22**.

---

## Using Remote Desktop Connection to Access Your AWS EC2 Instance



![RDP](https://raw.github.com/karthikeya03/IMAGES/JustMain/10.1.jpg)



### Remote Desktop Connection (RDC)
Allows you to connect to your AWS EC2 instance from a Windows machine.

### Steps to Connect to Your EC2 Instance Using Remote Desktop Connection (RDC)

1. **Launch Remote Desktop Connection:**
   - Press **Win + R** to open the Run dialog.
   - Type **mstsc** and press Enter to open Remote Desktop Connection.

2. **Connect to Your EC2 Instance:**
   - Paste the public IP address of your EC2 instance in the **Computer** field.
   - Click **Connect**.

3. **Enter Your Credentials:**
   - When prompted, enter `administrator` as the username.
   - Enter the password you set during the instance creation.

4. **Configure Local Resources:**
   - Before connecting, click on **Show Options** to reveal more settings.
   - Go to the **Local Resources** tab.

5. **Redirect Local Drives:**
   - Under **Local devices and resources**, click **More...**.
   - Check the **Drives** box to redirect your local drives to the virtual machine. This allows you to access your local files from the remote session.

6. **Finalize and Connect:**
   - Click **OK** to close the Local devices and resources window.
   - Click **Connect** to start the remote session.

### Additional Tips
- **Accessing Local Files:** By redirecting your drives, you can easily transfer files between your local machine and the EC2 instance.

### Summary
1. Press **Win + R** and type **mstsc** to open Remote Desktop Connection.
2. Paste your EC2 instance's public IP address and click **Connect**.
3. Enter `administrator` and the password.
4. Go to **Show Options → Local Resources → More... → check Drives** to redirect your local drives.
5. Click **Connect** to access your EC2 instance.

---

## Difference Between SSD and HDD

| Feature        | SSD (Solid State Drive)                             | HDD (Hard Disk Drive)                            |
|----------------|-----------------------------------------------------|--------------------------------------------------|
| **Technology** | Uses NAND flash memory, no moving parts             | Uses spinning disks (platters) and moving heads  |
| **Speed**      | Much faster read/write speeds compared to HDDs      | Slower read/write speeds compared to SSDs        |
| **Durability** | More resistant to physical shock and damage         | More susceptible to physical damage              |
| **Noise**      | Silent operation due to lack of moving parts        | Audible noise from spinning disks and moving parts |

**Usage Scenarios:**
- **SSD:** Ideal for faster boot times, quicker file transfers, and improved overall system responsiveness.
- **HDD:** Suitable for large storage capacities at lower cost per gigabyte, but slower performance for data access.

---

## Components of AWS

- **High-Speed Data Transfer:**
  AWS needs to support fast data transfer between its data centers and to the end-users. Fiber optic cables provide the high bandwidth required to handle large volumes of data with minimal delay.

- **Low Latency:**
  Applications and services hosted on AWS often require real-time or near-real-time data processing and communication. Fiber optics help achieve low latency, ensuring quick response times for services like streaming, gaming, and real-time analytics.

- **High Availability and Reliability:**
  AWS aims to provide highly available services with minimal downtime. Fiber optic networks are less prone to interference and signal loss compared to traditional copper cables, ensuring a more reliable and stable connection.

- **Scalability:**
  As AWS scales to meet increasing demand, the underlying infrastructure must support higher data throughput. Fiber optic cables can handle vast amounts of data, allowing AWS to scale its operations efficiently.

- **Global Reach:**
  AWS operates data centers worldwide, interconnected through a robust global network. Fiber optic cables, including undersea cables, are used to connect these data centers, enabling fast and reliable global data transmission.

- **Advanced Networking Technologies:**
  AWS leverages technologies such as Wavelength Division Multiplexing (WDM) to maximize the capacity of its fiber optic networks. This allows AWS to offer high-performance services like AWS Direct Connect, which provides a dedicated network connection between the user's premises and AWS.
