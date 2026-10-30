Question for the product owner:
1	Is the postal code validated for format or length?
2	How is tax calculated?
3	Does the cart persist after logout and login?
4	Is the product sorting alphabetical order case-insensitive, and should it use the complete product name?
5	Can a customer add multiple quantities of the same product, or is each product limited to one item?
6	Which browsers and screen sizes are supported?
7	What validation messages should appear when first name, last name or postal code are missing?
8	Should the checkout overview calculate tax on the subtotal, and how many decimal places should be displayed?
9	What accessibility standard applies?
10	should the cart badge display the total quantity of products or the number of distinct products?



ID	Area	Type	Title	Pre-conditions	Steps	Test data	Expected result	Priority (P1–P3)	Automate? (Yes / No) and why
TC01	Login	Positive	Verify that a registered user should be able to log in successfully using valid credentials.	1. Application should be accessible. 2. User should be on the login page.	1. Launch the application. 2. Enter a valid username in the Username field. 3. Enter a valid password in the Password field. 4. Click the Login button. 5. Verify the navigation after login.	Username: standard_user, Password: secret_sauce	Should authenticate the user successfully.	P1	Yes – Login is a frequently used functionality and can be validated repeatedly through automated regression tests.
TC02	Login	Negative	Verify that the application should reject login attempts when an incorrect password is entered.	1. Application should be accessible. 2. User should be on the login page.	1. Launch the application. 2. Enter a valid username. 3. Enter an incorrect password. 4. Click Login. 5. Observe the error message.	Username: standard_user; Password: wrong_password	Should reject the login attempt. Should display an appropriate authentication error message. Should keep the user on the login page without granting access.	P1	Yes – Negative authentication scenarios should be included in automated regression testing to ensure security and validation behavior.
TC03	Login	Negative	Verify that the application should reject login attempts when an invalid username is entered.	1. Application should be accessible. 2. User should be on the login page.	1. Launch the application. 2. Enter an invalid username. 3. Enter a valid password. 4. Click Login. 5. Observe the application response.	Username: invalid_user, Password: secret_sauce	Should reject the login attempt. Should display an appropriate invalid credentials error message.	P1	Yes – Invalid username validation is a repeatable authentication scenario suitable for automation.
TC04	Login	Negative	Verify that the application should display mandatory field validation when both username and password fields are empty.	1. Application should be accessible. 2. User should be on the login page.	1. Launch the application. 2. Leave the Username field empty. 3. Leave the Password field empty. 4. Click Login. 5. Observe the validation message.	Username: Blank, Password: Blank	Should prevent the login attempt. Should display a validation message indicating that the username is required	P1	Yes – Mandatory field validation is deterministic and can be automated easily.
TC05	Login	Negative	Verify that the application should restrict login access for locked-out users.	1. Application should be accessible. 2. User should be on the login page. 3. Locked-out test account should be available.	1. Launch the application. 2. Enter the locked-out username. 3. Enter the valid password. 4. Click Login. 5. Observe the error message.	Username: locked_out_user, Password: secret_sauce	Should prevent the locked-out user from logging in. Should display an appropriate account-locked error message	P1	Yes – Locked-account behavior should be covered in automated security and authentication regression tests.
TC06	Login / Security	Security	Verify that an unauthenticated user should not be able to access the inventory page through direct URL navigation.	1. Application should be accessible. 2. User should be logged out.	1. Open a new browser session. 2. Ensure the user is logged out. 3. Enter the direct inventory URL in the browser. 4. Press Enter. 5. Observe the application response.	URL: https://www.saucedemo.com/inventory.html	Should prevent unauthenticated access to the inventory page. Should redirect the user to the login page or display an appropriate access restriction. Should not expose protected application content.	P1	Yes – Direct URL access restrictions should be included in automated security regression testing.
TC07	Products	Positive	Verify that all available products should be displayed correctly on the inventory page.	1. User should be logged in successfully. 2. Inventory page should be displayed.	1. Log in using valid credentials. 2. Navigate to the inventory page. 3. Observe all available products. 4. Verify product names and descriptions. 5. Verify product images. 6. Verify product prices. 7. Compare displayed details with expected product information.	Username: standard_user; Password: secret_sauce; Expected products: All available inventory products	Should display all available products. Should display correct product names, descriptions and prices. Should load the corresponding product images without broken links. Should display Add to cart buttons.	P1	Yes – Product listing is a core functionality and can be validated using automated UI assertions.
TC08	Products / Sorting	Positive	Verify that products should be sorted in ascending alphabetical order when Name A to Z is selected.	1. User should be logged in. 2. Inventory page should contain multiple products.	1. Log in to the application. 2. Navigate to the inventory page. 3. Locate the sorting dropdown. 4. Select Name (A to Z). 5. Capture all displayed product names. 6. Compare the sequence with the expected alphabetical order.	Sorting option: az	Should display products in ascending alphabetical order. Should display the products starting with A and ending with Z. Should maintain the correct association between product names, images and prices.	P1	Yes – Sorting order can be validated automatically by comparing the displayed product names with a sorted array.
TC09	Products / Sorting	Positive	Verify that products should be sorted in descending alphabetical order when Name Z to A is selected.	1. User should be logged in. 2. Inventory page should be displayed.	1. Log in to the application. 2. Navigate to the inventory page. 3. Click the sorting dropdown. 4. Select Name (Z to A). 5. Capture all displayed product names. 6. Compare the sequence with the expected descending alphabetical order.	Sorting option: za	Should display products in descending alphabetical order. Should display the products starting with Z and ending with A. Should maintain correct product information after sorting.	P2	Yes – Reverse alphabetical sorting is deterministic and suitable for automated functional testing.
TC10	Products / Sorting	Positive	Verify that products should be sorted in ascending numerical price order when Price Low to High is selected.	1. User should be logged in. 2. Products with different prices should be available.	1. Log in to the application. 2. Navigate to the inventory page. 3. Click the sorting dropdown. 4. Select Price (low to high). 5. Capture all displayed product prices. 6. Compare the sequence against the expected ascending numerical order. 7. Verify the corresponding product names and prices.	Sorting option: lohi	Should arrange products in ascending numerical price order. Should display the lowest-priced product first and the highest-priced product last. Should not compare prices as text strings.	P1	Yes – Numeric price sorting can be validated using JavaScript array sorting and Playwright assertions.
TC11	Products / Sorting	Positive	Verify that products should be sorted in descending numerical price order when Price High to Low is selected.	1. User should be logged in. 2. Inventory page should be displayed.	1. Log in to the application. 2. Navigate to the inventory page. 3. Click the sorting dropdown. 4. Select Price (high to low). 5. Capture all displayed product prices. 6. Compare the sequence against the expected descending numerical price order.	Sorting option: hilo	Should arrange products in descending numerical price order. Should display the highest-priced product first and the lowest-priced product last. Should maintain correct product details.	P1	Yes – Price sorting can be validated through automated numeric comparisons.
TC12	Products / Sorting	Positive	Verify that product sorting should work correctly when switching between multiple sorting options.	1. User should be logged in. 2. Inventory page should be displayed.	1. Select Name (A to Z). 2. Verify ascending alphabetical order. 3. Change to Price (low to high). 4. Verify ascending price order. 5. Change to Name (Z to A). 6. Verify descending alphabetical order. 7. Change to Price (high to low). 8. Verify descending price order.	Sorting options: az, lohi, za, hilo	Should update the product listing based on each selected sorting option. Should apply the correct sorting logic every time. Should not display duplicate or missing products.	P2	Yes – Multiple sorting combinations can be validated using data-driven automation tests.
TC13	Shopping Cart	Positive	Verify that a selected product should be added successfully to the shopping cart.	1. User should be logged in. 2. Shopping cart should initially be empty.	1. Log in to the application. 2. Navigate to the inventory page. 3. Locate Sauce Labs Backpack. 4. Click Add to cart. 5. Verify the cart badge. 6. Open the shopping cart. 7. Verify the selected product details.	Product: Sauce Labs Backpack; Expected cart count: 1	Should add the selected product successfully. Should update the cart badge to 1. Should display the selected product name, description and price in the cart. Should change the product action to Remove.	P1	Yes – Adding products is a core shopping workflow and should be covered by automated regression tests.
TC14	Shopping Cart	Positive	Verify that multiple products should be added successfully to the shopping cart.	1. User should be logged in. 2. Shopping cart should initially be empty.	1. Log in to the application. 2. Add Sauce Labs Backpack. 3. Add Sauce Labs Bike Light. 4. Add one more available product. 5. Verify the cart badge count. 6. Open the shopping cart. 7. Verify all selected products.	Products: Sauce Labs Backpack, Sauce Labs Bike Light, Sauce Labs Bolt T-Shirt; Expected cart count: 3	Should allow multiple products to be added. Should display the correct total item count in the cart badge. Should display all selected products with correct names and prices. Should not add unselected products.	P1	Yes – Multiple product selection and cart count validation can be automated efficiently.
TC15	Shopping Cart	Positive	Verify that a selected product should be removed successfully from the shopping cart.	1. User should be logged in. 2. At least two products should be added to the cart.	1. Log in to the application. 2. Add Sauce Labs Backpack and Sauce Labs Bike Light. 3. Open the shopping cart. 4. Verify both products. 5. Locate Sauce Labs Backpack. 6. Click Remove for that product. 7. Verify the remaining product. 8. Verify the cart badge.	Products: Sauce Labs Backpack, Sauce Labs Bike Light; Product to remove: Sauce Labs Backpack	Should remove only the selected product. Should retain all other products. Should update the cart badge from 2 to 1. Should maintain the correct details of the remaining product.	P1	Yes – Product removal and cart badge updates are repeatable and suitable for UI automation.
TC16	Shopping Cart	Boundary	Verify that all products should be removed successfully from the shopping cart.	1. User should be logged in. 2. Multiple products should be available in the cart.	1. Log in to the application. 2. Add at least three products. 3. Open the shopping cart. 4. Verify all three products. 5. Click Remove for the first product. 6. Repeat for the remaining products. 7. Verify the cart contents and badge.	Products: Sauce Labs Backpack, Sauce Labs Bike Light, Sauce Labs Bolt T-Shirt; Expected cart count: 0	Should remove all selected products successfully. Should display an empty shopping cart. Should remove the cart badge or display zero items. Should not display any previously removed products.	P1	Yes – Empty cart behavior can be verified using automated assertions.
TC17	Shopping Cart	Positive	Verify that the shopping cart should retain previously added products when navigating between inventory and cart pages.	1. User should be logged in. 2. Inventory page should be displayed.	1. Log in to the application. 2. Add Sauce Labs Backpack. 3. Add Sauce Labs Bike Light. 4. Open the shopping cart. 5. Verify both products. 6. Click Continue Shopping. 7. Verify navigation to inventory. 8. Open the shopping cart again. 9. Verify previously added products.	Products: Sauce Labs Backpack, Sauce Labs Bike Light; Expected cart count: 2	Should retain previously added products during navigation. Should display the same products when the cart is reopened. Should maintain the correct cart badge count. Should not remove or duplicate products.	P2	Yes – Cart state persistence during navigation can be covered by automated end-to-end tests.
TC18	Checkout	Positive	Verify that the user should be able to proceed to the checkout overview page by entering valid customer information.	1. User should be logged in. 2. At least one product should be added to the shopping cart.	1. Log in using valid credentials. 2. Add Sauce Labs Backpack to the cart. 3. Open the shopping cart. 4. Verify the selected product. 5. Click Checkout. 6. Enter First Name. 7. Enter Last Name. 8. Enter Postal Code. 9. Click Continue. 10. Verify the checkout overview page.	First Name: Nandhini; Last Name: G; Postal Code: 641001	Should accept valid customer information. Should navigate to the checkout overview page. Should display selected product details, item subtotal, tax and final order total.	P1	Yes – Checkout navigation and mandatory customer information can be validated through automated end-to-end tests.
TC19	Checkout	Negative	Verify that the application should display validation when the First Name field is left empty during checkout.	1. User should be logged in. 2. Cart should contain at least one product. 3. User should be on the checkout information page.	1. Open the shopping cart. 2. Click Checkout. 3. Leave First Name empty. 4. Enter a valid Last Name. 5. Enter a valid Postal Code. 6. Click Continue. 7. Observe the validation message.	First Name: Blank; Last Name: G; Postal Code: 641001	Should prevent the user from proceeding to the overview page. Should display a validation message indicating First Name is required. Should retain the other entered field values.	P1	Yes – Mandatory field validation is deterministic and suitable for automated negative testing.
TC20	Checkout	Negative	Verify that the application should display validation when the Last Name field is left empty during checkout.	1. User should be logged in. 2. Cart should contain at least one product. 3. User should be on the checkout information page.	1. Open the shopping cart. 2. Click Checkout. 3. Enter a valid First Name. 4. Leave Last Name empty. 5. Enter a valid Postal Code. 6. Click Continue. 7. Observe the validation message.	First Name: Nandhini; Last Name: Blank; Postal Code: 641001	Should prevent the user from proceeding to the overview page. Should display a validation message indicating Last Name is required. Should retain the other entered field values.	P1	Yes – Last Name mandatory validation can be covered through automated negative testing.
TC21	Checkout	Negative	Verify that the application should display validation when the Postal Code field is left empty during checkout.	1. User should be logged in. 2. Cart should contain at least one product. 3. User should be on the checkout information page.	1. Open the shopping cart. 2. Click Checkout. 3. Enter a valid First Name. 4. Enter a valid Last Name. 5. Leave Postal Code empty. 6. Click Continue. 7. Observe the validation message.	First Name: Nandhini; Last Name: G; Postal Code: Blank	Should prevent the user from proceeding to the overview page. Should display a validation message indicating Postal Code is required. Should retain the other entered field values.	P1	Yes – Postal Code mandatory validation can be verified using Playwright assertions.
TC22	Checkout	Positive	Verify that the application should calculate the correct subtotal, tax and final order total during checkout.	1. User should be logged in. 2. At least two products should be added to the cart. 3. Valid customer information should be available.	1. Log in to the application. 2. Add two products to the cart. 3. Open the cart and verify selected products. 4. Click Checkout. 5. Enter valid customer details. 6. Click Continue. 7. Capture individual product prices. 8. Calculate the sum of product prices. 9. Compare it with Item Total. 10. Capture tax. 11. Add subtotal and tax. 12. Compare the calculated amount with the displayed Total.	Products: Sauce Labs Backpack ($29.99), Sauce Labs Bike Light ($9.99); Expected subtotal: $39.98; Tax: As displayed by application	Should calculate the subtotal correctly. Should display the correct tax amount. Should calculate the final total as subtotal plus tax. Should display the correct currency and decimal precision. Should exclude removed products from the calculation.	P1	Yes – Price calculations are deterministic and can be validated using JavaScript numeric assertions.
TC23	Checkout	Positive	Verify that the order should be completed successfully when the user clicks the Finish button after reviewing the order.	1. User should be logged in. 2. Cart should contain at least one product. 3. Valid customer details should be available.	1. Log in to the application. 2. Add the required products. 3. Open the shopping cart. 4. Click Checkout. 5. Enter valid customer details. 6. Click Continue. 7. Verify product details and final order total. 8. Click Finish. 9. Observe the confirmation page. 10. Verify the confirmation message.	First Name: Nandhini; Last Name: G; Postal Code: 641001; Product: Sauce Labs Backpack	Should process the order successfully. Should display the order confirmation page. Should display "Thank you for your order!" Should clear the cart after successful order completion.	P1	Yes – Successful order completion is a critical end-to-end business workflow and should be automated.
TC24	Checkout	Negative	Verify that the user should be able to cancel the checkout process without completing the order.	1. User should be logged in. 2. At least one product should be added to the cart.	1. Log in to the application. 2. Add Sauce Labs Backpack. 3. Open the shopping cart. 4. Click Checkout. 5. Enter valid customer information if required. 6. Continue to the overview page if necessary. 7. Click Cancel. 8. Observe the redirected page. 9. Open the shopping cart. 10. Verify the previously selected product.	Product: Sauce Labs Backpack; Customer details: Valid test data	Should cancel the checkout process. Should navigate to the appropriate shopping page. Should not place or complete an order. Should retain previously added products in the shopping cart. Should not display an order confirmation message.	P2	Yes – Checkout cancellation and cart state can be validated through automated functional tests.
TC25	Security / Authorization	Security	Verify that locked-out and unauthenticated users should not be able to access protected application pages or shopping functionality.	1. Application should be accessible. 2. User should be logged out. 3. Locked-out test account should be available.	1. Launch the application in a new browser session. 2. Ensure the user is logged out. 3. Enter the direct inventory URL. 4. Verify the application response. 5. Attempt to access the shopping cart URL directly. 6. Attempt to access the checkout URL directly. 7. Navigate to the login page. 8. Enter locked_out_user and secret_sauce. 9. Click Login. 10. Verify access restriction.	Username: locked_out_user; Password: secret_sauce; URLs: /inventory.html, /cart.html, /checkout-step-one.html	Should prevent unauthenticated users from accessing protected pages. Should redirect users to the login page or display an access restriction. Should deny login for locked-out users. Should not expose protected shopping or checkout information.	P1	Yes – Authentication and authorization restrictions should be included in automated security regression testing.






