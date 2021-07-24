Relevel OLX Clone – Java Spring Boot
 
Problem Statement:
Relevel is planning to build an e-commerce app like OLX to sell old stuffs.You have to design & build the backend for this application. It should have the ability for the users to list an item, search an item , delete an item , add an item to its favourite list etc.
Your task is to go through below templates/stories and create this OLX clone app.
The tech stack required is Java and Spring Boot. Preferred IDE is Intellij/Eclipse to import the project directly. Postman tool to test the REST APIs. Make sure maven and .m2 etc are configured on local.
 How to Set up the Application:
To get ready with building the application a basic or boilerplate template code is provided below.
Template Repo Link: https://github.com/RelevelBackendTest/olx_clone
Git clone the project from the above location to your local system and import it to any one of the IDE to get started.
 Once you clone the application, then run the main class of the application  as a Java Application. The default port is set to 8080 for this application , and there is a sample endpoint to test the setup is complete. Open the sample URL localhost:8080/ping in the browser to see a message “Ping is Successful” . This ensures the setup is complete.
 Database Set Up :
The application is configured with an in-memory H2 Database .Dependency for the database is already added in the pom.xml file. You can access the console of the H2 database using the following link.
URL for H2 Database: localhost:8080/h2-console
Username : sa
Password : password
Note : You can create tables for your problem statements using this database.
 
Problem Breakdown:
Template-1: Listing/Delisting of user’s Item
1.Story-1: Listing an item in the portal(~45min)
 As a user I should be able to list one of the items in the portal which I plan to sell .The task is to create an endpoint localhost:8080/item to create an Ad for selling the item.
1.      Choose appropriate HTTP methods (GET,POST,PUT,DELETE) to hit this URL.
2.      The user needs to provide the details of the item like (e.g Item Name e.g. TV,Fridge,AC,Cooler,Bike,Car etc , Description of the item,Max Price for the item, Location of the item(e.g. Bangalore,Hyderabad,Mumbai etc),Brand of the Item , Purchase Year,Negotiable, Item Ad Posting Date)
3.      Basic validation on the attributes of the item needs to be performed with following rules :
Item Name should contain characters between 1-30 chars
Description should be containing 2-100 chars max
Max price should be float number from 1.00 to 9999999.00 max
Location should be in range of 2-15  only chars, without number
Brand of Item should be 1-15 char 
Purchase Year should be valid number from 1950-2021
Negotiable should be either Yes or No
Item AdPosting Date  should be same as the current date
4.      In case a user provides wrong input , they should get a message saying “Invalid Input by user” with appropriate HTTP status.
5.      In case the user provides the right set of inputs, the data should get stored in the database with an unique itemID, and the user should get a response with message “Item Ad created Successfully” with appropriate HTTP status.
 
2.Story-2: Retrieving the details of an item posted by the user (~20min)
 As a user I should be able to retrieve the item posted  by a user
      The task is to create an endpoint localhost:8080/item/{itemId} to retrieve the details of the item.
1.      Choose appropriate HTTP methods (GET,POST,PUT,DELETE) to hit this URL.
2.      The user needs to provide the itemID in the URL to search for the item details
3.      In case the user provides an itemID which does not exist then they should get a response “Item ID does not exist” with appropriate HTTP status.
4.      In case the user provides a correct itemID they should get details of the Item (Item  Description,Price,Location,Brand ,Purchase Year, Item Ad Posting Date etc). with appropriate HTTP status. 
3. Story-3 : Deleting an Item posted by User (~30 min)
The task is to create an endpoint localhost:8080/item/{itemId} to delete  an item posted by the user.
1.      Choose appropriate HTTP methods (GET,POST,PUT,DELETE) to hit this URL.
2.      The user needs to provide the ItemID in the URL to delete an item posted by the user.
3.      In case the Item ID does not exist, the user should get a response “Item does not exist” with appropriate HTTP status.
4.      In case ItemID exists in the database , delete the Item from the database and send a response “Item Deleted Successfully” with appropriate HTTP status.
 

Template -2: Adding User and its related functionality
1.      Story -1 (~30 min): Create a User
      The task is to create an endpoint localhost:8080/user so that we can create a user
 Choose appropriate HTTP methods(GET,POST,PUT,DELETE) to hit this URL.
