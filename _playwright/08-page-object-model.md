---

layout: default
title: "Page Object Model (POM)"
permalink: /playwright/08-page-object-model/
---

# Page Object Model (POM) in Playwright

The **Page Object Model (POM)** is a design pattern used in test automation to make tests **organized, reusable, and maintainable**.

Instead of writing all interactions directly in test files, we **create classes that represent web pages**. These classes contain:

* Page locators
* Page actions
* Page validations

This approach separates **test logic from UI interaction logic**, making the framework easier to maintain.

---

# Why Use POM?

| Benefit          | Explanation                                  |
| ---------------- | -------------------------------------------- |
| Reusable code    | Page methods can be reused across many tests |
| Easy maintenance | UI changes require updates in only one place |
| Cleaner tests    | Tests read like real user scenarios          |
| Scalable         | Works well for medium and large projects     |

---

# 1️⃣ Without Page Object Model (Not Recommended)

Example test written without POM:

```ts
await page.fill('#username', 'admin');
await page.fill('#password', 'password');
await page.click('#login');
await expect(page).toHaveURL('/dashboard');
```

Problems:

* Locators repeated across tests
* Hard to maintain when UI changes
* Tests become cluttered and difficult to read

---

# 2️⃣ With Page Object Model (Recommended)

With POM, we move page logic into **separate classes**.

---

# Example Project Structure

A typical Playwright POM project structure:

```
tests/
   login.spec.ts

pages/
   loginPage.ts
   dashboardPage.ts

utils/
   test-data.ts
```

This structure keeps tests **clean and scalable**.

---

# Step 1: Create a Page Class

Create a page class that represents the login page.

### loginPage.ts

```ts
import { Page } from '@playwright/test';

export class LoginPage {

  readonly page: Page;

  constructor(page: Page) {
    this.page = page;
  }

  async goto() {
    await this.page.goto('https://example.com/login');
  }

  async enterUsername(username: string) {
    await this.page.getByLabel('Username').fill(username);
  }

  async enterPassword(password: string) {
    await this.page.getByLabel('Password').fill(password);
  }

  async clickLogin() {
    await this.page.getByRole('button', { name: 'Login' }).click();
  }

  async login(username: string, password: string) {
    await this.enterUsername(username);
    await this.enterPassword(password);
    await this.clickLogin();
  }
}
```

This class contains all actions related to the **Login page**.

---

# Step 2: Create Another Page Object

Example dashboard page.

### dashboardPage.ts

```ts
import { Page, expect } from '@playwright/test';

export class DashboardPage {

  readonly page: Page;

  constructor(page: Page) {
    this.page = page;
  }

  async verifyDashboardLoaded() {
    await expect(this.page).toHaveURL('/dashboard');
  }

  async verifyWelcomeMessage() {
    await expect(this.page.getByText('Welcome, Admin')).toBeVisible();
  }

}
```

This class contains validations related to the **Dashboard page**.

---

# Step 3: Use Page Objects in Test

### login.spec.ts

```ts
import { test } from '@playwright/test';
import { LoginPage } from '../pages/loginPage';
import { DashboardPage } from '../pages/dashboardPage';

test('Valid login', async ({ page }) => {

  const loginPage = new LoginPage(page);
  const dashboardPage = new DashboardPage(page);

  await loginPage.goto();

  await loginPage.login('admin', 'password');

  await dashboardPage.verifyDashboardLoaded();

  await dashboardPage.verifyWelcomeMessage();

});
```

Now the test reads like a **real user scenario**.

---

# Best Practices for Page Object Model

Follow these practices for maintainable automation frameworks.

### 1. One Class Per Page

Each web page should have its own class.

Example:

* `LoginPage`
* `DashboardPage`
* `CartPage`
* `CheckoutPage`

---

### 2. Keep Locators Inside Page Objects

Avoid putting locators inside test files.

Example:

```ts
await this.page.getByRole('button', { name: 'Login' }).click();
```

This keeps tests clean.

---

### 3. Reuse Page Methods

Example reusable methods:

* `login()`
* `addProductToCart()`
* `checkoutOrder()`

This reduces duplicate code.

---

### 4. Keep Tests Simple

Tests should describe **business flows**, not implementation details.

Example:

```ts
await loginPage.login('admin', 'password');
await dashboardPage.verifyDashboardLoaded();
```

---

# Advantages of POM

Using POM provides several advantages:

* Centralized locator management
* Reduced code duplication
* Easy maintenance when UI changes
* Improved readability of tests
* Better scalability for large automation projects

---

# Example: End-to-End Login Flow

```ts
await loginPage.goto();

await loginPage.login('admin', 'password');

await dashboardPage.verifyDashboardLoaded();

await dashboardPage.verifyWelcomeMessage();
```

This structure keeps automation tests **clean, modular, and easy to maintain**.

---

# Summary

The **Page Object Model** is a widely used design pattern in test automation.

It helps create **structured and maintainable test frameworks** by separating:

* Page interactions
* Test logic
* Assertions

Using POM in Playwright ensures your tests remain **scalable and easy to maintain** as the application grows.

---

# Next Steps

Now that you understand POM, you can explore advanced topics such as:

* Debugging & Tracing
* Generating Test Reports
* API Testing with Playwright
* CI/CD Integration

---
