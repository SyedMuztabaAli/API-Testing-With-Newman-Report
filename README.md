### **Rest Booking API Testing with Postman Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

### **Technology used:**
- Postman
- Newman

### **Prerequisite:**
- Node Js
- Newman
- Newman Html Report Library

## **Testing**

## Test Case Scenarios:

## _**1. Create New Booking**_

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
### Pre-request Script:
```console 
    //FirstName
	var firstName = pm.variables.replaceIn("{{$randomFirstName}}");
	console.log(firstName);
	pm.environment.set("firstName",firstName)
	
	//LastName
	var lastName = pm.variables.replaceIn("{{$randomLastName}}");
	pm.environment.set("lastName",lastName);
	
	//TotalPrice
	var totalPrice = pm.variables.replaceIn(Math.floor(Math.random() *9000))
	pm.environment.set("totalPrice",totalPrice);
	
	//DepositPaid
	var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}");
	pm.environment.set("depositPaid",depositPaid);
	console.log(depositPaid);

	//Date
	const moment  = require('moment');
	const today = moment();
	var checkin = today.add(1,'d').add(2,'M').format("YYYY-MM-DD")
	console.log(checkin);
	pm.environment.set("checkin",checkin);
	
	var checkout = today.add(3,'d').format("YYYY-MM-DD")
	pm.environment.set("checkout",checkout);

	//Additional Needs
	var additionalNeeds = pm.variables.replaceIn("{{$randomProduct}}")
	pm.environment.set("additionalneeds",additionalNeeds);
```
  **Request Body:** 
 ```console 
  {
     "firstname" : "{{firstName}}",
     "lastname" : "{{lastName}}",
     "totalprice" : {{totalPrice}},
     "depositpaid" : {{depositPaid}},
     "bookingdates" : {
         "checkin" : "{{checkin}}",
         "checkout" : "{{checkout}}"
     },
     "additionalneeds" : "{{additionalneeds}}"
 }
```
  **Response Body:**
 ```console 
  {
      "bookingid": 4334,
      "booking": {
          "firstname": "Joelle",
          "lastname": "Krajcik",
          "totalprice": 266,
          "depositpaid": true,
          "bookingdates": {
              "checkin": "2024-03-15",
              "checkout": "2024-03-20"
          },
          "additionalneeds": "monitor"
      }
  }
```
