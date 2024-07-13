# Security as a Service in Cloud Computing :

## Shared Responsibility Model :

The shared responsibility model in cloud computing defines the distinct responsibilities of the cloud service provider (CSP) and the user. It ensures that both parties understand their roles in securing the cloud environment.

### Cloud Service Provider (CSP) Responsibilities :
The security of the cloud is the responsibility of the Cloud Service Provider (CSP). This encompasses the physical infrastructure, networking, and foundational services that make up the cloud platform.

#### Example :
- **Data Center Security:** If the CSP fails to secure their data center, resulting in unauthorized physical access and potential data breaches, the CSP is at fault. This could involve breaches of physical barriers, lack of surveillance, or insufficient security protocols.

### User Responsibilities :
The security in the cloud is the responsibility of the user. This includes managing and securing data, applications, and services deployed within the cloud environment.

#### Example :
- **Access Management:** If a user provides their access credentials to another person, and that person misuses these credentials, the user is at fault, not the CSP. This underscores the importance of maintaining strict access controls and not sharing sensitive credentials.

### AWS Shared Responsibility Model :
- **Physical Security:** Managed by AWS. Example: AWS ensures that their data centers are physically secure, with multiple layers of security such as biometric scanning, surveillance, and restricted access areas.
- **Access Control:** Managed by the user. Example: If a user leaves port 80 open on their server and it gets hacked, the responsibility lies with the user to secure their ports and configure their firewall correctly.

### Example Scenarios :
1. **Scenario 1: Misconfigured Security Groups**
   - **Description:** A user misconfigures their security groups, which are essentially virtual firewalls that control inbound and outbound traffic to AWS resources. By accidentally allowing public access to sensitive data or services, they expose their system to potential attacks.
   - **Responsibility:** User. Users must ensure that security groups are correctly configured to restrict unauthorized access.

2. **Scenario 2: Data Breach at Data Center**
   - **Description:** An attacker physically breaches an AWS data center, bypassing the physical security measures put in place by AWS. This could lead to direct access to the hardware and potential data theft.
   - **Responsibility:** AWS. Ensuring physical security of data centers is the responsibility of AWS, and any breach here would be their fault.

3. **Scenario 3: Unencrypted Data**
   - **Description:** A user stores sensitive data in an S3 bucket without enabling encryption. If this data is accessed by unauthorized users due to a misconfiguration or data leak, the responsibility lies with the user.
   - **Responsibility:** User. Users must ensure their data is encrypted both at rest and in transit to protect against unauthorized access.

4. **Scenario 4: Vulnerable Application**
   - **Description:** A user deploys an application with known vulnerabilities or fails to apply necessary security patches. Attackers exploit these vulnerabilities to gain access to the system.
   - **Responsibility:** User. It is the user’s responsibility to maintain the security of their applications by applying updates and patches regularly.

5. **Scenario 5: Network Intrusion**
   - **Description:** An intruder gains access to the user’s AWS environment due to a weak or compromised password. This could lead to data breaches, unauthorized changes, or service disruptions.
   - **Responsibility:** User. Strong password policies and multi-factor authentication (MFA) should be implemented to prevent such intrusions.

## Identity and Access Management (IAM) :

1. **IAM User:** A person or application that can authenticate with an AWS account. Each user has a unique set of credentials and permissions.
    - **Example:** The root account is a highly privileged IAM user that has full access to all resources in the AWS account.
    ![IAM User](https://github.com/user-attachments/assets/df9df007-dafd-481c-9502-a0fe0bac6bc2)

2. **IAM Group:** A collection of IAM users that are granted identical authorization through group policies. This simplifies the management of permissions.
    - **Example:** Creating a "Developers" group with specific permissions and adding users to this group from the root account ensures consistent access management.
    ![IAM Group](https://github.com/user-attachments/assets/59050122-b143-4a26-b7f9-e676743195f5)

3. **IAM Policy:** The document that defines which resources can be accessed and the level of access granted. Policies are attached to users, groups, or roles to enforce permissions.
    - **Example:** An IAM policy might grant read-only access to certain S3 buckets while restricting write or delete operations.
    ![IAM Policy](https://github.com/user-attachments/assets/90be6cc6-ffcd-4a62-bf24-c36a9eb7226b)

4. **IAM Role:** A useful mechanism to grant a set of permissions for making AWS service requests without using long-term credentials. Roles can be assumed by trusted entities, such as EC2 instances or other AWS services.
    - **Example:** An IAM policy grants access to the photos bucket -> an IAM role assumed by an EC2 instance -> the application running on the EC2 instance has permissions to access the S3 bucket photos.
    ![IAM Role](https://github.com/user-attachments/assets/36c07da4-b8b0-4fe8-a8ee-6aa87d691070)
