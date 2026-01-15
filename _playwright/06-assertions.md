---
layout: page
title: "Assertions & Validations"
permalink: /playwright/06-assertions/

---

## Assertions & Validations in Playwright

Assertions are how we **verify that our application behaves as expected**.  
They are the backbone of automated testing.

Playwright has a built-in `expect` function that makes assertions **easy and reliable**.

---

## 1️⃣ Check Page Title

Verify the page title to ensure you are on the correct page:

```ts
import { test, expect } from '@playwright/test';

test('Verify Google title', async ({ page }) => {
  await page.goto('https://www.google.com');
  await expect(page).toHaveTitle('Google');
});
````

✅ This checks that the browser opened the correct page.

---

## 2️⃣ Check Page URL

Ensure that the user is on the expected URL:

```ts
await expect(page).toHaveURL('https://www.example.com/dashboard');
```

* Useful after **form submissions or navigation**
* Automatically waits until the URL changes

---

## 3️⃣ Check Element Visibility / Text

Verify that an element is visible or contains the correct text:

```ts
await expect(page.getByText('Welcome, Admin')).toBeVisible();
await expect(page.getByRole('button', { name: 'Logout' })).toBeEnabled();
```

* `toBeVisible()` → checks if the element is displayed
* `toBeEnabled()` → checks if a button or input is interactable

---

## 4️⃣ Check Input Values

You can assert input field values:

```ts
await expect(page.getByLabel('Username')).toHaveValue('admin');
```

---

## 5️⃣ Check Element Count

If multiple elements exist, verify the count:

```ts
await expect(page.locator('ul > li')).toHaveCount(5);
```

---

## Why Playwright Assertions Are Powerful

* **Auto-retries**: automatically waits for conditions to be met
* **Less flaky tests**: reduces random failures
* **Readable syntax**: easy to understand for beginners
* Works **cross-browser** without changes

---

## Example: Login Flow with Assertions

```ts
await page.getByLabel('Username').fill('admin');
await page.getByLabel('Password').fill('password');
await page.getByRole('button', { name: 'Login' }).click();

// Verify successful login
await expect(page).toHaveURL('/dashboard');
await expect(page.getByText('Welcome, Admin')).toBeVisible();
await expect(page.getByRole('button', { name: 'Logout' })).toBeEnabled();
```

✅ Complete, simple, and reliable login validation.

---

## Next Step

👉 [Playwright Test Runner](/playwright/test-runner/)

---

