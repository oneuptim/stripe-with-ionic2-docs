
# [Stripe Payments with Ionic2](https://www.noodl.io/market/product/P201702241736843/stripe-with-ionic2-quickly-and-easily-integrate-stripe-in-your-ionic2-app) | Documentation

This is one of the most easy ways to start monetizing your Ionic2 app. The template contains the full source code for a payment form that processes payments using [Stripe](https://www.stripe.com). Stripe is the best software platform for running an internet business and handles billions of dollars every year.

Specifically, the template illustrates how to **1. validate the credit card details**, handle the response, and proceed with **2. charging the customer** using the validated token. The payment is immediately transferred to your Stripe account and is visible in your Dashboard, which allows you to also for instance make a refund or change the settings. The package also utilizes the power of [Noodlio Pay](https://www.noodliopay.com). With Noodlio Pay you don't have to setup and host your own payment server, you can simply make calls to the [API](https://market.mashape.com/noodlio/noodlio-pay-smooth-payments-with-stripe). Nevertheless, the documentation also explains how to setup your own payment server in case you would wish that, and how this package can help you achieve that with one line of code (simply point the payment `URL` to your server).

In summary:

- Add payments to your app or website
- Validate the credit card details
- Process payments
- [Support for almost any currency](https://support.stripe.com/questions/which-currencies-does-stripe-support)

In addition, with Stripe you can:

- View your payments
- Process refunds
- Prevent fraud
- [And much more](https://stripe.com/)

# Setup

There are two ways to use this package:

1. Start a new Ionic 2 project
2. Add payments to your current Ionic2 app

## 1. Start a new Ionic2 project
Since we are dealing with an Ionic app, you'll need to have Ionic, Cordova and Nodejs installed in your workspace. If you haven't already, please install the latest version of [Nodejs](http://nodejs.org/) first. Then install Ionic and Cordova as follows:

```
npm install -g cordova ionic
```

Then, create an Ionic App using one of the ready-made app templates, or a blank one to start fresh.

```
ionic start --v2 myApp tabs
```

You may wish to replace `tabs` with `blank` or `sidemenu`. Finally, run the app and open the live reload:

```
cd myApp
ionic serve
```

Once your app is initialized, follow the instructions in the next step.

## 2. Add payments to your current Ionic2 app

Next, extract the content `.zip` of this package. You'll find a folder named `pay`. Copy and paste this folder in your Ionic2 workspace under the location:

```
/src/pages
```

Next, add the dependencies in your app by visiting the file `/app/app.module.ts`. There, add at the top:

```
import { PayPage } from '../pages/pay/pay';
```

and under `declarations`:

```
declarations: [
  ...
  PayPage
],
```

and under `entryComponents`:

```
entryComponents: [
  ...
  PayPage
],
```

Finally, don't forget to add the route to the payment page. For instance, if you are using `tabs`, then head over to `/src/tabs/tabs.html` and add:

```
<ion-tab [root]="tab4Root" tabTitle="Pay" tabIcon="card"></ion-tab>
```

and in `/src/tabs/tabs.ts` add at the top:

```
import { PayPage } from '../pay/pay';
```

and finally within the class `TabsPage`:

```
tab4Root: any = PayPage;
```

## Cordova Whitelist

If you are dealing with Cordova 4.x or higher (which you probably are), then you'll also need to whitelist the server (thus where the payments are processed).

This can be solved quickly with the Cordova whitelist plugin! To install it, just run the following in your project's directory:

**Shell**
```
ionic plugin add https://github.com/apache/cordova-plugin-whitelist.git
```

Now, you just need to whitelist the relevant domains in your app's config.xml. For example, here's how you would whitelist all net traffic:

**XML**
```
<allow-navigation href="*" />
```

In addition, I add the following line of code to the file `/src/index.html`:

```
<!-- cordova whitelist -->
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-eval' 'unsafe-inline' *; object-src 'self'; style-src 'self' 'unsafe-inline'; media-src *">
```


Read more about Cordova and whitelisting  [here](http://legacy.docs.ionic.io/docs/cordova-whitelist).

## Setting up the payment server

There are two ways to setup your payment server. You can use Noodlio Pay (no server side setup needed) or host your own server.

### No server side setup

This is the easiest and cheapest option as you don't need to setup your own server and host it 24/7 (this costs money!).  In this setup, we simply need to obtain replace two constants in the file `/src/pages/pay/noodliopay.ts`:

```
private stripe_account    = "<STRIPE-ACCOUNT-ID>";
private mashape_key       = "<MASHAPE-KEY";
```

To obtain your `stripe_account` id, head over to the following pages:

*Development mode* [**https://www.noodl.io/pay/connect/test**](https://www.noodl.io/pay/connect/test)

and

*For the production mode:* [**https://www.noodl.io/pay/connect**](https://www.noodl.io/pay/connect)

Note, you'll need to visit both links once and register for a stripe account or simply login with your existing one. Both times, you'll obtain the same `stripe_account` id. What happens is that you connect your Stripe account to the Noodlio Pay Stripe Payments API, which simply replaces your server side and processes all the payments.

Next, obtain your `mashape_key` by registering on the following page:

[**https://market.mashape.com/noodlio/noodlio-pay-smooth-payments-with-stripe**](https://market.mashape.com/noodlio/noodlio-pay-smooth-payments-with-stripe)

The `mashape_key` is located under the property `X-Mashape-Key` (look for it using ctrl + f)

### Development mode vs production

When altering between the development mode and production mode, simply alter the variable (make sure it's always a string!) in the file `/src/pages/pay/noodliopay.ts`:

```
private test              = 'true'; // or 'false'
```

### Currency

You can change the currency of your payments in the file `/src/pages/pay/pay.ts` under:

```
inputForm = {
  currency: 'USD',
  ...
}
```

The list of supported currencies by Stripe can be found [here](https://support.stripe.com/questions/which-currencies-does-stripe-support).

### Custom payment server

For this, we recommend that you download the [Stripe Payments Kit](https://www.noodl.io/market/product/P201512041604740/stripe-payments-kit-server-side-api-to-process-all-payments-with-a-live-example-in-ionic) and follow the instructions on how to host your own server (thus only use the files in the folder `node-server-side`).

The documentations also explain how to host it to a VPS such as Heroku or Cloud9.

[**Download the server-side package here**](https://www.noodl.io/market/product/P201512041604740/stripe-payments-kit-server-side-api-to-process-all-payments-with-a-live-example-in-ionic)

<a href="https://www.noodl.io/market/product/P201512041604740/stripe-payments-kit-server-side-api-to-process-all-payments-with-a-live-example-in-ionic">
<img src="http://www.seipel-ibisevic.com/assets-external/stripe-charge/banner_inline.jpg">
</a>



