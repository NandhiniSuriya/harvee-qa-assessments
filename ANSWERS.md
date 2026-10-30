const { test, expect } = require('@playwright/test');

test('TC22 - Verify checkout total calculation', async ({ page }) => {
  // Step 1: Open the application
  await page.goto('https://www.saucedemo.com');

  // Step 2: Login
  await page.locator('#user-name').fill('standard_user');
  await page.locator('#password').fill('secret_sauce');
  await page.locator('#login-button').click();

  // Step 3: Verify inventory page
  await expect(page).toHaveURL(/inventory.html/);

  // Step 4: Select a specific product
  const product = page.locator('.inventory_item')
    .filter({ hasText: 'Sauce Labs Backpack' });

  const priceText = await product
    .locator('.inventory_item_price')
    .textContent();

  const productPrice = Number(priceText.replace('$', ''));

  // Step 5: Add product to cart
  await product.getByRole('button', { name: 'Add to cart' }).click();

  // Step 6: Verify cart badge
  await expect(page.locator('.shopping_cart_badge'))
    .toHaveText('1');

  // Step 7: Navigate to cart
  await page.locator('.shopping_cart_link').click();

  await expect(page.locator('.cart_item'))
    .toContainText('Sauce Labs Backpack');

  // Step 8: Proceed to checkout
  await page.locator('#checkout').click();

  // Step 9: Enter checkout information
  await page.locator('#first-name').fill('John');
  await page.locator('#last-name').fill('Smith');
  await page.locator('#postal-code').fill('641001');
  await page.locator('#continue').click();

  // Step 10: Verify checkout overview
  await expect(page).toHaveURL(/checkout-step-two.html/);

  const subtotalText = await page
    .locator('.summary_subtotal_label')
    .textContent();

  const taxText = await page
    .locator('.summary_tax_label')
    .textContent();

  const totalText = await page
    .locator('.summary_total_label')
    .textContent();

  // Step 11: Calculate expected total
  const subtotal = Number(subtotalText.match(/[\d.]+/)[0]);
  const tax = Number(taxText.match(/[\d.]+/)[0]);
  const actualTotal = Number(totalText.match(/[\d.]+/)[0]);

  const expectedTotal = Number((subtotal + tax).toFixed(2));

  // Step 12: Validate subtotal and total
  expect(subtotal).toBe(productPrice);
  expect(actualTotal).toBe(expectedTotal);
});


----------------------------------------------------
B2) 1. Requirement coverage – By rubric: Compare generated test cases against a predefined checklist of acceptance criteria and assign a score based on how many requirements are covered.

2. No invented requirements – By human review: A QA reviewer compares the generated test cases with the original user story and checks whether the AI has introduced any unsupported functionality or assumptions.

3. Duplicate test cases – Automatically: Use a script to identify duplicate test case titles or similar steps and flag repetitive scenarios.

4. JSON format validation – Automatically: Use a JSON parser and schema validation to check whether the output is valid and can be successfully imported into the test management tool.


--------------------------------------------------

b3)

Title
[Release 4.2.0] Price sorting (Low to High) displays products in incorrect order

Environment
- Application: Sauce Demo
- Release: 4.2.0
- Browser: Google Chrome
- Test Type: Functional Testing
- Test Environment: QA
- Frequency: 100% reproducible since release 4.2.0

Preconditions
- User has valid login credentials.
- User is logged into the application.
- Inventory page contains products with different prices.

Steps to Reproduce
1. Launch the Sauce Demo application in Google Chrome.
2. Log in using valid credentials (`standard_user` / `secret_sauce`).
3. Navigate to the Products/Inventory page.
4. Open the product sorting dropdown.
5. Select **Price (low to high)**.
6. Observe the order of the displayed products and their prices.

Expected Result
Products should be displayed in ascending order of price, starting with the lowest-priced product and ending with the highest-priced product.

Example: A product priced at $15.99 should appear before a product priced at $29.99.

Actual Result
The product priced at $29.99 is displayed before the product priced at $15.99, which violates the expected ascending price order.

The issue is reproducible on every test run since release 4.2.0.

Severity
High


Priority
High (P1) – Recommend fixing before release.

Attach Evidence

-------------------------

b4)

Hi,

During our testing of release 4.2.0, we identified two issues that need attention before Friday's release:

1. Product sorting: Products are consistently displayed in the wrong price order when sorting from low to high.
2. Checkout: The checkout process fails intermittently in approximately 1 out of 10 test runs, although it passes when retried.

Recommendation: From a QA perspective, I recommend postponing the full release until the sorting issue is fixed and the checkout failure is investigated and verified.

Alternative: If Friday's release is business-critical, we can consider excluding the affected sorting functionality, with your approval, and proceed only after checkout passes repeated stability testing.

We can prioritize retesting both areas and share an updated QA status before the final release decision.

