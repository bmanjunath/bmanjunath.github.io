---

layout: default
title: "User Actions in Playwright"
permalink: /playwright/05-user-actions/
---

# User Actions in Playwright

After learning how to **locate elements**, the next step is to **interact with them**.

Playwright allows you to simulate **real user behavior**, such as:

* Clicking buttons
* Typing text
* Selecting dropdown values
* Hovering over elements
* Uploading files
* Dragging and dropping elements

Playwright actions are powerful because they **automatically wait for elements to be ready** before performing actions.

---

# 1️⃣ Click

Clicking is one of the most common user actions.

```ts
await page.getByRole('button', { name: 'Login' }).click();
```

Playwright automatically waits until the element is:

* Visible
* Stable
* Enabled
* Ready to receive the click

Example:

```ts
await page.getByText('Submit').click();
```

---

# 2️⃣ Double Click

You can perform a double click using `dblclick()`.

```ts
await page.getByText('Edit').dblclick();
```

Useful when UI actions require a double click.

---

# 3️⃣ Right Click (Context Click)

Right click opens a context menu.

```ts
await page.getByText('Options').click({ button: 'right' });
```

---

# 4️⃣ Typing Text

Playwright provides two ways to enter text.

### Using `fill()`

```ts
await page.getByLabel('Username').fill('admin');
```

This **replaces existing text instantly**.

### Using `type()`

```ts
await page.getByLabel('Username').type('admin');
```

This **simulates real typing**, character by character.

| Method | Behavior                                 |
| ------ | ---------------------------------------- |
| fill() | Clears existing text and enters new text |
| type() | Types like a real user                   |

---

# 5️⃣ Clear Input Field

```ts
await page.getByLabel('Search').clear();
```

Removes existing text from input fields.

---

# 6️⃣ Hover

Hovering triggers menus, tooltips, and UI effects.

```ts
await page.getByText('Settings').hover();
```

Useful for:

* Dropdown menus
* Hidden navigation menus
* Tooltips

---

# 7️⃣ Check and Uncheck Checkboxes

```ts
await page.getByLabel('Accept Terms').check();
```

Uncheck:

```ts
await page.getByLabel('Accept Terms').uncheck();
```

Playwright ensures the checkbox reaches the desired state.

---

# 8️⃣ Select Dropdown Values

Selecting values from `<select>` dropdowns.

```ts
await page.selectOption('#country', 'India');
```

Or:

```ts
await page.getByLabel('Country').selectOption('India');
```

You can also select by value:

```ts
await page.selectOption('#country', { value: 'IN' });
```

---

# 9️⃣ Upload Files

Playwright makes file upload easy.

```ts
await page.setInputFiles('input[type="file"]', 'tests/files/sample.pdf');
```

Upload multiple files:

```ts
await page.setInputFiles('input[type="file"]', [
  'file1.pdf',
  'file2.pdf'
]);
```

---

# 🔟 Drag and Drop

Used for UI interactions involving dragging elements.

```ts
await page.dragAndDrop('#source', '#target');
```

Example:

```ts
await page.dragAndDrop('#item', '#cart');
```

---

# 1️⃣1️⃣ Keyboard Actions

Simulate keyboard presses.

```ts
await page.keyboard.press('Enter');
```

Type text using keyboard:

```ts
await page.keyboard.type('Hello World');
```

Common keys:

| Key       | Action              |
| --------- | ------------------- |
| Enter     | Submit forms        |
| Escape    | Close dialogs       |
| ArrowDown | Navigate menus      |
| Tab       | Move between inputs |

Example:

```ts
await page.keyboard.press('Tab');
```

---

# 1️⃣2️⃣ Mouse Actions

Low-level mouse control.

```ts
await page.mouse.move(100, 200);
await page.mouse.down();
await page.mouse.up();
```

Click using coordinates:

```ts
await page.mouse.click(100, 200);
```

These are useful for:

* Canvas interactions
* Complex drag-and-drop
* Custom UI components

---

# Example: Login Flow

```ts
await page.getByLabel('Username').fill('admin');

await page.getByLabel('Password').fill('mypassword');

await page.getByRole('button', { name: 'Login' }).click();

await expect(page).toHaveURL('/dashboard');
```

This example demonstrates a **typical login automation flow**.

---

# Why Playwright User Actions Are Powerful

Playwright actions provide several advantages:

* **Auto waiting** – no need for manual sleep
* **Cross-browser compatibility** – Chromium, Firefox, WebKit
* **Real user simulation**
* **Stable test execution**
* **Readable automation code**

---

# Best Practices

Follow these practices for stable tests:

* Use **Playwright locators instead of raw CSS/XPath**
* Avoid hardcoded waits like `waitForTimeout`
* Prefer **role-based locators**
* Keep tests **small and readable**

---

# Summary

User actions allow Playwright tests to simulate **real user interactions with the browser**.

These actions include:

* Clicking elements
* Typing text
* Hovering
* Selecting dropdowns
* Uploading files
* Dragging elements

Combining **locators + user actions** creates reliable and maintainable automation tests.

---

# Next Step

👉 [Assertions & Validations](/playwright/assertions/)

---
