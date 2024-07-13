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
      <br>
    ![IAM Group](https://github.com/user-attachments/assets/59050122-b143-4a26-b7f9-e676743195f5)

3. **IAM Policy:** The document that defines which resources can be accessed and the level of access granted. Policies are attached to users, groups, or roles to enforce permissions.
    - **Example:** An IAM policy might grant read-only access to certain S3 buckets while restricting write or delete operations.
    ![IAM Policy](https://github.com/user-attachments/assets/90be6cc6-ffcd-4a62-bf24-c36a9eb7226b)

4. **IAM Role:** A useful mechanism to grant a set of permissions for making AWS service requests without using long-term credentials. Roles can be assumed by trusted entities, such as EC2 instances or other AWS services.
    - **Example:** An IAM policy grants access to the photos bucket -> an IAM role assumed by an EC2 instance -> the application running on the EC2 instance has permissions to access the S3 bucket photos.
    ![IAM Role](https://github.com/user-attachments/assets/36c07da4-b8b0-4fe8-a8ee-6aa87d691070)

## Introduction to AWS IAM

AWS Identity and Access Management (IAM) is a service that helps you manage access to AWS resources securely. With IAM, you can control who can access your AWS resources and what actions they can perform. This guide will walk you through the basics of IAM, focusing on users, groups, and permissions.

### Overview and Objectives
In this guide, you'll learn to:

1. **Explore IAM Users and Groups**:
   - Look at users and groups that are already set up.
   - Check the permissions assigned to these users and groups.

2. **Add Users to Groups**:
   - Follow a practical scenario where you add users to groups with specific permissions.

3. **Use the IAM Sign-In URL**:
   - Find and use the special URL for IAM users to sign in.

4. **Test the Effects of Policies**:
   - Experiment with how different policies affect what users can and cannot do.

### AWS Service Restrictions :
In this guide, you might find that access to some AWS services is limited to only what is needed for the tasks. This is to ensure you focus on the relevant services and actions.

![image](https://github.com/user-attachments/assets/152f4326-3984-46ef-8b2b-04acd7bc7b55)


### Managing IAM Users and Roles :
1. **Users**:
   - Create individual users and give them unique security credentials like passwords and access keys.
   - Set permissions to control what actions each user can perform.

2. **Roles** :
   - Define roles that have specific permissions. Roles can be assumed by users or services needing temporary access.

3. **Federated Users** :
   - Allow users from your existing organization (like those in Active Directory) to access AWS resources without needing to create individual IAM users for them.

### Accessing the AWS Management Console :
1. Start the lab and wait for the session to initialize.
2. Click the link provided to open the AWS Management Console. Wait until the session is fully ready (indicated by a green icon).

### Tasks :

#### Task 1: Explore Users and Groups
1. **Explore Users**:
   - Open the IAM console by searching for IAM in the services search box.
   - Click on "Users" in the left navigation pane to see the list of users (`user-1`, `user-2`, `user-3`).
   - Click on `user-1` and explore the permissions, groups, and security credentials tabs to understand what this user can do and their access details.

2. **Explore Groups**:
   - Click on "User groups" in the left navigation pane.
   - Explore groups like `EC2-Admin`, `EC2-Support`, and `S3-Support` by clicking on each group and examining the permissions assigned through policies.

    ![image](https://github.com/user-attachments/assets/7e17b903-7f75-441f-8d56-8c4e3686ec88)

### Business Scenario :
> For the remainder of this lab, you will work with these Users and Groups to enable permissions supporting the following business scenario:
> Your company is growing its use of Amazon Web Services, and is using many Amazon EC2 instances and a great deal of Amazon S3 storage. You wish to give access to new staff depending upon their job function:

![image](https://github.com/user-attachments/assets/f142495d-fcab-47b6-9ebb-f63fb069001e)

#### Task 1: Add Users to Groups
1. **Add user-1 to S3-Support Group**:
   - In the IAM console, click on "User groups" and select `S3-Support`.
   - Go to the "Users" tab and click "Add users".
   - Select `user-1` and click "Add users" to include `user-1` in the `S3-Support` group.
     
![image](https://github.com/user-attachments/assets/980e13bd-6a98-485d-9dc4-d4f659a038ff)

2. **Add user-2 to EC2-Support Group**:
   - Follow the same steps as above to add `user-2` to the `EC2-Support` group.

3. **Add user-3 to EC2-Admin Group**:
   - Similarly, add `user-3` to the `EC2-Admin` group.

Each group should now show a user count of 1, indicating that the users have been successfully added to their respective groups.

![image](https://github.com/user-attachments/assets/a5b2c53f-cbab-4b8f-aedd-5a5f5b4a3160)

#### Task 2: Sign-In and Test Users
1. **Test user-1**:
   - Open a private browser window and use the IAM sign-in URL.
   - Sign in as `user-1` and Password: `Lab-Password1`.
   - Verify that `user-1` can access S3 but cannot access EC2.
![image](https://github.com/user-attachments/assets/e4e82377-9cc4-4119-afdf-32ed9913015e)

2. **Test user-2**:
   - Sign out `user-1` and sign in as `user-2` and Password: `Lab-Password2`.
   - Verify that `user-2` can access EC2 but cannot make changes or access S3.
![image](https://github.com/user-attachments/assets/770b6e7a-91c6-484b-9c71-45c8b962fcc6)

3. **Test user-3**:
   - Sign out `user-2` and sign in as `user-3`.
   - Verify that `user-3` has full access to EC2, including the ability to stop and start instances.

### Conclusion
By the end of these tasks, you will have:
- Explored IAM users and groups.
- Inspected and tested IAM policies.
- Managed users and their permissions in a practical, real-world scenario.