Loginpage.js : 

class LoginPage {

    constructor(page) {

        this.page = page;

        this.username = page.locator('#user-name');

        this.password = page.locator('#password');

        this.loginButton = page.locator('#login-button');

        this.errorMessage = page.locator('[data-test="error"]');

    }

    async navigate() {

        await this.page.goto('/');

    }

    async login(username, password) {

        await this.username.fill(username);

        await this.password.fill(password);

        await this.loginButton.click();

    }

}

module.exports = { LoginPage };

-------------------------------------------------------


class InventoryPage {

    constructor(page) {

        this.page = page;

        this.inventoryItems = page.locator('.inventory_item');

        this.sortDropdown = page.locator('[data-test="product-sort-container"]');

        this.cartBadge = page.locator('.shopping_cart_badge');

        this.cartLink = page.locator('.shopping_cart_link');

    }

    async sortProducts(option) {

        await this.sortDropdown.selectOption(option);

    }

    async getProductNames() {

        return await this.inventoryItems
            .locator('.inventory_item_name')
            .allTextContents();

    }

    async getProductPrices() {

        const prices = await this.inventoryItems
            .locator('.inventory_item_price')
            .allTextContents();

        return prices.map(price =>
            Number(price.replace('$', ''))
        );

    }

    async addProduct(productName) {

        const product = this.inventoryItems.filter({
            has: this.page.locator('.inventory_item_name', {
                hasText: productName
            })
        });

        await product.locator('button').click();

    }

