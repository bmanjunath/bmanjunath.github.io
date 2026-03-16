---

layout: default
title: "Understanding Locators and Selectors"
permalink: /playwright/04-locators/
-----------------------------------

# Understanding Locators in Playwright

In Playwright, **locators** tell the framework **how to find elements on a page**.

Instead of relying only on brittle CSS or XPath, Playwright provides **smart, reliable, and readable locators** that improve test stability.

Locators are designed to:

* Automatically **wait for elements**
* Be **more readable**
* Be **less flaky**
* Encourage **accessible web practices**

---

# Why Not Use Plain CSS or XPath?

Traditional selectors have several problems:

| Problem               | Explanation                                      |
| --------------------- | ------------------------------------------------ |
| Fragile               | Minor UI changes can break tests                 |
| Hard to read          | Complex CSS/XPath expressions reduce readability |
| Flaky                 | Requires manual waits in many cases              |
| Difficult to maintain | Hard to reuse across test suites                 |

Because of this, Playwright provides **higher-level locator APIs**.

---

# Playwright Locator Methods

## 1. getByRole (Best Practice)

```ts
await page.getByRole('button', { name: 'Submit' }).click();
```

This locator:

* Uses the **ARIA role** of the element (`button`, `link`, `textbox`, etc.)
* Uses the **visible accessible name**
* Is the **most recommended locator**

Example:

```ts
await page.getByRole('textbox', { name: 'Username' }).fill('admin');
```

---

# 2. getByText

```ts
await page.getByText('Login').click();
```

This locator finds elements using **visible text content**.

Useful for:

* Buttons
* Links
* Headings
* Labels

Example:

```ts
await page.getByText('Sign in').click();
```

---

# 3. getByLabel

```ts
await page.getByLabel('Username').fill('admin');
```

Targets input elements associated with a `<label>`.

Example HTML:

```html
<label>Username</label>
<input type="text" />
```

Playwright automatically finds the correct input field.

---

# 4. getByPlaceholder

```ts
await page.getByPlaceholder('Enter your email').fill('abc@example.com');
```

Targets input fields using **placeholder text**.

Example HTML:

```html
<input placeholder="Enter your email">
```

---

# 5. getByAltText

```ts
await page.getByAltText('Company Logo').click();
```

Used for images and icons that contain an **alt attribute**.

Example HTML:

```html
<img src="logo.png" alt="Company Logo">
```

---

# 6. getByTitle

```ts
await page.getByTitle('Settings').click();
```

Targets elements using the **title attribute**.

Example HTML:

```html
<button title="Settings">⚙</button>
```

---

# 7. getByTestId (Automation Friendly)

```ts
await page.getByTestId('login-button').click();
```

Example HTML:

```html
<button data-testid="login-button">Login</button>
```

Benefits:

* Stable locator
* Recommended for **test automation frameworks**
* Less likely to break due to UI changes

---

# Using CSS Selectors

Sometimes CSS selectors are necessary.

Example:

```ts
await page.locator('#username').fill('admin');
```

Example with class:

```ts
await page.locator('.login-button').click();
```

Example with attribute selector:

```ts
await page.locator('input[name="username"]').fill('admin');
```

---

# Using XPath

XPath is another way to locate elements.

Example:

```ts
await page.locator('//button[text()="Login"]').click();
```

Another example:

```ts
await page.locator('//input[@name="username"]').fill('admin');
```

⚠ XPath should be used **only when other locators are not available**.

---

# Chaining Locators

Locators can be chained to narrow searches.

Example:

```ts
await page.locator('#login-form').locator('button').click();
```

This searches for the button **inside the login form only**.

---

# Filtering Locators

Playwright allows filtering based on text or other conditions.

Example:

```ts
await page.locator('button').filter({ hasText: 'Submit' }).click();
```

---

# Selecting Specific Elements

## First Element

```ts
await page.locator('.product').first().click();
```

## Last Element

```ts
await page.locator('.product').last().click();
```

## nth Element

```ts
await page.locator('.product').nth(2).click();
```

This selects the **third element** (index starts from 0).

---

# Example: Login Form Automation

```ts
await page.getByLabel('Username').fill('admin');

await page.getByLabel('Password').fill('password');

await page.getByRole('button', { name: 'Login' }).click();
```

Advantages:

* Clear
* Readable
* Reliable
* Maintainable

---

# Best Practices

Prefer locator strategies in the following order:

1. `getByRole()`
2. `getByLabel()`
3. `getByText()`
4. `getByTestId()`
5. CSS selectors
6. XPath (last option)

This approach improves **test stability and readability**.

---

# Summary

Playwright locators provide a **modern and reliable way to identify elements**.

Benefits include:

* Built-in auto waiting
* Cleaner test code
* Better maintainability
* Reduced flaky tests

Using the right locator strategy is one of the **most important skills in Playwright automation**.

---


