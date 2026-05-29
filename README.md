## **How to Use Gigit Web Components in Your Store**

Follow these steps to integrate individual components into your store.

---

### **1. Include the JavaScript Component File**

Add the following `<script>` tag to the HTML page where you want to use the components. Place it at the bottom of the `<body>` element for optimal performance.

```html
<script src="provided-script-url" type="module" async></script>
```

The script URL will be shared with you during onboarding. You can also pin to a specific version if needed.

#### **For Non-Shopify Platforms**

For stores not on Shopify, use your store's domain (e.g., `www.yourbrand.com`) as the `shop` attribute value. The script and components work the same way — add the script to your site's HTML and place components where needed.

#### **For Shopify Stores (Native Liquid Themes)**

On Shopify, add this script to `layout/theme.liquid` or any other **Liquid file that wraps your store** or the specific pages where the components will be used.

Example (`theme.liquid`):

```html
<script src="provided-script-url" type="module" async></script>
```

#### **For Shopify Stores Using Page Builders (e.g., Replo)**

If you're using a page builder on Shopify, the Gigit app is installed through the Shopify App Store as usual (this gives you the core backend, analytics, and checkout pixel). The web component script handles the frontend rendering.

**Setup Steps:**

1. **Install the Gigit Shopify App** — this installs the backend services, event tracking pixel, and analytics infrastructure.
2. **Add the web component script** — insert the script tag in your page builder's custom code section (usually in the `<head>` or before `</body>`):
   ```html
   <script src="provided-script-url" type="module" async></script>
   ```
3. **Place web components** — use the custom HTML elements documented below anywhere in your page builder's layout.

**Where to add the script in your page builder:**

| Page Builder | Where to Add Script |
| ------------ | ------------------- |
| **Replo** | Page Settings → Custom Code → Footer Code |

**Important Notes for Page Builder Users:**

