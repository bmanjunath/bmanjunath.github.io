---

layout: default
title: "Assertions & Validations"
permalink: /playwright/06-assertions/
---

# Assertions & Validations in Playwright

Assertions are how we **verify that our application behaves as expected**.

They confirm that the application state matches the **expected outcome** after performing actions.

Playwright provides a powerful built-in assertion library using the `expect` function from **Playwright Test**.

```ts
import { test, expect } from '@playwright/test';
```

Playwright assertions are designed to be:

* **Auto-retrying**
* **Readable**
* **Reliable**
* **Cross-browser compatible**

---

# Why Assertions Are Important

Assertions help validate:

* Page navigation
* UI visibility
* Form submissions
* Data updates
* User interactions

Without assertions, tests only **perform actions but never verify results**.

---

# 1️⃣ Verify Page Title

Ensure the browser opened the correct page.

```ts
import { test, expect } from '@playwright/test';

test('Verify Google title', async ({ page }) => {
  await page.goto('https://www.google.com');
  await expect(page).toHaveTitle('Google');
});
```

This confirms the correct page has loaded.

---

# 2️⃣ Verify Page URL

Check whether the page navigated to the expected URL.

```ts
await expect(page).toHaveURL('https://www.example.com/dashboard');
```

Useful for verifying:

* Login success
* Redirects
* Navigation flows

Playwright automatically **waits until the URL changes**.

---

# 3️⃣ Verify Element Visibility

Check if an element is visible on the page.

```ts
await expect(page.getByText('Welcome, Admin')).toBeVisible();
```

Other useful visibility assertions:

```ts
await expect(page.getByText('Error')).toBeHidden();
```

| Assertion        | Purpose               |
| ---------------- | --------------------- |
| `toBeVisible()`  | Element is visible    |
| `toBeHidden()`   | Element is hidden     |
| `toBeAttached()` | Element exists in DOM |

---

# 4️⃣ Verify Element State

Check whether elements are enabled, disabled, checked, or editable.

```ts
await expect(page.getByRole('button', { name: 'Logout' })).toBeEnabled();
```

Other examples:

```ts
await expect(page.getByLabel('Accept Terms')).toBeChecked();

await expect(page.getByLabel('Username')).toBeEditable();

await expect(page.getByRole('button', { name: 'Submit' })).toBeDisabled();
```

Common state assertions:

| Assertion        | Description             |
| ---------------- | ----------------------- |
| `toBeEnabled()`  | Element is enabled      |
| `toBeDisabled()` | Element is disabled     |
| `toBeChecked()`  | Checkbox is selected    |
| `toBeEditable()` | Input field is editable |

---

# 5️⃣ Verify Text Content

Check that an element contains expected text.

```ts
await expect(page.getByRole('heading')).toHaveText('Dashboard');
```

Partial text match:

```ts
await expect(page.getByText('Welcome')).toContainText('Admin');
```

---

# 6️⃣ Verify Input Values

Validate values entered in input fields.

```ts
await expect(page.getByLabel('Username')).toHaveValue('admin');
```

This ensures the field contains the expected value.

---

# 7️⃣ Verify Element Count

Useful when validating lists or tables.

```ts
await expect(page.locator('ul > li')).toHaveCount(5);
```

Example:

```ts
await expect(page.locator('.product-item')).toHaveCount(10);
```

---

# 8️⃣ Verify Attributes

You can validate HTML attributes.

```ts
await expect(page.locator('#logo')).toHaveAttribute('alt', 'Company Logo');
```

Example:

```ts
await expect(page.locator('#submit')).toHaveAttribute('type', 'submit');
```

---

# 9️⃣ Soft Assertions

Soft assertions allow the test to continue even if an assertion fails.

```ts
await expect.soft(page.getByText('Welcome')).toBeVisible();
```

This is useful when you want to **collect multiple failures in a single test**.

---

# Example: Login Flow with Assertions

```ts
await page.getByLabel('Username').fill('admin');

await page.getByLabel('Password').fill('password');

await page.getByRole('button', { name: 'Login' }).click();

await expect(page).toHaveURL('/dashboard');

await expect(page.getByText('Welcome, Admin')).toBeVisible();

await expect(page.getByRole('button', { name: 'Logout' })).toBeEnabled();
```

This example validates that:

* Login was successful
* User reached the dashboard
* Correct UI elements are displayed

---

# Why Playwright Assertions Are Powerful

Playwright assertions provide several benefits:

* **Auto-retry mechanism** → waits until conditions are met
* **Reduces flaky tests**
* **Improves readability**
* **Works across Chromium, Firefox, and WebKit**

Example:

```ts
await expect(page.getByText('Order Successful')).toBeVisible();
```

Playwright will **retry until the text appears or timeout occurs**.

---

# Best Practices

Follow these practices for stable tests:

* Use **locator-based assertions**
* Avoid manual waits (`waitForTimeout`)
* Prefer **Playwright locators over CSS/XPath**
* Keep assertions **clear and meaningful**

---

# Summary

Assertions validate that the application behaves as expected.

Common assertions include:

* Page title validation
* URL verification
* Element visibility
* Input value checks
* Element count verification
* Attribute validation

Using strong assertions ensures your tests are **reliable, maintainable, and trustworthy**.

---

# Next Step

👉 [Playwright Test Runner](/playwright/test-runner/)

---
