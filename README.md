# Playwright Restaurant Automation Framework

This document provides a comprehensive guide to setting up, running, and understanding the Playwright-based automation testing project for restaurant-related workflows.

## Project Overview

This automation framework is designed to test workflows such as user login, managing customers, managing restaurant admins, handling coupons, events, vouchers, and restaurant-specific features. It utilizes the following technologies:

- **Playwright**: For browser automation.
- **dotenv**: For managing environment variables.
- **Utility Scripts**: For reusable functions and constants.

---

## Project Structure

```
├── .github/                   # GitHub configuration files (for CI/CD workflows)
├── node_modules/              # Installed dependencies
├── tests/                     # Test scripts directory
│   ├── 1_login.spec.js         # Login functionality test
│   ├── 2_manageCustomer.spec.js # Manage customer functionality test
│   ├── 3_manageRestaurantAdmin.spec.js # Manage restaurant admin functionality test
│   ├── 4_restaurant.spec.js    # Restaurant module tests
│   ├── 5_coupon.spec.js        # Coupon module tests
│   ├── 6_event.spec.js         # Event module tests
│   ├── 7_manageVoucher.spec.js # Voucher management tests
│   └── example.spec.js         # Example test script
├── tests-examples/            # Example test scripts
├── utils/                     # Utility scripts
│   ├── constant.js             # Constants used across tests
│   └── helpers.js              # Helper functions used across tests
├── .env                       # Environment variables file (needs to be created)
├── .gitignore                 # Git ignore file
├── 10MB_Image.jpg             # Sample image for testing
├── Coupon.png                 # Sample coupon image for testing
├── Dummy_PDF.pdf              # Dummy PDF file for testing
├── event_banner.jpg           # Event banner image for testing
├── image.jiff                 # Sample JIFF image for testing
├── package-lock.json          # Lockfile for dependencies
├── package.json               # Project dependencies and npm scripts
├── pexels_10MB.jpg            # Another sample image for testing
├── playwright.config.js       # Playwright configuration file
├── Restaurant_Banner.png      # Restaurant banner sample
├── Restaurant_Logo.jpg        # Restaurant logo sample
└── voucher_book_click_error.png # Error screenshot example
```

---

## 1. Prerequisites

Ensure the following tools are installed on your machine:

- **Node.js**: Download from [Node.js Official Website](https://nodejs.org/).
- **npm**: Installed automatically with Node.js.

---

## 2. Project Setup

### Step 1: Clone the Repository

Clone the project repository or download the project folder. Navigate to the project directory via terminal:

```bash
cd path/to/your-project
```

### Step 2: Install Dependencies

Run the following command to install the required dependencies:

```bash
npm install
```

If specific dependencies are missing, install them manually:

- **Playwright**: `npm init playwright@latest`
- **dotenv**: `npm install dotenv`

---

## 3. Set Up Environment Variables

Create a `.env` file in the root directory to store sensitive data like URLs and credentials. Example:

```
BASE_URL=https://example.com
USERNAME=testuser
PASSWORD=testpassword
```

To use these variables in tests:

```javascript
require('dotenv').config();
const baseUrl = process.env.BASE_URL;
const username = process.env.USERNAME;
```

---

## 4. Running Tests

### Run All Tests:

```bash
npx playwright test
```

### Run a Specific Test File:

For example, to run the login test:

```bash
npx playwright test tests/1_login.spec.js
```

### Run in Headed Mode:

By default, Playwright runs in headless mode. To see the browser:

```bash
npx playwright test --headed
```

---

## 5. Viewing Reports

After running tests, Playwright generates an HTML report. To view it:

```bash
npx playwright show-report
```

---

## 6. Test Artifacts

- **Screenshots**: Automatically captured for failed tests, stored in the `Screenshots/` folder.
- **Reports**: Test results are saved in the `playwright-report/` folder.
- **Videos**: If enabled, video recordings of test executions are stored in the `videos/` folder.

---

## 7. Example Test Script

Below is an example test script for logging into the application:

```javascript
const { test, expect } = require('@playwright/test');
require('dotenv').config();

test('Login Test', async ({ page }) => {
  await page.goto(process.env.BASE_URL);
  await page.fill('#username', process.env.USERNAME);
  await page.fill('#password', process.env.PASSWORD);
  await page.click('#login');

  // Verify successful login
  await expect(page).toHaveURL('/dashboard');
});
```

---

## 8. Utilities

Reusable functions and constants are stored in the `utils/` directory. Example helper function:

```javascript
module.exports = {
  login: async function (page, username, password) {
    await page.fill('#username', username);
    await page.fill('#password', password);
    await page.click('#login');
  },
};
```

Usage in tests:

```javascript
const { login } = require('../utils/helpers');

test('Login Test', async ({ page }) => {
  await page.goto(process.env.BASE_URL);
  await login(page, process.env.USERNAME, process.env.PASSWORD);
});
```

---

## 9. Troubleshooting

- **Missing `.env` File**: Ensure the file exists at the project root with all required environment variables.
- **Dependencies Not Installed**: Run `npm install` to resolve missing packages.
- **Playwright Not Installed**: Run `npm init playwright@latest`.

---

This completes the setup and usage guide for the Playwright Restaurant Automation Framework. For additional support, refer to the Playwright [documentation](https://playwright.dev/docs/intro).

