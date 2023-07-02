# How to Store and Retrieve Any Type of File with MuleSoft API
MuleSoft is a powerful platform that allows you to create, integrate, and manage APIs for various applications and services. One of the common challenges that developers face is how to store and retrieve any type of file, such as images, videos, documents, etc., without compromising the quality or integrity of the file.
In this blog post, I will show you how I developed a MuleSoft API that can store and retrieve any type of file using MySql server DB. I will also demonstrate how to test the API using Postman.
# Prerequisites
To follow along with this tutorial, you will need:
Anypoint Studio 7.9 or later
MySql Server account( Register (freesqldatabase.com) )
Postman

# Step 1: Create a MySQL account
Click on MySql Account Registration to create an account.
login to the account.
select the Server Location.
go to Database Details and click on Start, it will generate the credentials.
wait for the DB Status to become Live.

# Step 2: Create a Mule Project
First, we need to create a new Mule project in Anypoint Studio. To do this, go to File > New > Mule Project and give it a name, such as "file-storage-api". Select the Mule runtime version as 4.3.0 or later and click Finish.
# Step 3: Add Dependencies
Next, we need to add some dependencies to our project. These are the modules and connectors that we will use to implement our API logic. To do this, go to the pom.xml file in your project and add the following dependencies:
~~~
<dependencies>
  <dependency>
   <groupId>org.mule.connectors</groupId>
   <artifactId>mule-http-connector</artifactId>
   <version>1.6.0</version>
   <classifier>mule-plugin</classifier>
  </dependency>
  <dependency>
   <groupId>org.mule.connectors</groupId>
   <artifactId>mule-sockets-connector</artifactId>
   <version>1.2.2</version>
   <classifier>mule-plugin</classifier>
  </dependency>
  <dependency>
   <groupId>org.mule.connectors</groupId>
   <artifactId>mule-file-connector</artifactId>
   <version>1.3.4</version>
   <classifier>mule-plugin</classifier>
  </dependency>
  <dependency>
   <groupId>org.mule.connectors</groupId>
   <artifactId>mule-db-connector</artifactId>
   <version>1.11.0</version>
   <classifier>mule-plugin</classifier>
  </dependency>
  <dependency>
   <groupId>mysql</groupId>
   <artifactId>mysql-connector-java</artifactId>
   <version>5.1.48</version>
  </dependency>
 </dependencies>
~~~
Save the file and wait for the dependencies to be downloaded.
# Step 4: Configure the DataBase MySQL Connector
Before we can implement our API logic, we need to configure the DataBase connector that will allow us to interact with the MySQL service. To do this, open the fs-db-filestore-retrive.xml file and go to the Global Elements tab. Click on Create and select Database_Config: MySQL Connection.
In the configuration window, enter the following details:
Host: sql12.freesqldatabase.com
Port: 3306
User: YourUserName
Password: YourPassword
Database: YourDatabaseName

Click OK to save the configuration.
# Step 5: Implement the API Logic
Now, we are ready to implement the API logic. To do this, go to the Message Flow tab and follow these steps:
# POST /postData
This endpoint will upload a file to MySQL and return its metadata as JSON.
Drag an HTTP Listener component from the Mule Palette to the canvas and drop it. This will create an HTTP Listener configuration. Enter the following details:

Name: httpListenerConfig
Host: 0.0.0.0
Port: 8081

Click OK to save the configuration.
2. Double-click on the HTTP Listener component and set the Path to /postData
3. Drag a DataBase component from the Mule Palette to the canvas and drop it in the POST:/postData flow, after the Transform Message component. Double-click on it and set the following properties:
set connector configuration
SQL query test
input params

# GET /getData
This endpoint will upload a file to MySQL and return its metadata as JSON.
Drag an HTTP Listener component from the Mule Palette to the canvas and drop it. This will create an HTTP Listener configuration. Enter the following details:

Name: httpListenerConfig
Host: 0.0.0.0
Port: 8081

Click OK to save the configuration.
2. Drag a DataBase component from the Mule Palette to the canvas and drop it in the POST:/postData flow, after the Transform Message component. Double-click on it and set the following properties:
set connector configuration
SQL query test
input params

3. Drag the file connector to write the file in a specific location. Double-click on it and set the following properties:
set connector configuration
path
content

# Step 6: Test the API
Now, we can test our API using Postman or any other API testing tool. To do this, follow these steps:
Open Postman and create a new request.
Set the method to POST and enter http://localhost:8081/postData as the URL.
In the params tab, add a key-value pair with filePath as the key and a file of your choice as the value.
Click on Send and check that you get a 201 response with a JSON object.
Create another request with GET method and enter http://localhost:8081/getData
Click on Send and check that you get a 200 response with a JSON array containing all your file's metadata.
once you retrieve the data you can verify that your file is stored in the specified path and that the file is not corrupted.

# Project GIT URL : [Store-and-Retrieve-Any-Type-of-File-with-MuleSoft-API](https://github.com/sandy551/Store-and-Retrieve-Any-Type-of-File-with-MuleSoft-API/edit/main/README.md)
Congratulations! You have successfully created a MuleSoft API that can store and retrieve any type of file using Amazon S3. I hope you enjoyed this blog post and learned something new. If you have any questions or feedback, please leave a comment below. Thank you for reading! 😊
