# Contentsquare E-commerce Tag for Google Tag Manager

**Collect and send transaction data from your e-commerce site to your Contentsquare instance.**

This Google Tag Manager template simplifies the integration of Contentsquare e-commerce tracking into your website, enabling automatic collection of purchase transaction data for advanced analytics and insights.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Configuration](#configuration)
- [Parameters](#parameters)
- [Transaction Items](#transaction-items)
- [Support & Documentation](#support--documentation)
- [Version History](#version-history)
- [License](#license)

---

## Overview

The **Contentsquare E-commerce Tag** is a Google Tag Manager community template that enables seamless tracking of e-commerce transactions within the Contentsquare platform. This template automates the collection of transaction-level data including order ID, revenue, currency, and individual product/item details.

### What is Contentsquare?

Contentsquare is a digital experience analytics platform that helps businesses understand how users interact with their digital properties. With e-commerce tracking enabled, you can correlate user behavior with purchase events to optimize conversion funnels and improve customer experience.

---

## Features

- **Automated Transaction Tracking**: Captures transaction data with minimal setup
- **Mandatory Parameter Support**: Enforces collection of critical transaction metrics (Transaction ID and Revenue)
- **Optional Parameters**: Supports optional fields like currency code for more granular tracking
- **Item-Level Tracking**: Track individual products/items within transactions
- **Flexible Item Field Mapping**: Works out of the box with standard GA4/GTM item property names, or lets you map custom property names if your dataLayer uses a non-standard naming convention
- **Easy Configuration**: Simple parameter mapping through GTM interface
- **Supports Multiple Data Types**: Works with all standard GTM variable types

---

## Installation

### Prerequisites

- Active Google Tag Manager container with web container type
- Access to your website's confirmation/thank-you page
- Variables defined for transaction data (see [Configuration](#configuration))
- Contentsquare account with e-commerce tracking enabled

### Installation Steps

1. **Open Google Tag Manager** and navigate to your container
2. **Go to Templates** > **Tag Templates** > **Search Gallery**
3. **Search for** "Contentsquare Ecommerce" or browse the Analytics category
4. **Click on** "Contentsquare - Ecommerce/Merchandising" template
5. **Click Add to Workspace** to import the template
6. **Accept** the Community Template Gallery Developer Terms of Service
7. **Create a New Tag** using this template in your container

---

## Configuration

### Basic Setup

After creating a new tag with this template:

1. **Name your tag** (e.g., "Contentsquare - Purchase Transaction")
2. **Map your GTM variables** to the template parameters (see [Parameters](#parameters) section)
3. **Set your trigger** to fire on your confirmation/thank-you page
   - Recommended trigger: "Page View - Confirmation Page" or "Custom Event"
4. **Test the tag** using GTM Preview mode
5. **Publish** the container once validated

### Trigger Configuration

The tag should fire on your e-commerce confirmation page. Common trigger configurations:

- **Page Path matches regex** `/(confirmation|thank-you|order-received)/`
- **Event name equals** `purchase` (if using GA4 or custom event)
- **Custom event** when order data becomes available on page

---

## Parameters

### Mandatory Parameters

These parameters **must** be configured for the tag to function properly:

| Parameter | Description | Data Type | Example |
|-----------|-------------|-----------|---------|
| **Transaction ID** | Unique identifier for the transaction/order | String | `ORD-12345` |
| **Revenue** | Total transaction revenue/order amount | Number | `99.99` |

**Note**: Transaction ID must be unique per transaction. Revenue should be the total order value, typically in the site's default currency.

### Optional Parameters

These parameters are optional and can enhance your tracking:

| Parameter | Description | Data Type | Example |
|-----------|-------------|-----------|---------|
| **ISO Currency Code** | 3-letter ISO 4217 currency code | String | `USD`, `EUR`, `GBP` |

**Supported Currencies**: Any valid ISO 4217 currency code (e.g., USD, EUR, GBP, JPY, etc.)

---

## Transaction Items

### Overview

The transaction items section is optional but highly recommended for detailed product-level tracking. This functionality loops through an array of purchased items and sends each one to Contentsquare individually, right before the transaction is sent.

### Item Parameters

Map the **Transaction Items** field (under the **Purchased Products** group) to a variable (e.g. a Custom JavaScript Variable) that returns an array of item objects. By default, each item object is expected to use the standard naming convention from Google's [GA4 ecommerce `items` array](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce):

| Field | Description | Required |
|-------|-------------|----------|
| **item_id** | Product code / SKU (string) | Yes |
| **price** | Unit price actually paid (string/number) | Yes |
| **quantity** | Quantity | Yes |
| **item_name** | Product name (string) | Yes |
| **item_category** | Product category (string) | No |

### Custom Item Field Names

If your dataLayer doesn't follow the standard `item_id` / `item_name` / `item_category` / `price` / `quantity` naming convention, you can tell the tag which property to read for each field instead of renaming your dataLayer. Under **Purchased Products**, fill in any of these optional text fields with the actual property name used in your item objects:

| Parameter | Overrides property | Example |
|-----------|--------------------|---------|
| **Product ID (SKU)** | `item_id` | `sku` |
| **Product Name** | `item_name` | `productName` |
| **Product Category (optional)** | `item_category` | `productCategory` |
| **Product Price** | `price` | `unitPrice` |
| **Product Quantity** | `quantity` | `qty` |

Any field left blank falls back to the standard property name.

### Configuration

1. **Build a variable** (typically a Custom JavaScript Variable) that reads your ecommerce dataLayer and returns an array shaped like:
   ```js
   [
     { item_id: "123ABC", price: "9.99", quantity: "1", item_name: "Black scarf", item_category: "Scarves" },
     { item_id: "456DEF", price: "19.99", quantity: "2", item_name: "Red beanie", item_category: "Hats" }
   ]
   ```
   If your items use different property names (e.g. `sku` instead of `item_id`), keep the array shaped however your dataLayer already provides it and set the matching override in [Custom Item Field Names](#custom-item-field-names) instead of transforming the data.
2. **Map that variable** to the **Transaction Items** parameter in the tag configuration
3. **Test item tracking** in GTM Preview mode - each item is pushed via `ec:transaction:items:add` before the final `ec:transaction:send`

**Note**: Leave the Transaction Items field empty to skip item-level tracking.

---

## Support & Documentation

### Official Resources

- **Contentsquare Website**: [https://contentsquare.com/](https://contentsquare.com/)
- **Documentation**: [https://docs.contentsquare.com/uxa-en/](https://docs.contentsquare.com/uxa-en/)
- **GTM Community Templates**: Available in Google Tag Manager's template gallery
- **GA4 Ecommerce `items` array reference**: [https://developers.google.com/analytics/devguides/collection/ga4/ecommerce](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce) - the standard `item_id`/`item_name`/`item_category`/`price`/`quantity` naming convention used by this template's [Transaction Items](#transaction-items) parameter is based on this Google format

### Getting Help

For implementation support or questions:

1. **Review Contentsquare Documentation**: Check the official docs for e-commerce tracking guidelines
2. **Contact Your Implementation Manager**: Available through your Contentsquare account team
3. **Check GTM Logs**: Use the GTM debug console to verify tag firing and variable mapping
4. **Test in Preview Mode**: Use GTM Preview mode before publishing changes

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.3 | Current | Renamed template to "Contentsquare - Ecommerce/Merchandising"; added item-level tracking (loops through a Transaction Items array and sends each item before the transaction) with support for custom item property name mapping |
| 1.2 | - | Updated company logo |
| 1.1 | - | Removed Shipping and Tax fields |
| 1.0 | - | Updated Brand Name; Changed e-commerce tracking command; Added currency tracking |
| 0.1 | - | First Version |

**Recent Updates**:
- Renamed the template in the Community Template Gallery to "Contentsquare - Ecommerce/Merchandising"
- Added item-level tracking via a new Transaction Items parameter
- Added support for mapping custom item property names (for dataLayers that don't follow the standard `item_id`/`item_name`/`item_category`/`price`/`quantity` naming)
- Updated company logo for brand consistency
- Removed Shipping and Tax parameters (use Revenue for total)
- Enhanced currency support with ISO currency codes
- Improved parameter validation

---

## License

By creating or modifying this template, you agree to [Google Tag Manager's Community Template Gallery Developer Terms of Service](https://developers.google.com/tag-manager/gallery-tos).

This template is provided by Contentsquare and maintained in the Google Tag Manager Community Template Gallery.

---

## Quick Start Example

### Step 1: Create GTM Variables

In your GTM container, create the following variables from your dataLayer:

```
Variable Name: Transaction ID
Type: Data Layer Variable
Data Layer Variable Name: transactionId

Variable Name: Order Revenue
Type: Data Layer Variable
Data Layer Variable Name: orderRevenue

Variable Name: Currency Code
Type: Data Layer Variable
Data Layer Variable Name: currencyCode
```

### Step 2: Configure the Tag

1. Create a new tag using the Contentsquare E-commerce template
2. Set Transaction ID → `{{Transaction ID}}`
3. Set Revenue → `{{Order Revenue}}`
4. Set Currency Code → `{{Currency Code}}`
5. Create a trigger for your confirmation page

### Step 3: Test

1. Enable GTM Preview mode
2. Complete a test purchase on your site
3. Check the GTM console for tag firing
4. Verify data in your Contentsquare account

---

For additional questions or advanced implementations, reach out to your Contentsquare account team or implementation manager.