The user should provide details like Name, Password, Phone Number, Email ID, Age, Gender.
 Validate the user input using following rules .
1.      Name – Max 20 Chars without any special character except space
2.      Password – Max 10 chars with alphanumeric string
3.      Phone Number : Should be exactly 10 digit
4.      Email ID : Valid Email Id format e.g. relevel.com is not valid where as relevel@gmail.com is valid
5.      Age should be between 10 -99 years max
6.      Gender should be male or female.
Create an appropriate table to store these details of the user.
Upon successful creation of the user return appropriateHTTP status as 201 with a message “User Created Successfully”.
If a user has provided wrong input , provide appropriate HTTP status with a message “User inputs are valid” .


2.      Story -2 (~30 min): Login for the User
      The task is to create an endpoint localhost:8080/login so that we can verify if user credentials are valid .
Choose appropriate HTTP methods(GET,POST,PUT,DELETE) to hit this URL.
The user needs to provide email address as username and password to verify if the user credentials are correct
Authenticate the value against the data stored in the database and upon successful authentication return appropriate HTTP status.
In case the user has provided a wrong password , return a HTTP status as 401 with a message as “Invalid Password”.
If the user name provided by the user doesn’t exist return a HTTP status as 404 with message “User does not exist”

3.      Story-3 (~ 30 min): Retrieve the Details of the user
The task is to create an endpoint localhost:8080/user/{userid}  to fetch the user details
 Choose appropriate HTTP methods (GET,POST,PUT,DELETE) to hit this URL.
The user needs to provide the ID of the user to get user details as  response.
 In case a user provides an ID which does not correspond to any user , they should see a HTTP 404 status with “No users for the given ID” as the response message.
 In case of Success , the user should see details of the user with appropriate HTTP status
 
 




Template: 3 : Search and Adding item Functionality for the user
 
Story-1: Flexible search by different fields (~60 min)
The task is to create an endpoint localhost:8080/search so that a user can search for a particular item to buy.
 Choose appropriate HTTP methods (GET,POST,PUT,DELETE) to hit this URL.
User needs to provide the input as a request body consisting of fields and their values as the payload to the request.
E.g.{
    {
     "item_name":"TV",
    "description":"6 months old TV with light usage",
     "price_upper_range":15000.00,
     "price_lower_range":10000.00,
     "location":"Bangalore",
     "brand":"Samsung",
     “negotiable”:true,
     "purchase_year":2021
    }

It should be optional for the user to omit any of the mentioned fields while the search functionality still should be able to work , e.g. If the user provides only brand as “Samsung” , we should get a response which consists of all samsung items .
In case of user provides wrong payload , they should get a message “Bad Request by User” wit appropriate HTTP status
In case user provides correct input , they should get a list of items with appropriate HTTP response.

Story-2 : Adding an item to favourite list (~45 min)
The task is to create an endpoint localhost:8080/favourite/{userId}/{itemId} so that a user can add an item to his/her favourite list
 Choose appropriate HTTP methods (GET,POST,PUT,DELETE) to hit this URL.
 The user should provide its User ID and the ItemID to this endpoint and should be able to add the item to his favourite list by storing the association between userID and itemID  in the database.
In case the user ID or Item ID do not exist  ,we should get a response “User ID or the ItemID are not valid ” with appropriate HTTP status
 In case of correct input by the user , the user should be able to add the item to his/her favourite list by storing into DB with a message “Item added to favourite list successfully” with appropriate HTTP response . 


Story -3 : Removing all Items from Favourite list of  a user(~30 min)
The task is to create an endpoint localhost:8080/favourite/{userId} so that a user can remove all items from his/her favourite list.
 Choose appropriate HTTP methods (GET,POST,PUT,DELETE) to hit this URL.
 The user should provide its User ID to delete all items under its favourite list.
In case the user ID does not exist,we should get a response “User ID is not valid ” with appropriate HTTP status. In case user UserID is correct but it does not contain any favourite items in its list , it should return a message “Empty Favourite List” with appropriate HTTP status.
 In case of correct input by the user , the user should be able to delete all items from its favourite list , and the association from the database should also be deleted .  Upon successful deletion of the favourite list , the user should get a message “Delete all items from favourite list” with appropriate HTTP status.
 


