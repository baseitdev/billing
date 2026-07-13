<div align="center">

# @base/billing

**Payments made simple.**

![Discord](https://img.shields.io/discord/1492979180084920331?label=Discord&logo=Discord&logoColor=white&style=for-the-badge)
![GitHub contributors](https://img.shields.io/github/contributors/baseitdev/billing?style=for-the-badge)
![License](https://img.shields.io/github/license/baseitdev/billing?style=for-the-badge)

</div>

`@base/billing` is a modern payment library that provides a clean and unified API for integrating payment providers into your application.

Instead of learning different SDKs and APIs for every provider, you interact with a single interface while `@base/billing` handles the provider-specific implementation.

## Create a provider

Initialize the payment provider using your credentials.

```js
const billing = require("@base/billing");

const paybylink = await billing.provider({
    provider: "paybylink",
    shopId: "<SHOP_ID>",
    token: "<SHOP_TOKEN>"
});
```

Once initialized, the provider instance exposes all available payment methods.

---

## Create a payment

Creating a payment only requires the information related to the transaction.

```js
const payment = await paybylink.createPayment({
    price: 49.99,
    control: "ORDER_12345",
    description: "Premium subscription",
    email: "customer@example.com",
    notifyUrl: "https://example.com/api/payment/webhook",
    returnUrl: "https://example.com/payment/success"
});
```

The provider returns a payment object containing all information required to complete the transaction.

```js
console.log(payment);

{
    success: true,
    transactionId: "123456789",
    paymentUrl: "https://secure.paybylink.pl/transfer/123456789"
}
```

Redirect your customer to the returned `paymentUrl` to complete the payment.

---

## Philosophy

Every payment provider should feel the same.

Whether you're using PayByLink, Stripe, PayPal or another supported gateway, the developer experience remains consistent and predictable.

Write your payment logic once, change providers whenever you need.
