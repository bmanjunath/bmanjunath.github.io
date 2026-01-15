---
layout: page
title: "Understanding Locators and Selectors"
permalink: /playwright/locators/
---

## Understanding Locators in Playwright

In Playwright, **locators** tell the framework **how to find elements on a page**.

Instead of relying on brittle CSS or XPath, Playwright provides **smart, reliable, and readable locators**.

---

## Why Not Use Plain CSS or XPath?

Traditional selectors have problems:

| Problem | Explanation |
|---------|------------|
| Fragile | Minor UI changes break tests |
| Hard to read | Complex CSS/XPath is not intuitive |
| Flaky | Requires manual waits; often fails |
| Less maintainable | Hard to reuse across tests |

---

## Playwright Locators

Playwright offers **robust locators** that are:

- **Readable** — easy to understand what element is being targeted  
- **Stable** — less likely to break when UI changes  
- **Auto-waiting** — automatically waits for elements to appear

---

## Recommended Locator Methods

### 1. getByRole (Best Practice)

```ts
await page.getByRole('button', { name: 'Submit' }).click();
Uses the ARIA role of the element (button, link, checkbox, etc.)

Uses the visible name

Most reliable and accessible
```
### 2. getByText
```ts
Copy code
await page.getByText('Login').click();
Finds elements by visible text

Great for links, buttons, or labels
```
### 3. getByLabel
```ts
Copy code
await page.getByLabel('Username').fill('admin');
Works for input fields with labels

Automatically finds associated <input> using <label>
```
### 4. getByPlaceholder
```ts
Copy code
await page.getByPlaceholder('Enter your email').fill('abc@example.com');
Targets inputs using placeholder text

Useful when labels are missing
```
### 5. getByAltText
```ts
Copy code
await page.getByAltText('Company Logo').click();
Targets images or icons using alt attribute

Very readable and maintainable
```

Why Playwright Locators Are Better Than Selectors
Auto-waiting built-in → waits for elements to be visible/ready

Readable & maintainable → easier for team members to understand

Accessible-first → encourages good practices

Cross-browser friendly → works on Chromium, Firefox, WebKit without changes

Example: Filling a Login Form
```ts

await page.getByLabel('Username').fill('admin');
await page.getByLabel('Password').fill('password');
await page.getByRole('button', { name: 'Login' }).click();
```
✅ Clear, readable, and reliable.

Summary
Avoid CSS/XPath unless absolutely necessary

Prefer getByRole, getByLabel, getByText for clarity and stability

Playwright locators make tests less flaky and easier to maintain

```
Next Step
[User Actions](/playwright/user-actions/)
```
