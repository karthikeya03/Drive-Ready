# SESSION 12 : Platform as a Service: Elastic Beanstalk

## Creating an Application

1. **Create Application**
   - Navigate to the Elastic Beanstalk section in AWS.
   - Click on "Create Application".

2. **Enter Domain Name**
   - Enter a desired domain name.
   - Check for its availability.

3. **Select a Platform**
   - Choose the appropriate platform for your application.

4. **Upload Code**
   - Open the folder containing your application code.
   - Select all the files of the internal components.
   - Create a zip file of these files.

5. **Provide Version Label**
   - Give a version label for your application.
  
     ![bean](https://raw.github.com/karthikeya03/IMAGES/JustMain/12.1.png)

## Instance Configuration

1. **Select an Instance**
   - Choose between a high or single instance based on your needs.

2. **EC2 Instance Role**
   - Select the default EC2 instance role.

3. **Key Pair**
   - Select the default VPC key.

4. **Instance Profile**
   - Select the default LabInstanceProfile.

## Network Configuration

1. **VPC Selection**
   - Select the first VPC (if it doesn't work, choose another option).

2. **Instance Zones**
   - Select two instance zones to ensure high availability of the website.

3. **EC2 Security Group**
   - Use the default security group settings.

## Final Steps

1. **Review Settings**
   - Click "Next" to review your configuration.

2. **Deploy Application**
   - Click "Next" again to start the deployment process.
  
      ![bean](https://raw.github.com/karthikeya03/IMAGES/JustMain/12.2.png)