- The Gigit Shopify app must be installed on your store for authentication and backend services.
- The web component script works independently of Shopify's theme extension system — no theme blocks needed.
- Analytics events (`ADD_TO_CART`, `CHECKOUT_COMPLETED`) must be tracked manually using `GigitApps.trackEvent` (see [Data Tracking](#data-tracking-for-analytics) section below).
- The checkout pixel is installed automatically via the Shopify app — no additional setup needed for conversion tracking.

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

| **Attribute**        | **Required?** | **Type** | **Description**                                                                                                               |
| -------------------- | ------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `shop`               | ✅ Yes        | `string` | Your store's domain (e.g., `your-store.myshopify.com` for Shopify, or your store domain for non-Shopify platforms).           |
| `producttitle`       | Optional      | `string` | The name of the product.                                                                                                      |
| `productid`          | Optional      | `string` | Enables product-specific chat if provided.                                                                                    |
| `productdescription` | Optional      | `string` | The description of the product. Required on product pages.                                                                    |
| `productspecific`    | Optional      | `string` | If set to `false` (string),disables product-specific chat channels. Default is enabled when omitted.                          |
| `test`               | Optional      | `string` | If set to `true` (string), interactions will not be logged.                                                                   |
| `locale`             | Optional      | `string` | The language of the QA Widget. For example, `en` or `ar`.                                                                     |
| `storetype`          | Optional      | `string` | If the value is `playground`, this store will be a playground store.                                                          |
| `storeindustry`      | Optional      | `string` | Provide industry context for playground stores. This is required if `storetype` is `playground`. Possible values: `skincare`. |

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

| **Attribute**        | **Required?** | **Type** | **Description**                                                                                                               |
| -------------------- | ------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `shop`               | ✅ Yes        | `string` | The domain of your store.                                                                                                     |
| `producttitle`       | Optional      | `string` | The name of the product. Required on product pages (for inline type - simple QA widget).                                      |
| `productid`          | Optional      | `string` | Enables product-specific chat if provided. Required on product pages (for inline type - simple QA widget).                    |
| `productdescription` | Optional      | `string` | The description of the product. Required on product pages (for inline type - simple QA widget).                               |
| `test`               | Optional      | `string` | If set to `true` (string), interactions will not be logged.                                                                   |
| `locale`             | Optional      | `string` | The language of the QA Widget Entrypoint. For example, `en` or `ar`.                                                          |
| `storetype`          | Optional      | `string` | If the value is `playground`, this store will be a playground store.                                                          |
| `storeindustry`      | Optional      | `string` | Provide industry context for playground stores. This is required if `storetype` is `playground`. Possible values: `skincare`. |

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

| **Attribute**        | **Required?** | **Type**  | **Description**                                                                                                               |
| -------------------- | ------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `shop`               | ✅ Yes        | `string`  | The domain of your store.                                                                                                     |
| `producttitle`       | ✅ Yes        | `string`  | The name of the product.                                                                                                      |
| `productdescription` | ✅ Yes        | `string`  | The description of the product.                                                                                               |
| `preview`            | Optional      | `boolean` | Enables design preview mode.                                                                                                  |
| `locale`             | Optional      | `string`  | The language of the Highlights. For example, `en` or `ar`.                                                                    |
| `storetype`          | Optional      | `string`  | If the value is `playground`, this store will be a playground store.                                                          |
| `storeindustry`      | Optional      | `string`  | Provide industry context for playground stores. This is required if `storetype` is `playground`. Possible values: `skincare`. |

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

| **Attribute**   | **Required?** | **Type** | **Description**                                                                                                               |
| --------------- | ------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `shop`          | ✅ Yes        | `string` | The domain of your store.                                                                                                     |
| `pageType`      | Optional      | `string` | Page type: `index`, `product` or `collection`.                                                                                |
| `locale`        | Optional      | `string` | The language of the SmartMenu. For example, `en` or `ar`.                                                                     |
| `test`          | Optional      | `string` | If set to `true` (string), interactions will not be logged.                                                                   |
| `storetype`     | Optional      | `string` | If the value is `playground`, this store will be a playground store.                                                          |
| `storeindustry` | Optional      | `string` | Provide industry context for playground stores. This is required if `storetype` is `playground`. Possible values: `skincare`. |

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

| **Attribute**   | **Required?** | **Type** | **Description**                                                                                                               |
| --------------- | ------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `shop`          | ✅ Yes        | `string` | The domain of your store.                                                                                                     |
| `test`          | Optional      | `string` | If set to `true` (string), interactions will not be logged.                                                                   |
| `pageType`      | Optional      | `string` | Page type: `index`, `product` or `collection`.                                                                                |
| `locale`        | Optional      | `string` | The language of the Shop Concierge. For example, `en` or `ar`.                                                                |
| `storetype`     | Optional      | `string` | If the value is `playground`, this store will be a playground store.                                                          |
| `storeindustry` | Optional      | `string` | Provide industry context for playground stores. This is required if `storetype` is `playground`. Possible values: `skincare`. |

---

### **Gigit Storefront Agent**

The Storefront Agent dynamically renders personalized content based on visitor context (device, visitor type, UTM parameters, page type). It supports multiple content types including text, images, banners, and custom HTML.

#### **Site-Wide Deployment**

Place a single element in your site layout (e.g., `theme.liquid` or global footer). It auto-detects the current page and applies configured behaviors — no per-page agent ID needed.

```html
<gigit-storefront-agent shop="your-store.myshopify.com"></gigit-storefront-agent>
```

In Shopify Liquid (`theme.liquid`):

```html
<gigit-storefront-agent
    shop="{{ shop.permanent_domain }}"
></gigit-storefront-agent>
```

#### **Per-Page Deployment (Required for visible content types)**

For content types that render visible output (text, image, banner, custom_html), pass the `agentid` explicitly and place the element where the content should appear:

```html
<gigit-storefront-agent
    agentid="your-agent-id"
    shop="your-store.myshopify.com"
    pagetype="index"
></gigit-storefront-agent>
```

#### **Usage in Page Builders (e.g., Replo)**

Place the custom HTML element in any section of your page builder where you want dynamic content to appear:

```html
<gigit-storefront-agent
    agentid="your-agent-id"
    shop="your-store.myshopify.com"
    pagetype="product"
    productid="123456789"
    producttitle="Product Name"
></gigit-storefront-agent>
```

#### **Props**

| **Attribute**  | **Required?** | **Type** | **Description**                                                                                  |
| -------------- | ------------- | -------- | ------------------------------------------------------------------------------------------------ |
| `shop`         | ✅ Yes        | `string` | Your store's domain (e.g., `your-store.myshopify.com` for Shopify, or your store domain for non-Shopify platforms). |
| `agentid`      | Optional      | `string` | Agent ID from the Gigit Dashboard. If omitted, auto-detects agents for the current page URL.     |
| `pagetype`     | Optional      | `string` | Page type context: `index`, `product`, `collection`, `page`, `blog`, `cart`. Defaults to `index`. |
| `productid`    | Optional      | `string` | The product ID. Required on product pages for product-aware behaviors.                           |
| `producttitle` | Optional      | `string` | The product title. Required on product pages for product-aware behaviors.                        |

#### **Content Types**

The Storefront Agent supports the following content types (configured in the Gigit Dashboard):

| Content Type   | Description                                                              |
| -------------- | ------------------------------------------------------------------------ |
| `text`         | Renders text or HTML content. Supports styled text with custom fonts.    |
| `image`        | Renders a responsive image (separate mobile/desktop URLs supported).     |
| `banner`       | Full-width banner with optional overlay title.                           |
| `custom_html`  | Renders arbitrary HTML content.                                          |

Analytics events are tracked automatically.

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