    async openCart() {

        await this.cartLink.click();

    }

}

module.exports = { InventoryPage };

-------------------------------------------------

class CartPage {

    constructor(page) {

        this.page = page;

        this.cartItems = page.locator('.cart_item');

        this.checkoutButton = page.locator('#checkout');

    }

    async removeProduct(productName) {

        const product = this.cartItems.filter({
            has: this.page.locator('.inventory_item_name', {
                hasText: productName
            })
        });

        await product.locator('button').click();

    }

    async checkout() {

        await this.checkoutButton.click();

    }

}

module.exports = { CartPage };

---------------------------------------------

class CheckoutPage {

    constructor(page) {

        this.page = page;

        this.firstName = page.locator('#first-name');

        this.lastName = page.locator('#last-name');

        this.postalCode = page.locator('#postal-code');

        this.continueButton = page.locator('#continue');

        this.finishButton = page.locator('#finish');

        this.confirmationMessage = page.locator('.complete-header');

    }

    async enterCustomerDetails(first, last, postal) {

        await this.firstName.fill(first);

        await this.lastName.fill(last);

        await this.postalCode.fill(postal);

        await this.continueButton.click();

    }

    async finishOrder() {

        await this.finishButton.click();

    }

}

module.exports = { CheckoutPage };

---------------------------------------------------

