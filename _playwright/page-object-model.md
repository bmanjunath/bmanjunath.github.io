---
layout: page
title: "Page Object Model (POM)"
permalink: /playwright/page-object-model/
---

## Page Object Model (POM) in Playwright

The **Page Object Model (POM)** is a design pattern that helps keep your tests **organized, reusable, and maintainable**.  

Instead of writing all actions directly in tests, you **create classes for each page** that contain the elements and actions.

---

## Why Use POM?

| Benefit | Explanation |
|---------|------------|
| Reusable code | Methods can be used across multiple tests |
| Easy maintenance | Update locators in one place if UI changes |
| Cleaner tests | Tests read like a scenario, not code clutter |
| Scalable | Works well for large projects |

---

## 1️⃣ Without POM (Not Recommended)

```ts
await page.fill('#username', 'admin');
await page.fill('#password', 'password');
await page.click('#login');
await expect(page).toHaveURL('/dashboard');
````

* Hard to maintain
* Locators repeated everywhere
* Test logic mixed with page details

---

## 2️⃣ With POM (Recommended)

### Create a Page Class

**loginPage.ts**

```ts
import { Page, expect } from '@playwright/test';

export class LoginPage {
  constructor(private page: Page) {}

  async goto() {
    await this.page.goto('https://example.com/login');
  }

  async login(username: string, password: string) {
    await this.page.getByLabel('Username').fill(username);
    await this.page.getByLabel('Password').fill(password);
    await this.page.getByRole('button', { name: 'Login' }).click();
  }

  async verifyLoginSuccess() {
    await expect(this.page).toHaveURL('/dashboard');
    await expect(this.page.getByText('Welcome, Admin')).toBeVisible();
  }
}
```

---

### Use the Page Object in Your Test

**login.spec.ts**

```ts
import { test } from '@playwright/test';
import { LoginPage } from './loginPage';

test('Valid login', async ({ page }) => {
  const loginPage = new LoginPage(page);

  await loginPage.goto();
  await loginPage.login('admin', 'password');
  await loginPage.verifyLoginSuccess();
});
```

✅ Clean, readable, and maintainable.

---

## Tips for Using POM

1. **One class per page** → Keep locators and actions together
2. **Reusable methods** → Avoid duplicating code in tests
3. **Keep assertions optional in page class** → Or separate into a `DashboardPage` for more complex flows
4. **Use clear method names** → Makes tests read like plain English

---

## Benefits

* Easy to maintain when UI changes
* Tests are **more readable**
* Locators are centralized, reducing errors
* Scales well for medium/large automation projects

---

## 🎉 Congratulations!

You now have the **core beginner → intermediate Playwright skills**:

* Installed Playwright
* Written your first test
* Used locators and selectors effectively
* Performed user actions
* Added assertions and validations
* Ran tests with the Playwright Test Runner
* Learned how to structure tests using POM

---

## Next Steps

You can now continue to **advanced topics** like:

* Debugging & Tracing
* Generating Reports
* API Testing
* CI/CD Integration

```

