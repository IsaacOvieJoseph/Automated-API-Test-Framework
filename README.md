# 📖 Email Micro-Service API Tests
##📌 Overview

This project contains automated functional tests for the Email Service API using Newman
, the Postman CLI runner.
The tests validate normal cases, edge cases, and error handling, and can generate detailed HTML reports.

📂 Project Structure
email-service-tests/
├── EmailServiceTests.postman_collection.json   # Postman test collection
├── newman/                                     # Newman output reports
│   └── report.html                             # Example generated report
├── package.json                                # Project config & dependencies
└── README.md                                   # Documentation

# ⚙️ Setup & Installation
## 1. Install Node.js & npm

 -- Download and install Node.js LTS

 -- Verify installation:
``` sh
    node -v
    pm -v
```
## 2. Install Dependencies

Inside the project folder, run:
``` sh
    npm install
```

 This installs:

  -- newman → CLI test runner for Postman collections

  -- newman-reporter-htmlextra → HTML report generator

  Verify Installation

    Check Newman:
      ``` sh
        npx newman -v
      ```

    Check HTML reporter:
    ``` sh
        npx newman run EmailServiceTests.postman_collection.json -r htmlextra
    ```

# ▶️ Running Tests

Instead of typing long Newman commands, you can use npm scripts defined in package.json.

  ## Run tests in CLI only
    ``` sh
      npm run test
    ```

  ## Run tests with HTML report
    ``` sh
      npm run report
    ```
    Generates newman/report.html.

  ## Run tests with timestamped HTML reports
    ``` sh
      npm run report:timestamp
    ```
    Generates reports like newman/report-20250822154030.html.

# 🛠 Adjusting for Your API

  By default, the collection points to a placeholder API.
  ## To test your own API:
    -- Open EmailServiceTests.postman_collection.json.
    -- Find the request URL, e.g.:

        "url": "http://localhost:3000/api/send-email"

    -- Replace it with your own API’s base URL and endpoint.
    -- Save the file.
    -- Now rerun the tests with npm run report.

# 📊 Reports

  After running with npm run report or npm run report:timestamp, open the generated file in a browser:
      ``` sh
        open newman/report.html    # Mac

        start newman/report.html   # Windows

        xdg-open newman/report.html # Linux
      ```

  ## The HTML report includes:
    -- Test execution summary
    -- Pass/Fail breakdown
    -- Detailed request/response logs
