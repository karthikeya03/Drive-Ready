Lab 5.1: Working with Amazon DynamoDB
Lab overview and objectives
In this lab, you use Amazon DynamoDB to store and manage menu information. Using databases, such as DynamoDB, simplifies data management because you can easily query, sort, edit, and index data. You will use both the AWS Command Line Interface (AWS CLI) and the AWS SDK for Python (Boto3) to work with DynamoDB. 

In upcoming labs, you will use application programming interface (API) calls from the café website to dynamically retrieve and update data that's stored in a DynamoDB table. 

After completing this lab, you should be able to:

Create a new DynamoDB table 
Add data to the table 
Modify table items based on conditions 
Query the table 
Add a global secondary index to the table
 

When you start the lab, the following resources are already created for you in the AWS account:

AWS Cloud9 integrated development environment (IDE) instance
Amazon Elastic Compute Cloud (Amazon EC2) instance for authoring code and running commands through the AWS CLI

![image](https://github.com/user-attachments/assets/98064026-5a24-4afc-9f77-5309437fb39f)

At the end of this lab, your architecture should look like the following example:

![image](https://github.com/user-attachments/assets/d07b8b04-1b06-40d1-8956-745cb016e147)

Scenario :
The café website is up and running, and the café staff noticed a significant increase in new customer visits. Multiple customers also mentioned that it would be helpful if the website had an up-to-date menu. They could then use the menu to check the availability of food items before going to the café. 

Frank and Martha ask Sofía to explore whether she can implement this feature for customers. Sofía is feeling more confident in her coding skills and has also been learning about different ways to store information in AWS. She knows that before they can dynamically update data on the website, she must first choose a data storage service to hold the data. She also needs to learn how to manage table data, load the product records, and create scripts to retrieve information from the data platform.

starting resources :

A business request from the café: Store menu information in the cloud
Frank and Martha mentioned to Sofía that they want the website to dynamically update its menu information. To prepare for this new functionality, Sofía decides to store this information in DynamoDB. 

Café staff must be able to retrieve information from the table. Sofía decides to create one script that retrieves all inventory items from the table and another script (as a proof of concept) that uses a product name to retrieve a single record.

For this first challenge, you take on the role of Sofía. You use the AWS CLI and the SDK for Python to configure and create a DynamoDB table, load records into the table, and extract data from the table.

Task 1: Preparing the lab:

Connect to the AWS Cloud9 IDE.

From the Services menu, search for and select Cloud9. You should see an existing IDE named Cloud9 Instance.

In the Cloud9 Instance pane, choose Open IDE.

The AWS Cloud9 IDE loads in a new browser tab.

![image](https://github.com/user-attachments/assets/8d308d62-f29b-45be-b4ad-15344e68ddf0)

Download and extract the files that you need for this lab.

![image](https://github.com/user-attachments/assets/92b2c977-d667-4a11-b37a-8e1fa523898e)


Extract the file by running the following command: 

![image](https://github.com/user-attachments/assets/902e9df8-5be8-4340-a641-7bad40da1e70)

Run a script that upgraded the version of Python installed on the Cloud9 instance. It will also upgrade the version of the AWS CLI installed.

To set permissions on the script and then run it, run the following commands:

![image](https://github.com/user-attachments/assets/b6d1f6a7-f110-4d12-a825-b6c9663c618b)

Verify the AWS CLI version and also verify that the SDK for Python is installed.

Confirm that the AWS CLI is now at version 2 by running the aws --version command.

In the AWS Cloud9 Bash terminal (at the bottom of the IDE), run the following command:

![image](https://github.com/user-attachments/assets/e1809618-b653-4d9e-af39-1d14ade1e46f)

Task 2: Creating a DynamoDB table by using the SDK for Python
To store and dynamically manage the café's menu items, Sofía decides to create a new DynamoDB table. 

In this task, you take on the role of Sofía to create and define the new DynamoDB table.

1.
First, verify that no tables exist in the environment by using the AWS Management Console:

In the top-left corner of the AWS Cloud9 IDE, choose the AWS Cloud9 icon, and choose Go To Your Dashboard.

A new tab opens in your browser. 

In the new tab, open the DynamoDB console by choosing the Services menu and then choosing DynamoDB.

![image](https://github.com/user-attachments/assets/5e207d63-0588-4262-b9ef-6863181d8053)

On the left, expand the DynamoDB navigation pane by choosing the  menu icon.

From the DynamoDB menu, choose Tables.

Review the Tables pane.

![image](https://github.com/user-attachments/assets/b1623038-0610-480a-a14a-9cb46e651514)

2.Edit the script that will create the table:

Return to the AWS Cloud9 IDE browser tab.
In the navigation pane of the AWS Cloud9 IDE, expand the python_3 directory. 
Open the create_table.py script by double-clicking it.
Replace the <FMI_1> placeholder with the table name, which is:

![image](https://github.com/user-attachments/assets/bf11b257-67b1-49c9-b8a6-f915e89f10d4)

3. To understand what the script does, review the code:

The line that defines the DDB variable also configures the SDK for Python resource. 
It sets both the AWS service and the AWS Region that the Python script will call.

![image](https://github.com/user-attachments/assets/a84f61d2-08d1-4284-baa2-3d655a627526)
![image](https://github.com/user-attachments/assets/5ddc5a75-eb7e-4bcf-bc0e-825376dc2e5b)

The line that defines the table variable also creates the table:

💁‍♂ Boto requires key values arguments rather than the object literal format, so you use **params to pass the parameters to the create_table operation.

![image](https://github.com/user-attachments/assets/3023e29a-7a1d-451c-bcdc-bdc98801e518)

3. In the AWS Cloud9 terminal window, go to the python_3 directory, and run the following code:

```
cd python_3
python3 create_table.py
```

![image](https://github.com/user-attachments/assets/9415edb3-59b3-4c2d-b646-8290e8a02465)

4. Return to the browser tab with the DynamoDB console. Use the refresh icon on the far right, choose FoodProducts, and verify that the table has a created state of Active.

![image](https://github.com/user-attachments/assets/c08c3b6b-0eaf-4a40-820a-7daea71fa750)

Task 3: Working with DynamoDB data – Understanding DynamoDB condition expressions :

1. Review the JavaScript Object Notation (JSON) data that defines the new record.

In the AWS Cloud9 IDE, expand the resources folder.
Open the not_an_existing_product.json file by double-clicking it.
Analysis: This file contains one item with two attributes: product_name and product_id. Both of these attributes are strings. The primary key (product_name) was defined when the DynamoDB table was created. Because DynamoDB tables are schemaless (to be exact, not bound by a fixed schema), you can add new attributes to the table when items are inserted or updated. With DynamoDB, you don't need to change the table definition before you add records that contain additional attributes.

 2. To insert the new record, run the following command. Ensure that you are still in the python_3 folder.

    ![image](https://github.com/user-attachments/assets/01b84c1f-6310-4e30-b99a-56a5d8416f07)

3. Verify that the new record was added to the table by using the DynamoDB console to complete the following tasks:

Return to the DynamoDB console and choose the FoodProducts link.

Choose Explore table items.

Under Items returned, review the information. 

![image](https://github.com/user-attachments/assets/06f36d6c-7082-443e-959c-9558425b109b)

4. Update the JSON data to create a new record:

Return to the AWS Cloud9 IDE and load the not_an_existing_product.json file in the text editor.

Replace the product_name value of <best cake> with best pie

Do not change the product_id value.

In the upper left, choose File > Save to save your changes.

5. To add the new record, run the following command. Notice that this command is the same AWS CLI command that you used to add the first record.

   ![image](https://github.com/user-attachments/assets/578d7718-e980-4283-867f-2a7714247d1c)
   
7. Again, view the new record in the table by using the console:
 ![image](https://github.com/user-attachments/assets/1c766096-b6cb-4454-8ccf-bdafd26f414f)
![image](https://github.com/user-attachments/assets/01992740-c747-4b88-9489-ae7d0d82009b)
💁‍♂ Because the product_id attribute is not the primary key of the table, it doesn't need to be unique, and a new record is inserted successfully. If the value of product_name is different, a new record is created in the table.

What do you think will happen if you try to insert a duplicate record? 

 8. In the DynamoDB console, choose Run again and review the Items returned list. Do you notice any changes?

💁‍♂ When a primary key doesn't exist in the table, the DynamoDb put-item command inserts a new item. However, if the primary key already exists, this command replaces the existing record with the new record, removing any previous attributes. 
This behavior is why you don't see a new item in the table: the record was overwritten with identical information. The primary key prevents the same product_name values from being added multiple times.

Now, try to insert a record with an existing primary key and a different product_id value.    

9. Update the JSON record:

Return to the AWS Cloud9 IDE and the not_an_existing_product.json file.

Don't change the value of product_name.

Replace the product_id value of <676767676767> with 3333333333

In the upper left, choose File > Save to save your changes.

10. Run the previous AWS CLI put-item command again:

 ![image](https://github.com/user-attachments/assets/bee35828-a41a-4bee-8395-bb54b4112673)

11. View the table data in the DynamoDB item explorer by choosing Run :
    ![image](https://github.com/user-attachments/assets/7b2ac896-b993-4faa-a9d9-80baf5948c2a)

12. Update the JSON record:

Return to the AWS Cloud9 IDE and the not_an_existing_product.json file.

Don't change the value of product_name.

Replace the product_id value of <3333333333> with 2222222222

Save your changes.

13. In the AWS Cloud9 terminal, run the following AWS CLI put-item command:
    
    ![image](https://github.com/user-attachments/assets/9631022c-f1c4-4e1d-a5c6-cdc56058c128)
    
 This behavior is expected because the condition expression prevented an overwrite of the existing item.

If you like, you can also make sure the record was unchanged by viewing the data in the DynamoDB console again.

Next, you apply what you learned about conditional expressions to working with the SDK.

 
Task 4: Adding and modifying a single item by using the SDK :

1. Update the conditional_put.py script.

In the AWS Cloud9 IDE, go to the python_3 directory.

Open the conditional_put.py script.

Replace the <FMI> placeholders as directed in the script. You can also refer to the code analysis in the following step.

In the upper left, choose File > Save to save your changes.

 2. Review the code to understand what it does:

Focus on the definition of the response variable, which begins on line 49. 

Notice the call to the put_item operation. In the SDK for Python, the put_item operation is equivalent to the put-item command in the AWS CLI. 

The put_item SDK operation requires a value for Item, which defines the record that is inserted into the table.

3. Review the code to understand what it does:

Focus on the definition of the response variable, which begins on line 49. 

Notice the call to the put_item operation. In the SDK for Python, the put_item operation is equivalent to the put-item command in the AWS CLI. 

The put_item SDK operation requires a value for Item, which defines the record that is inserted into the table.

 ![image](https://github.com/user-attachments/assets/06e65462-f5c7-43f4-bc3e-0d3a62c23234)

4.In the AWS Cloud9 terminal, run the file.

python3 conditional_put.py

![image](https://github.com/user-attachments/assets/946f96b7-4908-4190-a0c2-027fb41c4c37)

 5. python3 conditional_put.py
#Done

6. In the AWS Cloud9 IDE, update the conditional_put.py script by replacing the product_name value of <apple pie> to cherry pie and saving the file.

Run the python3 conditional_put.py again.

 ![image](https://github.com/user-attachments/assets/f4bbbf17-6bc7-419b-9224-883af052925e)

Task 5: Adding multiple items by using the SDK and batch processing

1. In the DynamoDB Item explorer, refresh the view of the data by choosing Run
2. Delete all records:

Select the check boxes for all the table records. 
From the Actions menu, choose Delete item(s). 
In the pop-up window confirmation box, enter Delete and choose Delete items

3. In the AWS Cloud9 IDE, open the resources > test.json file, and review the data.

This file contains six records that you use to test the batch-load script. Notice that this file contains multiple entries for apple pie on purpose. 

Now, update the script that performs the batch load.

4. Update the test_batch_put.py script:

In the AWS Cloud9 IDE, open the python_3 > test_batch_put.py script.

Update the <FMI_1> placeholder with the FoodProducts table name. 

Replace the <FMI_2> with the product_name primary key name. 

In the upper left, choose File > Save to save your changes.

5. To understand what the script does, review the code:

The table that will be written to by the script is defined in the table variable on line 11. 

The with statement that begins on line 12 calls batch_writer(), which opens the connection to the database. 

Then, the code loops through each record and inserts the new data into the FoodProducts table:

![image](https://github.com/user-attachments/assets/1836098b-a160-4a3b-923a-6c68b0055e20)

6. In the AWS Cloud9 terminal, run the file:
   ![image](https://github.com/user-attachments/assets/827b4f66-4086-4b1b-91ae-7ed73127aa83)
   
7. In the DynamoDB Item explorer, select the FoodProducts table, and run the scan again.
![image](https://github.com/user-attachments/assets/81b6fc01-1b7a-43be-838c-2e3f2670e061)
Instead of keeping the first value of price_in_cents, for apple_pie, the most recent value in the data file was applied. Why did this behavior happen?

With single-item PUT requests (put_item), you can avoid overwriting duplicate records by including a condition. However, with batch inserts, you have two options for handling duplicate keys. You can either allow the overwrite, or you can cause the entire batch process to fail. 

 

Review the test_batch_put.py script again. Focus on line 12. 
The overwrite_by_pkeys=['product_name'] parameter is included in the batch_writer method. This parameter tells DynamoDB to use last write wins if the key already exists.
Last write wins is why the price_in_cents attribute was updated for apple pie. 
 

However, you know that the café doesn't want the database to add incorrect values. For this dataset, it's better for the load to fail when duplicate product_name values are found instead of allowing the update to add incorrect values. 

ou must change the script so that it fails when duplicates are included in the batch. You can then review and clean up the data. To implement this feature, you remove the overwrite_by_pkeys parameter from the batch_writer method.

8. To prepare for the production data load, go to the browser tab with the DynamoDB console, and delete all records from the table as you did in the previous steps.

 

You can fix the overwrite behavior by updating the test_batch_put.py script and preparing to load the production data. 

In the AWS Cloud9 IDE, open python_3 > test_batch_put.py.
Update line 12 by changing <with table.batch_writer(overwrite_by_pkeys=['product_name']) as batch> to the following and saving the file:
with table.batch_writer() as batch:

9. Now run the script again:
