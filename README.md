## **How to Use Gigit Web Components in Your Store**

Follow these steps to integrate individual components into your store.

---

### **1. Include the JavaScript Component File**

Add the following `<script>` tag to the HTML page where you want to use the components. Place it at the bottom of the `<body>` element for optimal performance.

```html
<script src="provided-link-to-js-file" type="module" async></script>
```

#### **For Shopify Stores**

On Shopify, add this script to `layout/theme.liquid` or any other **Liquid file that wraps your store** or the specific pages where the components will be used.

Example (`theme.liquid`):

```html
<script src="provided-link-to-js-file" type="module" async></script>
```

---

## **Component Usage**

### **Gigit QA Widget**

The QA Widget enables AI-powered Q&A for answering customer questions.

#### **Usage in HTML**

```html
<gigit-qa-widget
    shop="shop-domain"
    producttitle="Product Title"
    productid="123"
    test="true"
></gigit-qa-widget>
```

#### **Usage in Shopify Liquid**

```html
<gigit-qa-widget
    shop="{{ shop.permanent_domain }}"
    producttitle="{{ product.title | escape }}"
    productid="{{ product.id }}"
    test="true"
>
</gigit-qa-widget>
```

#### **Props**

| **Attribute**     | **Required?** | **Type** | **Description**                                                |
| ----------------- | ------------- | -------- | -------------------------------------------------------------- |
| `shop`            | ✅ Yes        | `string` | The domain of your store.                                      |
| `producttitle`    | Optional      | `string` | The name of the product.                                       |
| `productid`       | Optional      | `string` | Enables product-specific chat if provided.                     |
| `productspecific` | Optional      | `bool`   | If set to `true`, each product will have its own chat channel. |
| `test`            | Optional      | `bool`   | If set to `true`, interactions will not be logged.             |
| `locale`          | Optional      | `string` | The language of the QA Widget. For example, `en` or `ar`.      |

---

### **Gigit QA Widget Entrypoint**

The QA Widget Entrypoint will scroll the screen to the QA Widget when clicked.

#### **Usage in HTML**

```html
<gigit-qa-widget-entrypoint
    shop="shop-domain"
    producttitle="Product Title"
    productid="123"
    test="true"
></gigit-qa-widget-entrypoint>
```

#### **Usage in Shopify Liquid**

```html
<gigit-qa-widget-entrypoint
    shop="{{ shop.permanent_domain }}"
    producttitle="{{ product.title | escape }}"
    productid="{{ product.id }}"
    test="true"
>
</gigit-qa-widget-entrypoint>
```

#### **Props**

| **Attribute**  | **Required?** | **Type**  | **Description**                                                      |
| -------------- | ------------- | --------- | -------------------------------------------------------------------- |
| `shop`         | ✅ Yes        | `string`  | The domain of your store.                                            |
| `producttitle` | Optional      | `string`  | The name of the product.                                             |
| `productid`    | Optional      | `string`  | Enables product-specific chat if provided.                           |
| `test`         | Optional      | `boolean` | If set to `true`, interactions will not be logged.                   |
| `locale`       | Optional      | `string`  | The language of the QA Widget Entrypoint. For example, `en` or `ar`. |

---

### **Gigit Highlights**

The Highlights component displays key product features.

#### **Usage in HTML**

```html
<gigit-highlights
    shop="shop-domain"
    producttitle="Product Title"
    preview="true"
></gigit-highlights>
```

#### **Usage in Shopify Liquid**

```html
<gigit-highlights
    shop="{{ shop.permanent_domain }}"
    producttitle="{{ product.title | escape }}"
    preview="true"
>
</gigit-highlights>
```

#### **Props**

| **Attribute**  | **Required?** | **Type**  | **Description**                                            |
| -------------- | ------------- | --------- | ---------------------------------------------------------- |
| `shop`         | ✅ Yes        | `string`  | The domain of your store.                                  |
| `producttitle` | ✅ Yes        | `string`  | The name of the product.                                   |
| `preview`      | Optional      | `boolean` | Enables design preview mode.                               |
| `locale`       | Optional      | `string`  | The language of the Highlights. For example, `en` or `ar`. |

---

### **Gigit Smart Menu**

The Smart Menu enhances navigation for a better shopping experience.

#### **Usage in HTML**

```html
<gigit-smart-menu shop="shop-domain"></gigit-smart-menu>
```

#### **Usage in Shopify Liquid**

```html
<gigit-smart-menu shop="{{ shop.permanent_domain }}"></gigit-smart-menu>
```

#### **Props**

| **Attribute** | **Required?** | **Type** | **Description**                                           |
| ------------- | ------------- | -------- | --------------------------------------------------------- |
| `shop`        | ✅ Yes        | `string` | The domain of your store.                                 |
| `pageType`    | Optional      | `string` | Page type: `index`, `product` or `collection`.            |
| `locale`      | Optional      | `string` | The language of the SmartMenu. For example, `en` or `ar`. |

---

### **Gigit Shop Concierge**

The Shop Concierge provides AI-driven customer assistance.

#### **Usage in HTML**

