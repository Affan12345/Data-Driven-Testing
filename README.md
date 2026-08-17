# Data-Driven API Testing with Postman & Newman

## 📝 Project Summary

This project demonstrates **Data-Driven API Automation Testing** for the open-source **Restful Booker API** (`https://restful-booker.herokuapp.com`) using Postman and Newman. 

The test suite validates the endpoint `POST /booking` across multiple test datasets stored in an external CSV file (`booking_test_data1.csv`)[cite: 1, 2]. During each iteration, Postman's **Pre-request Script** dynamically extracts iteration data (`pm.iterationData`) and sets environment variables. The request payload dynamically sends these values to the API, and the **Test Script** executes assertions to verify status codes, response data types, and payload field accuracy against expected values.

During test execution, 5 iterations were completed with 45 test assertions executed (9 assertions per iteration) with a **100% pass rate**.

---

## 📌 Features

- **Data-Driven Testing:** Automated test execution across multiple data records using an external CSV dataset.
- **Pre-Request Dynamic Assignment:** Captures values per iteration and assigns them directly to environment variables (`fName`, `lName`, `tPrice`, `dPaid`, `cinDate`, `coutDate`, `aNeeds`).
- **Comprehensive Assertions:** Validates HTTP `200 OK` status, JSON response structure, dynamic field assertions, and captures `booking_id` for downstream requests.

---

## 🖼️ Postman Implementation & Screenshots

### 1. Request Body Setup
Uses dynamic environment variables in JSON raw body payload format:
`POST {{base_url}}/booking`

```json
{
    "firstname": "{{fName}}",
    "lastname": "{{lName}}",
    "totalprice": {{tPrice}},
    "depositpaid": {{dPaid}},
    "bookingdates": {
        "checkin": "{{cinDate}}",
        "checkout": "{{coutDate}}"


```json


    },
    "additionalneeds": "{{aNeeds}}"
}

```

### 2. Environment Variables Configuration
Configured environment variables for variable scoping, base URL management, authentication tokens, and dynamic value assignments.

### 3. Collection Runner Execution Results
Executed 5 iterations using the CSV test data file.

Total Tests Passed: 45 / 45

Failed / Skipped: 0

Average Response Time: ~289 ms

### 📁 Repository Structure
.
├── Data Driven Testing.postman_collection.json   
├── Data Driven Test.postman_environment.json    
├── booking_test_data1.csv                       
└──                                   
└── README.md                                 

### 📁 Getting Started

Prerequisites
Download and install Postman.

Install Node.js and Newman CLI (for command-line execution):

npm install -g newman

### 🛠️ How to Run
Option 1: Running in Postman Collection Runner
Import Data Driven Testing.postman_collection.json and Data Driven Test.postman_environment.json into Postman.

Select the Data Driven Test environment.

Right-click the Data Driven Testing collection and click Run collection.

Upload booking_test_data1.csv in the Data section.

Click Run Data Driven Testing.

Option 2: Running via Newman CLI
To run the automated suite via terminal:

newman run "Data Driven Testing.postman_collection.json" \
  -e "Data Driven Test.postman_environment.json" \
  -d "booking_test_data1.csv" \
  -r cli,html

 ### 🧪 Assertions Executed Per Iteration

| Test Assertion | Purpose | Status |
| :--- | :--- | :--- |
| Status code is 200 | Verifies the response returns HTTP status code 200 OK. | PASS |
| Response data format is JSON | Asserts that response body is in JSON format. | PASS |
| First name match | Verifies response.booking.firstname matches fName. | PASS |
| Last name match | Verifies response.booking.lastname matches lName. | PASS |
| Total price match | Verifies response.booking.totalprice matches tPrice. | PASS |
| Deposit paid match | Verifies response.booking.depositpaid matches dPaid. | PASS |
| Check-in date match | Verifies response.booking.bookingdates.checkin matches cinDate. | PASS |
| Check-out date match | Verifies response.booking.bookingdates.checkout matches coutDate. | PASS |
| Additional needs match | Verifies response.booking.additionalneeds matches aNeeds. | PASS |

### 📜 API Reference
API Base URL: https://restful-booker.herokuapp.com

Documentation: Restful Booker API Docs

