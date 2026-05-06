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
3. **Search for** "Contentsquare E-commerce" or browse the Analytics category
4. **Click on** "Contentsquare - E-commerce data" template
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

The transaction items section is optional but highly recommended for detailed product-level tracking. This functionality allows you to track individual products/items purchased within a transaction.

### Item Parameters

If implementing item-level tracking, the following data can be captured per item:

- **Product ID**: Unique identifier for the product
- **Product Name**: Name of the product
- **Category**: Product category
- **Price**: Unit price of the product
- **Quantity**: Number of units purchased

### Configuration

For detailed item-level implementation instructions:

1. **Contact your Implementation Manager** at Contentsquare
2. **Prepare your item data** in a structured array format
3. **Map item variables** in the template configuration
4. **Test item tracking** in GTM Preview mode

**Note**: Item tracking requires additional setup and coordination with your Contentsquare account team.

---

## Support & Documentation

### Official Resources

- **Contentsquare Website**: [https://contentsquare.com/](https://contentsquare.com/)
- **Documentation**: [https://docs.contentsquare.com/uxa-en/](https://docs.contentsquare.com/uxa-en/)
- **GTM Community Templates**: Available in Google Tag Manager's template gallery

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
| 1.2 | Current | Updated company logo |
| 1.1 | - | Removed Shipping and Tax fields |
| 1.0 | - | Updated Brand Name; Changed e-commerce tracking command; Added currency tracking |
| 0.1 | - | First Version |

**Recent Updates**:
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
