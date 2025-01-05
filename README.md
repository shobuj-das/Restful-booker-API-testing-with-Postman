
# Restful-booker-API-testing-with-Postman

This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API.


##  Features
- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations
## API Documentation
https://documenter.getpostman.com/view/34618466/2sAYBUFDPn
## Technology used:
- Postman
- Newman
## Prerequisite:
- Node Js
- Newman
- Newman Html Report Library
## Installation
1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:
```
https://github.com/shobuj-das/Restful-booker-API-testing-with-Postman.git
```

3. Import the Postman collection:
   - Open Postman.
   - Click on the Import button.
   - Select the file from the repository.

4. Import the Postman environment:
   - In Postman, click on the gear icon in the top right corner.
   - Select Import and choose the file.

5. Newman and Report Installation Process:
   - Newman Install Command:
   ```
    npm install -g newman
    ```
   - Newman Html Report Install Command:
   ```
    npm install -g newman-reporter-htmlextra
   ```

   
## Uses

1. Select Environment:
   - In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
2. Run Collection:
   - Select the imported collection from the Collections sidebar.
   - Click on the Runner button to open the collection runner.
   - Select the desired environment.
   - Click Start Test to run the collection.
3. View Results:
   - Once the tests are complete, view the results in the Runner tab.
   - Detailed test results can be viewed for each request.
## Test Case Scenarios
### 1. Create New Booking

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
#### Pre-request Script:
```
var firstName=pm.variables.replaceIn("{{$randomFirstName}}")

pm.environment.set("firstName", firstName)

var lastName=pm.variables.replaceIn("{{$randomLastName}}")
 
pm.environment.set("lastName", lastName)

var totalPrice = pm.variables.replaceIn("{{$randomInt}}")

pm.environment.set("totalPrice", totalPrice)

var depositPaid=pm.variables.replaceIn("{{$randomBoolean}}")
pm.environment.set("depositPaid", depositPaid)

var moment = require('moment');
var momentObject = moment().subtract(2, 'days');
var formattedMoment = momentObject.format("YYYY-MM-DD");
pm.environment.set("checkinTime", formattedMoment);
);



var moment = require('moment');
var momentObject = moment().add(2, 'days');
var formattedMoment = momentObject.format("YYYY-MM-DD");
pm.environment.set("checkoutTime", formattedMoment);


function generateRandomString(length) {
    var result = '';
    var characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
    var charactersLength = characters.length;
    for (var i = 0; i < length; i++) {
        result += characters.charAt(Math.floor(Math.random() * charactersLength));
    }
    return result;
}

var randomString = generateRandomString(10);

pm.environment.set("additionalNeeds", randomString);
```

#### Request body:
```
{
	"firstname" : "{{firstName}}",
	"lastname" : "{{lastName}}",
	"totalprice" : {{totalPrice}},
	"depositpaid" : {{depositPaid}},
	"bookingdates" : {
    	"checkin" : "{{checkinTime}}",
    	"checkout" : "{{checkoutTime}}"
	},
	"additionalneeds" : "{{additionalNeeds}}"
}
```
#### Response body:
```
{
    "bookingid": 3094,
    "booking": {
        "firstname": "Abner",
        "lastname": "MacGyver",
        "totalprice": 616,
        "depositpaid": false,
        "bookingdates": {
            "checkin": "2025-01-04",
            "checkout": "2025-01-08"
        },
        "additionalneeds": "1WRVuRkXug"
    }
}
```

### 2. Get Booking Details By ID
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
#### Response Body:
```
{
    "firstname": "Abner",
    "lastname": "MacGyver",
    "totalprice": 616,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2025-01-04",
        "checkout": "2025-01-08"
    },
    "additionalneeds": "1WRVuRkXug"
}
```
### 3. Create A Token For Authentication.
### Request URL: https://restful-booker.herokuapp.com/auth
### Request Method: POST
#### Pre-request Script: None
#### Request Body:
```
{
	"username": "admin",
	"password": "password123"
}
```
#### Response body:
```
{
    "token": "7cdfae3cfc252bc"
}
```
### 4. Update the Booking Details
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
#### Pre-request Script:
```
var updated_first_name = pm.variables.replaceIn("{{$randomFirstName}}");
pm.environment.set("updated_firstName", updated_first_name);
var updated_price = pm.variables.replaceIn("{{$randomInt}}");
pm.environment.set("updated_price", updated_price);

```
#### Request body:
```
{
    "firstname": "{{updated_firstName}}",
    "lastname": "Heaney",
    "totalprice": {{updated_price}},
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2024-05-03",
        "checkout": "2024-05-07"
    },
    "additionalneeds": "EKt3rztwbD"
}
```
#### Response body:
```
{
    "firstname": "Johnnie",
    "lastname": "Heaney",
    "totalprice": 952,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2024-05-03",
        "checkout": "2024-05-07"
    },
    "additionalneeds": "EKt3rztwbD"
}
```

### 5. Delete Booking Record
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: DELETE
#### Response Body: None

## Run Command:
- ### Run Command for Console:
```
newman run Shobuj-Das_Rest-booking-API.postman_collection.json -e Shobuj-Das_Rest-booking-API.postman_environment.json
```
- ### Run Command for Report:
```
newman run Shobuj-Das_Rest-booking-API.postman_collection.json -e Shobuj-Das_Rest-booking-API.postman_environment.json -r cli, htmlextra
```

## Newman Report Summary:

![image](https://github.com/user-attachments/assets/fc24c39f-f6fe-40f3-9c75-57a7eceb76c8)
![image](https://github.com/user-attachments/assets/9e0f5868-14ae-4a44-8639-ae4bdeaecd4e)
![image](https://github.com/user-attachments/assets/b86a7074-f35a-48ef-8330-24da81edea27)
![image](https://github.com/user-attachments/assets/d5b0b3fa-012a-408b-b858-4cab3cceb9f5)