const { test, expect } = require('@playwright/test');

const { LoginPage } = require('../pages/LoginPage');

const { InventoryPage } = require('../pages/InventoryPage');

const { CartPage } = require('../pages/CartPage');

const { CheckoutPage } = require('../pages/CheckoutPage');


const username = 'standard_user';

const password = 'secret_sauce';


// Reusable login method

async function loginAsStandardUser(page) {

    const login = new LoginPage(page);

    await login.navigate();

    await login.login(username, password);

    await expect(page).toHaveURL(/inventory.html/);

}


// TC01 - Valid Login

test('AT01 - Verify successful login with valid credentials', async ({ page }) => {

    const login = new LoginPage(page);

    await login.navigate();

    await login.login(username, password);

    await expect(page).toHaveURL(/inventory.html/);

    await expect(page.locator('.inventory_item')).toHaveCount(6);

});


// TC05 - Locked Out User

test('AT02 - Verify login restriction for locked out user', async ({ page }) => {

    const login = new LoginPage(page);

    await login.navigate();

    await login.login('locked_out_user', password);

    await expect(login.errorMessage).toBeVisible();

    await expect(login.errorMessage).toContainText('locked out');

});


// TC08 - Sort Products A to Z

test('AT03 - Verify products are sorted alphabetically A to Z', async ({ page }) => {

    await loginAsStandardUser(page);

    const inventory = new InventoryPage(page);

    await inventory.sortProducts('az');

    const actualNames = await inventory.getProductNames();

    const expectedNames = [...actualNames].sort((a, b) =>
        a.localeCompare(b)
    );

    expect(actualNames).toEqual(expectedNames);

});


