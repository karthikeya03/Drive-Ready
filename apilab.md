# Lab 6.1: Developing REST APIs with Amazon API Gateway

## Lab Overview and Objectives
In this lab, you will create a REST API using Amazon API Gateway. By the end of this lab, you should be able to:

- Create simple mock endpoints for REST APIs and use them in your website.
- Enable Cross-Origin Resource Sharing (CORS).

**AWS Service Restrictions**: Access to AWS services and actions might be restricted. Errors may occur if you attempt actions beyond the lab instructions.

## Scenario
In the previous lab, you built a web application for a café, creating an Amazon DynamoDB table named `FoodProducts` to store information about menu items. You loaded JSON-formatted data into this table.

![image](https://github.com/user-attachments/assets/7ed7bc12-573b-4b31-b433-80cd656c111f)

You also configured code to:
- Scan the DynamoDB table to retrieve product details.
- Return a single item by product name using `get-item`.
- Create a Global Secondary Index (GSI) named `special_GSI` to filter out menu items on offer.

In this lab, you will continue by using Amazon API Gateway to configure mock data endpoints. These endpoints will eventually be connected to the DynamoDB table.
. [GET] /products (which will eventually invoke a DynamoDB table scan)
. [GET] /products/on_offer (which will eventually invoke a DynamoDB index scan and filter)
. [POST] /create_report (which will eventually trigger a batch process that will send out a report)

## Tasks

### Task 1: Preparing the Development Environment
**Definition**: The development environment is a setup including all the tools and configurations needed to build and test your application.

When you start the lab, the following resources are pre-created for you in the account.

![image](https://github.com/user-attachments/assets/1ab553f2-8621-4f9f-9a5d-4d9ec0ab0cd6)

However, by the end of this lab, you will have created the following architecture:

![image](https://github.com/user-attachments/assets/bd12f1a8-52c0-43a9-9897-56bf40406f25)


1. **Access AWS Cloud9**:
   - Connect to the AWS Cloud9 IDE named `Cloud9 Instance`.

2. **Download and Extract Files**:
   - Run `wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-200-ACCDEV-2-91558/04-lab-api/code.zip -P /home/ec2-user/environment`
   - Extract with `unzip code.zip`.

3. **Run Setup Script**:
   - Run `chmod +x resources/setup.sh && resources/setup.sh`.
   - Enter your IP address when prompted.

4. **Verify Installations**:
   - Check AWS CLI version: `aws --version` (should show version 2).
   - Verify Boto3: `pip show boto3`.

5. **Verify Website**:
   - Open Amazon S3 console and check for the `index.html` file.
   - Load the website and check the developer console for logs.

### Task 2: Creating the First API Endpoint (GET)
**Definition**: A GET endpoint retrieves data from the server. In this task, you will create a GET endpoint to fetch mock data.

1. **Open the File**:
   - Open `create_products_api.py` in Cloud9.

2. **Update Code**:
   - Replace placeholder values with the correct API Gateway client values.

3. **Run the Code**:
   - Save changes and run `python create_products_api.py`.

4. **Verify API Gateway**:
   - Open API Gateway console, check the `ProductsApi` and `GET` method.
   - Test the method to see mock data response.

### Task 3: Creating the Second API Endpoint (GET)
**Definition**: This task involves creating another GET endpoint for a different purpose, such as filtering items based on certain criteria.

1. **Open the File**:
   - Open `create_on_offer_api.py` in Cloud9.

2. **Update Code**:
   - Replace placeholders with correct values for creating the `on_offer` endpoint.

3. **Run the Code**:
   - Save changes and run `python create_on_offer_api.py`.

4. **Verify API Gateway**:
   - Check the `/on_offer` resource in API Gateway and test it.

### Task 4: Creating the Third API Endpoint (POST)
**Definition**: A POST endpoint sends data to the server to create or update a resource. In this task, you will create a POST endpoint.

1. **Open the File**:
   - Open `create_report_api.py` in Cloud9.

2. **Update Code**:
   - Replace placeholders with the correct values for creating the `create_report` endpoint.

3. **Run the Code**:
   - Save changes and run `python create_report_api.py`.

4. **Verify API Gateway**:
   - Check the `/create_report` resource and test it.

### Task 5: Deploying the API
**Definition**: Deployment involves making your API available for use. You will deploy the API to a stage in this task.

1. **Deploy the API**:
   - In API Gateway console, choose `Deploy API`.
   - Create a new stage named `prod` and deploy.

2. **Copy Invoke URL**:
   - Save the Invoke URL for use in the website configuration.

### Task 6: Updating the Website to Use the APIs
**Definition**: Updating the website involves configuring it to use the newly created API endpoints for fetching and displaying data.

1. **Update Config File**:
   - Open `config.js` in Cloud9.
   - Replace `null` with the Invoke URL and save changes.

2. **Update and Run Script**:
   - Open `update_config.py`, update the bucket name, and run the script: `python update_config.py`.

3. **Test the Website**:
   - Load the website, check that it displays mock data from API Gateway.
   - Check developer console for logs and ensure API calls are working.

## Definitions
- **REST API**: A Representational State Transfer Application Programming Interface (API) is an architectural style for designing networked applications.
- **API Gateway**: A managed service that provides a gateway for API requests, allowing you to create, publish, maintain, monitor, and secure APIs.
- **CORS**: Cross-Origin Resource Sharing is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the resource originated.
- **Mock Data**: Sample data used for testing purposes before real data is available.

## Conclusion
Congratulations! You've successfully created and deployed a REST API with mock data endpoints using Amazon API Gateway. The next steps involve replacing mock endpoints with real endpoints that connect to your DynamoDB table.

