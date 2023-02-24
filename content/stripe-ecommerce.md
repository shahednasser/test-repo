---
title: 'Ecommerce with Stripe: How to guide'
date: '2023-02-22'
excerpt: >-
  Explore the benefits of using Stripe and Medusa, and learn how to set up a
  complete ecommerce store with Stripe and Medusa.
darkTheme: true
layout: PostLayout
bottomSections:
  - type: RecentPostsSection
    variant: variant-b
    colors: colors-a
    title: Want to know more about Medusa
    subtitle: Find related blog posts below
    recentCount: 6
    showExcerpt: true
    showImage: false
    styles:
      self:
        height: auto
        width: wide
        margin:
          - mt-0
          - mb-0
          - ml-0
          - mr-0
        padding:
          - pt-12
          - pb-20
          - 'sm:pb-56'
          - pr-4
          - pl-4
        justifyContent: center
      title:
        textAlign: center
      subtitle:
        textAlign: center
        color: grey-40
      actions:
        justifyContent: center
---

## Introduction


In today's digital age, it's crucial for businesses to have a seamless and secure payment system in place. Using an ecommerce platform that enables the integration of third-party payment providers like Stripe will simplify the payment process for customers and enhance the overall shopping experience, thereby increasing sales.


[Stripe](https://stripe.com/) is a widely-used payment gateway that offers a suite of payment APIs to help businesses accept payments online. Using a flexible ecommerce platform like [Medusa](https://docs.medusajs.com/introduction) to set up your ecommerce site could be a game changer. 


Medusa provides the building blocks to create an ecommerce system with the necessary components, including processing payments and handling customer data with other advanced features that come with it. 


In this tutorial, you will explore the benefits of using Stripe and Medusa, and learn how to set up a complete ecommerce store with Stripe and Medusa.


## What is Stripe?


[Stripe](https://medusajs.com/blog/nextjs-ecommerce-storefront-comes-packed-with-ready-integrations-to-paypal-meilisearch-stripe-and-more/) is one of the biggest payment providers supporting thousands of businesses in the United States and globally. It provides a platform for businesses to process online payments. Stripe offers tools and services for businesses to accept customer payments, including a payment gateway, a payment processor, and a suite of developer-friendly APIs.



Stripe supports a variety of payment methods, including credit cards, debit cards, Apple Pay, Google Pay, Microsoft Pay, Afterpay/Clearpay, Alipay, and ACH payments. Additionally, Stripe has fraud detection tools and can manage subscriptions and recurring payments. 


![](//hIxTvKUzeG.png)


Stripe is particularly popular among SMEs (Small and Medium-Sized Enterprises), developers, and online marketplaces. It is a good choice for ecommerce platforms looking to sell both locally and internationally. It provides tools for managing and analyzing transactions, as well as the ability to integrate with other software and services.


### Why Use Stripe?

- Easy Integration: Stripe offers easy integration with websites and mobile apps, allowing businesses to quickly and easily start accepting payments online.
- Security: Stripe is compliant with industry security standards and regulations, providing customers with a secure and reliable payment experience.
- Developer-Friendly API: Stripe is known for its developer-friendly API and robust documentation, making it a popular choice among businesses and developers of all sizes and industries.
- Global Coverage: Stripe supports payments in over 135+ currencies and can be used in over 40 countries, allowing businesses to easily expand to new markets and accept payments from customers around the world.

## What is Medusa?


[Medusa](https://docs.medusajs.com/introduction) is an open source, Node.ja-based, [composable commerce](https://medusajs.com/blog/composable-commerce/) engine. Its APIs can be integrated with frontend tools to create a scalable ecommerce store.


Medusa allows developers to build sophisticated commerce systems seamlessly. It’s great for developers who want full control over their development process. Medusa has three main components: the [headless](https://medusajs.com/blog/headless-architecture/) server, [the admin panel](https://docs.medusajs.com/admin/quickstart), and the storefront for speed enhancement.


![](//_TE-1gkvII.png)


Medusa is a highly customizable platform that allows for seamless integration with various third-party services. This allows users to utilize the best solutions available in different areas, maximizing efficiency and optimizing their workflow.


It has various features, including multiple payment options, a shopping cart, a [multi-currency feature](https://medusajs.com/blog/shopify-multi-currency-issue/), and third-party payment integration. Medusa commerce engine comes with a manual payment provider by default.


### Why Use Medusa?

- Advanced Ecommerce Features: Medusa provides some advanced ecommerce features such as multi-currency, automated RMA flows, and sales channels.
- Developer-Friendly Features: Medusa has a pre-built open source codebase that developers clone. It has every feature of advanced ecommerce already built into it.
- Flexible Backend: Medusa uses [Node.js backend](https://medusajs.com/blog/nodejs-ecommerce-backend/); it is built in such a way that developers can easily study, understand, and write new code for what they intend to achieve.
- Third-Party Integration: Medusa supports integration with other services through plugins, which add new features and functionality to the platform. Some examples of such services are [Segment](https://docs.medusajs.com/add-plugins/segment), [Contentful](https://docs.medusajs.com/add-plugins/contentful/customize-contentful), [PayPal](https://docs.medusajs.com/add-plugins/paypal), [Algolia](https://docs.medusajs.com/add-plugins/algolia), and more.

## Prerequisites


To follow through this tutorial effectively, ensure you have the following:

- [Node.js](https://nodejs.org/en/) version 14 or later
- [Stripe](https://stripe.com/) Account with API keys ready

## **How to Set up Medusa Ecommerce with Stripe**


For this tutorial, you will use the Medusa commerce engine to build an ecommerce store; this will enable you to utilize all prebuilt features of Medusa for an easy development process. You’ll use the Medusa Server, Medusa Admin, and Medusa Storefront. 


## **Create a Medusa Server Project**


To create your new Medusa project, follow the steps below:


### Install the Medusa CLI Tool


Medusa CLI gets your computer ready to run the Medusa codebase locally. You can run this command below to install it:


```bash
npm install @medusajs/medusa-cli -g
```


### Create a New Medusa Server


Creating a new Medusa project is simple; run the command below:


```bash
medusa new my-medusa-store --seed
```


`my-medusa-store` is the name of the project folder, so you can edit it as you wish. If you have completed the above step successfully, switch to your new project:


```bash
cd my-medusa-store
```


Next, start your Medusa server with the command below:


```bash
medusa develop
```


Medusa runs by default on port `9000`. You can navigate to `localhost:9000/store/products/` to see your store products.


### How to Install Medusa Stripe Plugin


The Stripe plugin is a package in Medusa that enables Stripe payment on your project. In the root of your Medusa project, run the following command to install the Stripe plugin:


```bash
npm install medusa-payment-stripe
```


Next, in your `.env` file, add the code snippet below:


```text
STRIPE_API_KEY=<STRIPE-API-KEY>
STRIPE_WEBHOOK_SECRET=<STRIPE-WEBHOOK-SECRET>
```


In the above code snippet, replace `<STRIPE-API-KEY>` and `<STRIPE-WEBHOOK-SECRET>`  with keys from your [Stripe dashboard](https://dashboard.stripe.com/test/apikeys).


### How to Configure Stripe in Medusa Server


Firstly, in `medusa-config.js`, add the following at the end of the `plugins` array:


```javascript
const plugins = [
  // ...
  {
    resolve: `medusa-payment-stripe`,
    options: {
      api_key: process.env.STRIPE_API_KEY,
      webhook_secret: process.env.STRIPE_WEBHOOK_SECRET,
    },
  },
]

```


### Create Medusa Admin


Medusa Admin is a component of Medusa that allows merchants to handle all administrative functions which include product management, order management, customer management, discounts, currencies, regions, prices, settings, and more.


The steps below will guide you in creating Medusa Admin:

1. Clone the Medusa Admin repository and switch the directory to the newly created folder:

	```bash
	git clone https://github.com/medusajs/admin medusa-admin
	cd medusa-admin
	```

2. Run the command below to install all necessary dependencies:

	```bash
	npm install
	```

3. Test it. Before you test the Medusa Admin, make sure your Medusa store server is running.

	```bash
	npm start
	```


By default, Medusa Admin runs on port `7000`; navigate to `localhost:7000`.


![](//BL1F2BNyuf.png)


Medusa has default admin login details: `admin@medusa-test.com` as the email address and `supersecret` as the password. The default admin credentials are added because you used the `--seed` option while installing the Medusa server.


### How to Enable Stripe in a Region


Before you can use Stripe as a payment option during the checkout process of your storefront, you need to add it as a payment provider to every region in your store. Medusa Region is used to control the market in which your store operates. It supports multiple countries, payment options, and currencies.


Follow the steps below to add Stripe in Medusa Region:

	1. On your Medusa Admin dashboard, go to _Settings → Regions_.

		![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5dc8ea70-1be5-4466-922b-98857738a189/s3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230224%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230224T133536Z&X-Amz-Expires=3600&X-Amz-Signature=fb284cb7fba880e4948c569a376e83b1e0a14884d49b63019ee943b927d9aaf2&X-Amz-SignedHeaders=host&x-id=GetObject)

	2. Click on the region you want to edit from the _Regions_ section. This enables you to edit different information and data related to the region.

		![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1a3f29c5-19b8-4848-b790-1a45f92e6366/s4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230224%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230224T133536Z&X-Amz-Expires=3600&X-Amz-Signature=f809aa7ea6ce7eaa93c32ef609522f905fc36101b60b160f0ca104a0354678ed&X-Amz-SignedHeaders=host&x-id=GetObject)

	3. Click on the three-dot icon at the top right of the selected region. Select _Edit Region Details_ from the dropdown. This opens a new window where you can edit the region's details.

		![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/65a41574-aff7-4101-a7ef-3bd988b500a4/s5.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230224%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230224T133537Z&X-Amz-Expires=3600&X-Amz-Signature=c8ac81c069ad5fe80058cc0fa355cfc436311a69e183297f11145fe0d850f98d&X-Amz-SignedHeaders=host&x-id=GetObject)

	4. Select Stripe as the only payment method from the _Payment Provider_ input field.

		![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bead4827-1279-41e8-a117-811af39b1baa/s6.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230224%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230224T133537Z&X-Amz-Expires=3600&X-Amz-Signature=1f5980349ad358392e2ef430982bbd203376d33da23ec659db14062b1928dde7&X-Amz-SignedHeaders=host&x-id=GetObject)

	5. Once done, click the _Save and close_ button.

_You can repeat the steps above for other regions as well._


## **Creating Medusa Storefront**


Medusa has prebuilt storefronts in two frameworks: [Next.js](https://docs.medusajs.com/starters/nextjs-medusa-starter) and [Gatsby](https://docs.medusajs.com/starters/gatsby-medusa-starter). This tutorial will focus on setting up a working storefront with Next.js and Stripe as its payment providers.


To create a Medusa Storefront, follow the steps below:

1. Create a new Next.js project using the [Medusa starter template](https://github.com/medusajs/nextjs-starter-medusa).

	```bash
	npx create-next-app -e https://github.com/medusajs/nextjs-starter-medusa my-medusa-storefront
	```

2. Switch to the newly created directory, `my-medusa-storefront`, and rename the template environment variable file to use environment variables in development:

	```bash
	cd my-medusa-storefront
	mv .env.template .env.local
	```


### Configure Stripe in Medusa Storefront


In your `.env.local` file (or the file you’re using for your environment variables), add the following variable:


```text
NEXT_PUBLIC_STRIPE_KEY=<YOUR_PUBLISHABLE_KEY>
```


Make sure to replace `<YOUR_PUBLISHABLE_KEY>` with your [Stripe Publishable Key](https://dashboard.stripe.com/test/apikeys).


## Test Stripe Payment


Before you test Stripe payment in your storefront, ensure your Medusa server is running. Run the command below to start your storefront:


```bash
npm run dev
```


After running the above command, navigate to `localhost:8000` to test your storefront. 


![](//J1XT_J45fN.png)


You can try adding products to your shopping cart and checkout; you should be able to pay with Stripe.


![](//hsQ5yPYGb3.png)


### Capturing the Payment from the Admin


When a payment is successfully made by a customer from your storefront, the payment is authorized but not captured. You’ll need to capture the payment from your admin panel.


Follow the steps below to capture payments:

1. In the admin, go to _Orders_ _⇒ Select the particular order._

	![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ecc36e71-5574-4706-a95c-ce973486bf0f/m2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230224%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230224T133539Z&X-Amz-Expires=3600&X-Amz-Signature=287ba26cdb642ab0ecc66f2ac0a343765a1e4941c226427ef6a5d07d7796c831&X-Amz-SignedHeaders=host&x-id=GetObject)

2. Scroll down the page to Payment Card and click on _Capture Payment._

	![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/af9f83cc-f380-4255-8135-cf2bf74201c7/m3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230224%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230224T133539Z&X-Amz-Expires=3600&X-Amz-Signature=8e80c42119c47d3ecddeea96e30ab9cd593834d72431411966a01295ee04a499&X-Amz-SignedHeaders=host&x-id=GetObject)


Once you capture the payment, the payment status will automatically turn to _Paid._ Next, you can check your Stripe dashboard to view the payment.


![](//0EbUgkcIAJ.png)


## Conclusion


This article explained what ecommerce is. It highlighted the features and benefits of Stripe and Medusa and showed a step-by-step guide to using Medusa ecommerce with Stripe. 


You can add the following integrations to your store:

- [Segment](https://docs.medusajs.com/add-plugins/segment) plugin for advanced analytics and tracking,
- [Mailchimp](https://docs.medusajs.com/add-plugins/mailchimp) for adding a newsletter subscription to your ecommerce store, and
- [Contentful](https://docs.medusajs.com/add-plugins/contentful/) for rich CMS functionalities such as two-way sync for the content, localization, versioning, and more.

You can learn more from [Medusa Documentation](https://docs.medusajs.com/introduction).


> Should you have any issues or questions related to Medusa, feel free to reach out to the Medusa team via [Discord](https://discord.gg/medusajs).

