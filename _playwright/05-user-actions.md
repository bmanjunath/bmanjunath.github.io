---
layout: page
title: "User Actions in Playwright"
permalink: /playwright/05-user-actions/
---

## User Actions in Playwright

After learning how to locate elements, the next step is to **interact with them**.  
Playwright lets you simulate **real user actions** like clicking buttons, typing text, and hovering over elements.

These actions are reliable and automatically wait for elements to be ready.

---

## 1️⃣ Click

Clicking is one of the most common actions.

```ts
// Click a button by its role and name
await page.getByRole('button', { name: 'Login' }).click();
````

* **Auto-waits** for the button to be visible and enabled
* Works reliably across browsers

---

## 2️⃣ Type Text

Fill input fields with `fill()` or `type()`.

```ts
// Fill username and password fields
await page.getByLabel('Username').fill('admin');
await page.getByLabel('Password').fill('mypassword');
```

Difference between `fill()` and `type()`:

| Method | Behavior                                          |
| ------ | ------------------------------------------------- |
| fill() | Replaces existing text instantly                  |
| type() | Simulates actual typing (slower, more human-like) |

---

## 3️⃣ Hover

Hovering is used to reveal hidden menus or tooltips.

```ts
await page.getByText('Settings').hover();
```

* Automatically waits for the element to appear
* Triggers hover effects like dropdown menus

---

## 4️⃣ Keyboard Actions

You can simulate **keyboard keys**:

```ts
// Press Enter
await page.keyboard.press('Enter');

// Type text manually
await page.keyboard.type('Hello World!');
```

---

## 5️⃣ Mouse Actions (Optional)

Advanced mouse actions:

```ts
await page.mouse.move(100, 200);  // Move cursor to coordinates
await page.mouse.down();           // Press mouse button
await page.mouse.up();             // Release mouse button
await page.mouse.click(100, 200);  // Click at coordinates
```

These are rarely needed with modern locators but useful for drag-and-drop or canvas interactions.

---

## Why Playwright User Actions Are Powerful

* **Auto-waiting** → no need for manual sleep
* **Cross-browser** → works on Chromium, Firefox, WebKit
* **Human-like interactions** → better simulation of real users
* **Debuggable** → works with headed mode for visual validation

---

## Example: Login Flow with User Actions

```ts
await page.getByLabel('Username').fill('admin');
await page.getByLabel('Password').fill('mypassword');
await page.getByRole('button', { name: 'Login' }).click();
await expect(page).toHaveURL('/dashboard');
```

✅ Clean, readable, and reliable.

---

## Next Step

👉 [Assertions & Validations](/playwright/assertions/)

---