```html
<gigit-shop-concierge shop="shop-domain" test="true"></gigit-shop-concierge>
```

#### **Usage in Shopify Liquid**

```html
<gigit-shop-concierge
    shop="{{ shop.permanent_domain }}"
    test="true"
></gigit-shop-concierge>
```

#### **Props**

| **Attribute** | **Required?** | **Type**  | **Description**                                                |
| ------------- | ------------- | --------- | -------------------------------------------------------------- |
| `shop`        | ✅ Yes        | `string`  | The domain of your store.                                      |
| `test`        | Optional      | `boolean` | If set to `true`, interactions will not be logged.             |
| `pageType`    | Optional      | `string`  | Page type: `index`, `product` or `collection`.                 |
| `locale`      | Optional      | `string`  | The language of the Shop Concierge. For example, `en` or `ar`. |

---

## **Data Tracking for Analytics**

`GigitApps` is a global object that provides tracking functionality for user interactions in your store. It allows developers to log important actions such as adding a product to the cart or completing a checkout.

`GigitApps` does not track events automatically (except page views). **The developer must manually call `GigitApps.trackEvent`** when relevant user actions occur.

---

## **Tracking Events with GigitApps.trackEvent**

`GigitApps.trackEvent(eventType, eventData)` is used to send event tracking data.

-   **`eventType` (string, required)** → The name of the event (e.g., `"ADD_TO_CART"`).
-   **`eventData` (object, optional)** → Additional details about the event.

---

### **1. `ADD_TO_CART` Event**

`ADD_TO_CART` must be called when a user adds a product to the cart.

#### **Example:**

```html
<script>
    function addToCart(productId, title, quantity, price, currency) {
        window.GigitApps.trackEvent('ADD_TO_CART', {
            productId: productId,
            productTitle: title,
            quantity: quantity,
            totalPrice: price,
            currency: currency,
        })
    }
</script>
```

#### **Parameters:**

| **Parameter**  | **Required?** | **Type** | **Description**                    |
| -------------- | ------------- | -------- | ---------------------------------- |
| `productId`    | ✅ Yes        | `string` | Unique identifier for the product. |
| `productTitle` | ✅ Yes        | `string` | Name of the product.               |
| `quantity`     | ✅ Yes        | `number` | Number of items added.             |
| `totalPrice`   | ✅ Yes        | `number` | Total cost of the added items.     |
| `currency`     | ✅ Yes        | `string` | Currency code (e.g., `"USD"`).     |
| `custom`       | Optional      | `object` | Any additional custom data.        |

---

### **2. `CHECKOUT_COMPLETED` Event**

`CHECKOUT_COMPLETED` must be triggered after the checkout process is finalized. This should happen in a callback, promise, or after an API request confirms the order.

#### **Example:**

```html
<script>
    function onCheckoutSuccess(orderData) {
        window.GigitApps.trackEvent('CHECKOUT_COMPLETED', {
            currencyCode: orderData.currency,
            totalPrice: orderData.totalPrice,
            email: orderData.customerEmail,
            phone: orderData.customerPhone,
            order: {
                id: orderData.id,
                customerId: orderData.customerId,
            },
            lineItems: orderData.items.map((item) => ({
                productId: item.id,
                productTitle: item.title,
                quantity: item.quantity,
                price: item.price,
            })),
        })
    }
</script>
```

#### **Parameters:**

| **Parameter**              | **Required?** | **Type** | **Description**                                                                             |
| -------------------------- | ------------- | -------- | ------------------------------------------------------------------------------------------- |
| `currencyCode`             | ✅ Yes        | `string` | Currency code (e.g., `"USD"`).                                                              |
| `totalPrice`               | ✅ Yes        | `number` | The total amount of the completed checkout.                                                 |
| `order.id`                 | ✅ Yes        | `string` | The id of the order                                                                         |
| `order.customerId`         | Optional      | `string` | The id of the customer                                                                      |
| `email`                    | Optional      | `string` | Customer's email (if available).                                                            |
| `phone`                    | Optional      | `string` | Customer's phone number (if available).                                                     |
| `lineItems`                | ✅ Yes        | `array`  | List of purchased products, including `productId`, `productTitle`, `quantity`, and `price`. |
| `lineItems[].productId`    | ✅ Yes        | `string` | The product ID for each item in the order.                                                  |
| `lineItems[].productTitle` | ✅ Yes        | `string` | The name of the product.                                                                    |
| `lineItems[].quantity`     | ✅ Yes        | `number` | The quantity purchased.                                                                     |
| `lineItems[].price`        | Optional      | `number` | The price of the product.                                                                   |

---

### **3. Ensuring GigitApps.trackEvent is Available**

Since the script loads asynchronously, developers should **check if `trackEvent` is available before calling it**:

```js
if (window.GigitApps?.trackEvent) {
    window.GigitApps.trackEvent('ADD_TO_CART', {
        productId: '123',
        productTitle: 'Test Product',
        quantity: 1,
        totalPrice: 49.99,
        currency: 'USD',
    })
} else {
    console.warn('GigitApps.trackEvent is not available yet.')
}
```