// TC10 - Sort Products by Price Low to High

test('AT04 - Verify products are sorted by price Low to High', async ({ page }) => {

    await loginAsStandardUser(page);

    const inventory = new InventoryPage(page);

    await inventory.sortProducts('lohi');

    const actualPrices = await inventory.getProductPrices();

    const expectedPrices = [...actualPrices].sort((a, b) => a - b);

    expect(actualPrices).toEqual(expectedPrices);

});


// TC13 - Add Product to Cart

test('AT05 - Verify selected product is added to cart', async ({ page }) => {

    await loginAsStandardUser(page);

    const inventory = new InventoryPage(page);

    await inventory.addProduct('Sauce Labs Backpack');

    await expect(inventory.cartBadge).toHaveText('1');

    await inventory.openCart();

    const cart = new CartPage(page);

    await expect(cart.cartItems).toHaveCount(1);

    await expect(cart.cartItems).toContainText('Sauce Labs Backpack');

});


// TC15 - Remove Product from Cart

test('AT06 - Verify selected product is removed from cart', async ({ page }) => {

    await loginAsStandardUser(page);

    const inventory = new InventoryPage(page);

    await inventory.addProduct('Sauce Labs Backpack');

    await inventory.addProduct('Sauce Labs Bike Light');

    await inventory.openCart();

    const cart = new CartPage(page);

    await cart.removeProduct('Sauce Labs Backpack');

    await expect(cart.cartItems).toHaveCount(1);

    await expect(cart.cartItems).toContainText('Sauce Labs Bike Light');

    await expect(cart.cartItems).not.toContainText('Sauce Labs Backpack');

});


