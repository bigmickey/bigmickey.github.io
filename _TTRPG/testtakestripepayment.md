---
title: "Test taking a payment"
date: 2020-09-19
---

Lets's see if I can take a payment ..

<!-- Load Stripe.js on your website. -->
<script src="https://js.stripe.com/v3"></script>

<!-- Create a button that your customers click to complete their purchase. Customize the styling to suit your branding. -->
<button style="background-color:#6772E5;color:#FFF;padding:8px 12px;border:0;border-radius:4px;font-size:1em" id="checkout-button-price_1HSxR9JXz6foPx50VQp3gg0F" role="link" type="button" >
  Checkout
</button>

<div id="error-message"></div>

<script>
(function() {
  var stripe = Stripe('pk_test_51HSxCEJXz6foPx50Cr5SBaeoCihBRrZaOVuZZJ4EmDEMQ9bUBbk5wR2sFIzOmG9LrwqZ1SDGVgWXr4gYeRZzynp1001AvI1jsv'); 
  var checkoutButton = document.getElementById('checkout-button-price_1HSxR9JXz6foPx50VQp3gg0F');
  checkoutButton.addEventListener('click', function () {
    // When the customer clicks on the button, redirect
    // them to Checkout.
    stripe.redirectToCheckout({
      lineItems: [{price: 'price_1HSxR9JXz6foPx50VQp3gg0F', quantity: 1}],
      mode: 'payment',
      // Do not rely on the redirect to the successUrl for fulfilling
      // purchases, customers may not always reach the success_url after
      // a successful payment.
      // Instead use one of the strategies described in
      // https://stripe.com/docs/payments/checkout/fulfill-orders
      successUrl: 'https://bigmickey.github.com/success',
      cancelUrl: 'https://bigmickey.github.com/cancel',
    })
    .then(function (result) {
      if (result.error) {
        // If `redirectToCheckout` fails due to a browser or network
        // error, display the localized error message to your customer.
        var displayError = document.getElementById('error-message');
        displayError.textContent = result.error.message;
      }
    });
  });
})();
</script>
