# Payment Request

Many problems related to online shopping-cart abandonment can be traced to checkout forms, which can be difficult and time consuming to fill out and often require multiple steps to complete. The Payment Request API is meant to reduce the number of steps needed to complete a payment online, potentially doing away with checkout forms. It aims to make the checkout process easier, by remembering a user's details, which are then passed along to a merchant hopefully without requiring a HTML form.

Advantages of using the Payment Request API with "basic-card" (card-based payments):

Fast purchase experience: Users enter their details once into the browser and are then ready to pay for goods and services on the web. They no longer have to fill out the same details repeatedly across different sites.
Consistent experience on every site (that supports the API): As the payment sheet is controlled by the browser, it can tailor the experience to the user. This can include localizing the UI into the user's preferred language.
Accessibility: As the browser controls the input elements of the payment sheet, it can assure consistent keyboard and screen reader accessibility on every website without developers needing to do anything. A browser could also adjust the font size or color contrast of the payment sheet, making it more comfortable for the user to make a payment.
Credentials management: Users can manage their credit cards and shipping addresses directly in the browser. A browser can also sync these "credentials" across devices, making it easy for users to jump from desktop to mobile and back again when buying things.
Consistent error handling: The browser can check the validity of card numbers, and can tell the user if a card has expired (or is about to expire). The browser can automatically suggest which card to use based on past usage patterns or restrictions from the merchant (e.g, "we only accept Visa or Mastercard"), or allow the user to say which is their default/favorite card.
To request a payment, a web page creates a PaymentRequest object in response to a user action that initiates a payment, such as clicking a "Purchase" button. The PaymentRequest allows the web page to exchange information with the user agent while the user provides input to complete the transaction.

## Interfaces

### PaymentAddress

An object that contains address information; used for billing and shipping addresses, for example.

### PaymentRequest

An object that provides the API for creating and managing the user agent's payment interface.

### PaymentRequestEvent

An event delivered to a payment handler when a PaymentRequest is made.

### PaymentRequestUpdateEvent

Enables the web page to update the details of the payment request in response to a user action.

### PaymentMethodChangeEvent

Represents the user changing payment instrument (e.g., switching from a credit card to debit card).

### PaymentResponse

An object returned after the user selects a payment method and approves a payment request.
MerchantValidationEvent
Represents the browser requiring the merchant (website) to validate themselves as allowed to use a particular payment handler (e.g., registered as allowed to use Apple Pay).

## The basics of making a payment

This section details the basics of using the Payment Request API to make a payment.

Note: The code snippets from this section are from our Feature detect support demo.

#### Creating a new payment request object

A payment request always starts with the creation of a new PaymentRequest object — using the PaymentRequest() constructor. This takes two mandatory parameters and one option parameter:

methodData — an object containing information concerning the payment provider, such as what payment methods are supported, etc.
details — an object containing information concerning the specific payment, such as the total payment amount, tax, shipping cost, etc.
options (optional) — an object containing addtional options related to the payment.
So for example, you could create a new PaymentRequest instance like so:

```js
var request = new PaymentRequest(buildSupportedPaymentMethodData(),
                                 buildShoppingCartDetails());
The functions invoked inside the constructor simply return the required object parameters:

function buildSupportedPaymentMethodData() {
  // Example supported payment methods:
  return [{
    supportedMethods: 'basic-card',
    data: {
      supportedNetworks: ['visa', 'mastercard'],
      supportedTypes: ['debit', 'credit']
    }
  }];
}

function buildShoppingCartDetails() {
  // Hardcoded for demo purposes:
  return {
    id: 'order-123',
    displayItems: [
      {
        label: 'Example item',
        amount: {currency: 'USD', value: '1.00'}
      }
    ],
    total: {
      label: 'Total',
      amount: {currency: 'USD', value: '1.00'}
    }
  };
}
```

#### Starting the payment process

Once the PaymentRequest object has been created, you call the PaymentRequest.show() method on it to initiate the payment request. This returns a promise that fulfills with a PaymentResponse object if the payment is successful:

```js
request.show().then(function(paymentResponse) {
  // Here we would process the payment. For this demo, simulate immediate success:
  paymentResponse.complete("success").then(function() {
    // For demo purposes:
    introPanel.style.display = "none";
    successPanel.style.display = "block";
  });
});
```

This object provides the developer with access to details they can use to complete the logical steps required after the payment completes, such as an email address to contact the customer, a shipping address for mailing goods out to them, etc. In the code above, you'll see that we've called the PaymentResponse.complete() method to signal that the interaction has finished — you'd use this to carry out finishing steps, like updating the user interface to tell the user the transaction is complete, etc.

Other useful payment request methods
There are some other useful payment request methods worth knowing about.

PaymentRequest.canMakePayment() can be used to check whether the PaymentRequest object is capable of making a payment before you start the payment process. It returns a promise that fulfills with a boolean indicating whether it is or not, for example:

```js
// Dummy payment request to check whether payment can be made
new PaymentRequest(buildSupportedPaymentMethodData(), {
  total: { label: "Stub", amount: { currency: "USD", value: "0.01" } }
})
  .canMakePayment()
  .then(function(result) {
    if (result) {
      // Real payment request
      var request = new PaymentRequest(
        buildSupportedPaymentMethodData(),
        checkoutObject
      );

      request.show().then(function(paymentResponse) {
        // Here we would process the payment.
        paymentResponse.complete("success").then(function() {
          // Finish handling payment
        });
      });
    }
  });
```

PaymentRequest.abort() can be used to abort the payment request if required.

Detecting availability of the Payment Request API
You can effectively detect support for the Payment Request API by checking if the user's browser supports PaymentRequest, i.e. if (window.PaymentRequest).

In the following snippet, a merchant page performs this check, and if it returns true updates the checkout button to use PaymentRequest instead of legacy web forms.

```js
const checkoutButton = document.getElementById("checkout-button");
if (window.PaymentRequest) {
  let request = new PaymentRequest(
    buildSupportedPaymentMethodNames(),
    buildShoppingCartDetails()
  );
  checkoutButton.addEventListener("click", function() {
    request
      .show()
      .then(function(paymentResponse) {
        // Handle successful payment
      })
      .catch(function(error) {
        // Handle cancelled or failed payment. For example, redirect to
        // the legacy web form checkout:
        window.location.href = "/legacy-web-form-checkout";
      });
    // Every click on the checkout button should use a new instance of
    // PaymentRequest object, because PaymentRequest.show() can be
    // called only once per instance.
    request = new PaymentRequest(
      buildSupportedPaymentMethodNames(),
      buildShoppingCartDetails()
    );
  });
}
```