// TC18 - Checkout with Valid Details

test('AT07 - Verify checkout with valid customer information', async ({ page }) => {

    await loginAsStandardUser(page);

    const inventory = new InventoryPage(page);

    await inventory.addProduct('Sauce Labs Backpack');

    await inventory.openCart();

    const cart = new CartPage(page);

    await cart.checkout();

    const checkout = new CheckoutPage(page);

    await checkout.enterCustomerDetails('Nandhini', 'G', '641001');

    await expect(page).toHaveURL(/checkout-step-two.html/);

    await expect(page.locator('.summary_info')).toBeVisible();

    await expect(page.locator('.cart_item')).toContainText('Sauce Labs Backpack');

});


// TC23 - Complete Order

test('AT08 - Verify successful order placement', async ({ page }) => {

    await loginAsStandardUser(page);

    const inventory = new InventoryPage(page);

    await inventory.addProduct('Sauce Labs Backpack');

    await inventory.openCart();

    const cart = new CartPage(page);

    await cart.checkout();

    const checkout = new CheckoutPage(page);

    await checkout.enterCustomerDetails('Nandhini', 'G', '641001');

    await checkout.finishOrder();

    await expect(page).toHaveURL(/checkout-complete.html/);

    await expect(checkout.confirmationMessage)
        .toHaveText('Thank you for your order!');

});
