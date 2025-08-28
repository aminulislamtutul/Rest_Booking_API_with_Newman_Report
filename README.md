# **Rest Booking API Testing with Postman Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API.
### **Feature**
- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations
## API Documentation
- https://documenter.getpostman.com/view/46763324/2sB34oDdmD
### **Technology Used**
- Postman
- Newman
### **Prerequisite**
- Node.js
- Newman
- Newman html Report Library
### **Installation**
1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:
 ```console 
  git clone https://github.com/aminulislamtutul/API_Tasting_Store_Management_System_With_Newman_Report.git
```
3. Import the Postman collection:
    - Open Postman.
    - Click on the Import button.
    - Select the file from the repository.
4. Import the Postman environment:
    - In Postman, click on the gear icon in the top right corner.
    - Select **Import** and choose the file.
5. Newman and Report Installation Process:
    - Newman Install Command:
     ```console 
      npm install -g newman
    ```
    - Newman html Report Install Command:
     ```console 
      npm install -g newman-reporter-htmlextra
    ```
### **Usage**
1. Select Environment:
    -   In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
2. Run Collection:
    -   Select the imported collection from the Collections sidebar.
    -   Click on the Runner button to open the collection runner.
    -   Select the desired environment.
    -   Click Start Test to run the collection.
3. View Results:
    -   Once the tests are complete, view the results in the Runner tab.
    -   Detailed test results can be viewed for each request.
## **Testing**

## Test Case Scenarios:

## _**1. Create New Booking**_
### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
### Pre-request Script:
```console 
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
pm.environment.set("First Name", firstName)

var lastName = pm.variables.replaceIn("{{$randomLastName}}")
pm.environment.set("Last Name", lastName)

var totolPrice = pm.variables.replaceIn("{{$randomInt}}")
pm.environment.set("Total Price", totolPrice )

var depositePaid = pm.variables.replaceIn("{{$randomBoolean}}")
pm.environment.set("Deposite Paid", depositePaid )

//Date
const moment = require('moment')
const today = moment()

var checkIn = today.add(5,'d').format("YYYY-MM-DD")
pm.environment.set("Check In", checkIn)

var checkOut = today.add(3,'d').format("YYYY-MM-DD")
pm.environment.set("Check Out", checkOut)
```
  **Request Body:** 
 ```console 
{
	"firstname" : "{{First Name}}",
	"lastname" : "{{Last Name}}",
	"totalprice" : {{Total Price}},
	"depositpaid" : {{Deposite Paid}},
	"bookingdates" : {
    	"checkin" : "{{Check In}}",
    	"checkout" : "{{Check Out}}"
	},
	"additionalneeds" : "Breakfast"
}
```
  **Response Body:**
```console
{
    "bookingid": 3598,
    "booking": {
        "firstname": "Isac",
        "lastname": "Brekke",
        "totalprice": 213,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2025-07-31",
            "checkout": "2025-08-03"
        },
        "additionalneeds": "Breakfast"
    }
}
```
## _**2. Get Booking Details By ID**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Response Body:
```console
{
    "firstname": "Emmie",
    "lastname": "Wiegand",
    "totalprice": 840,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2025-07-31",
        "checkout": "2025-08-03"
    },
    "additionalneeds": "Breakfast"
}
```
## _**3. Create A Token For Authentication.**_
### Request URL: https://restful-booker.herokuapp.com/auth
### Request Method: POST
### Pre-request Script: None
### Request Body:
 ```console 
{
    "username": "admin",
    "password": "password123"
}
```
 **Response Body:**
 ```console 
{
    "token": "06eb798bf6f2caa"
}
```
 ## _**4. Update the Booking Details**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
### Pre-request Script:
```console 
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
pm.environment.set("First Name", firstName)

//console.log(firstName)

var lastName = pm.variables.replaceIn("{{$randomLastName}}")
pm.environment.set("Last Name", lastName)

var totolPrice = pm.variables.replaceIn("{{$randomInt}}")
pm.environment.set("Total Price", totolPrice )

var depositePaid = pm.variables.replaceIn("{{$randomBoolean}}")
pm.environment.set("Deposite Paid", depositePaid )

//Date
const moment = require('moment')
const today = moment()

var checkIn = today.add(5,'d').format("YYYY-MM-DD")
pm.environment.set("Check In", checkIn)

var checkOut = today.add(3,'d').format("YYYY-MM-DD")
pm.environment.set("Check Out", checkOut)
```
  **Request Body:** 
 ```console 
{
	"firstname" : "{{First Name}}",
	"lastname" : "{{Last Name}}",
	"totalprice" : {{Total Price}},
	"depositpaid" : {{Deposite Paid}},
	"bookingdates" : {
    	"checkin" : "{{Check In}}",
    	"checkout" : "{{Check Out}}"
	},
	"additionalneeds" : "Breakfast"
}
```
  **Response Body:**
```console
{
    "firstname": "Jude",
    "lastname": "Jacobi",
    "totalprice": 936,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2025-07-31",
        "checkout": "2025-08-03"
    },
    "additionalneeds": "Breakfast"
}
```
 ## _**5. Delete Booking Record**_

### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: DELETE
### Response Body: None 
## Run Command:  
- Run Command for Console:
```console
newman run Aminul_Islam.postman_collection.postman_collection.json -e Aminul_Islam.postman_Enviroment.postman_environment.json
```
- Run Command for Report: 
```console
newman run Aminul_Islam.postman_collection.postman_collection.json -e Aminul_Islam.postman_Enviroment.postman_environment.json -r cli,htmlextra
```
## Newman Report Summary:

<img width="662" height="413" alt="Screenshot 2025-07-27 010757" src="https://github.com/user-attachments/assets/7480913b-9263-4294-8cd5-3b3871b989fa" />
<img width="662" height="382" alt="Screenshot 2025-07-27 010555" src="https://github.com/user-attachments/assets/a832e2e2-f875-4c9e-b92c-fdd43eada298" />
<img width="662" height="206" alt="Screenshot 2025-07-27 010651" src="https://github.com/user-attachments/assets/cc70cdb4-ab21-47ab-a524-2045d339ec9f" />
<img width="662" height="206" alt="Screenshot 2025-07-27 010708" src="https://github.com/user-attachments/assets/961ec449-9eb8-4beb-b7ea-d8c57a3d8fce" />







