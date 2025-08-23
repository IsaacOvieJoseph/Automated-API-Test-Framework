# Email Micro-Service API Tests
## 📖 Overview

This project contains automated functional tests for the Email Service API using Newman
, the Postman CLI runner.
The tests validate positive case, negative case, edge cases, and error handling, and can generate detailed HTML reports.
```
📂 Project Structure
email-service-tests/
├── EmailServiceTests.postman_collection.json   # Postman test collection
├── newman/                                     # Newman output reports
│   └── report.html                             # Example generated report
├── package.json                                # Project config & dependencies
└── README.md                                   # Documentation
```

# ⚙️ Setup & Installation
**Clone this repo to local folder**
## 1. Install Node.js & npm

 - Download and install Node.js LTS
 ```sh
    # Windows
    winget install OpenJS.NodeJS.LTS    

    # macOS
    brew install node                   

    # Linux (Debian/Ubuntu)
    sudo apt update                    
    sudo apt install -y nodejs npm
```
 - Verify installation:
``` sh
    node -v
    npm -v
```
## 2. Install Dependencies

Inside the project folder, run:
``` sh
    npm install
```
 This installs:
   - newman → CLI test runner for Postman collections

   - newman-reporter-htmlextra → HTML report generator

 Verify Installation:
 
   Check Newman
     ```sh  npx newman -v```
    
   Check HTML reporter 
    ```sh 
    npx newman run EmailServiceTests.postman_collection.json -r htmlextra
    ```

# ▶️ Running Tests

Instead of typing long Newman commands, you can use npm scripts defined in package.json.

  - Run tests in CLI only
    ```sh
      npm run test
    ```

  - Run tests with HTML report
    ``` sh
      npm run report
    ```
    Generates newman/report.html.

  - Run tests with timestamped HTML reports

    ``` sh
      npm run report:timestamp
    ```
    
    Generates reports like newman/report-20250822154030.html.

       <img width="565" height="640" alt="image" src="https://github.com/user-attachments/assets/e208075f-a3f1-4e95-81d6-c9b8cb24dd8f"/>

    *sample of HTML report*

    

# ⚙️ Adjusting Tests to Your API

You can easily configure the collection to match your own API endpoint and payload.

## Option 1: Change the Base URL in Scripts

Edit **package.json** and replace the **baseUrl** value in the scripts.
Example:

```sh
"scripts": {
  "test": "newman run EmailServiceTests.postman_collection.json --env-var baseUrl=https://api.yourdomain.com"
}
```

Now all requests will hit https://api.yourdomain.com.

## Option 2: Edit the Postman Collection

Open Postman.

Import **EmailServiceTests.postman_collection.json** .

Update the request endpoint to your API (e.g., /api/v1/sendEmail).

Adjust the request body fields if your API requires different keys.
Example:

``` sh
{
  "recipient": "user@example.com", 
  "subject": "Welcome!",
  "content": "Thanks for signing up."
}
```

Export the updated collection and replace the JSON file in this repo.

## Option 3: Use Environment Variables (Best Practice)

Instead of editing scripts, you can pass your API dynamically at runtime:

```sh 
     newman run EmailServiceTests.postman_collection.json --env-var baseUrl=https://staging.yourdomain.com
```

This avoids hardcoding and makes switching between local / staging / production easy.

**NB**

 - If your API uses auth tokens (e.g., Bearer token), add them under Authorization in Postman before exporting.

 - If your API has different error codes, update the test assertions in Postman accordingly.

 - If your payload structure differs (different field names), you must update the request body in the collection.


# 📊 Reports

  After running with npm run report or npm run report:timestamp, open the generated file in a browser:
   ```sh
        open newman/report.html    # Mac
        start newman/report.html   # Windows
        xdg-open newman/report.html # Linux
   ```

  ## The HTML report includes:
   - Test execution summary
   - Pass/Fail breakdown
   - Detailed request/response logs


# 📌 Notes & Assumptions

- The ```simulateQueueFull=true``` query parameter is assumed to exist to test **503** Service Unavailable.

- These tests validate API contract & error handling, not actual email delivery.

- For security/load tests, additional scripts/tools would be required.
