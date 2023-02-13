---
title: 'Vercel Ecommerce: Ecommerce store with Next.js + Medusa + Stripe'
date: '2023-02-13'
excerpt: ''
darkTheme: true
layout: 'PostLayout'
---

## Introduction


When it comes to setting up an online store, finding the right hosting provider is essential. A reliable host can ensure that your website stays up and running, even during periods of high traffic. [Vercel](https://vercel.com/) is a hosting provider optimized for performance and scalability; it's a great choice for ecommerce storefronts.


Having a good host, however, is only half the battle; you also need a flexible ecommerce engine that can be customized to suit your needs, and this is where you need Medusa. Medusa is a composable ecommerce engine that offers many out-of-the-box features. It allows developers to choose any frontend stack and tailor the storefront as they wish.


In this tutorial, you will learn how to build a complete commerce site using Next.js,  Medusa, and  Stripe, and deploy the site using Vercel.


![](/images/1VhJEcev9a.gif)


## What is Vercel?


[Vercel](https://vercel.com/docs/concepts/get-started) is a cloud platform that enables developers to easily build and deploy modern web projects built with frameworks like Next.js, Svelte, React.js, Nuxt.js, and more. With Vercel, you can host static sites and serverless functions. You can take advantage of the exciting features, such as automatic HTTPS, global CDN, Vercel CLI, and atomic deployments. 


Vercel integrates with Git, i.e. it can connect to your Git repository and automatically deploy your code when changes are made to it. This is known as "continuous integration and deployment" (CI/CD). 


Hence, you can easily deploy your projects without having to worry about managing infrastructure. Whether you're a beginner or an experienced developer, Vercel provides a seamless developer experience that allows you to focus on building great products.


### Why use Vercel?

- Easy Deployment and Hosting: Vercel makes it simple to deploy and host web projects with its intuitive interface and one-click setup.
- Integration with Popular Frameworks and Tools: Vercel supports a many popular frameworks and tools, including React, Angular, Vue, Next.js, and more, making it a versatile option for a variety of web projects.
- Automatic HTTPS and Global CDN: Vercel automatically provisions and renews SSL certificates for your domain and distributes your project's files to a global CDN, which helps to improve the performance and security of your website.

## What is Next.js?


[Next.js](https://nextjs.org/docs/getting-started) is a popular open source JavaScript framework for building server-rendered and statically-generated web applications. It is based on React, a JavaScript library for building user interfaces. It is designed to make it easy for developers to create fast, scalable web applications that are optimized for performance.


Next.js provides features and tools for building and deploying web applications, including server-side rendering, automatic code splitting, incremental static regeneration, data fetching, and support for static and dynamic routes. 


It is SEO-friendly and widely used by developers to build modern web applications. It is known for its simplicity and ease of use.


### Why use Next.js?

- Server Rendering: Next.js is a framework for building server-rendered React applications. This means that the initial render of a Next.js application is done on the server, which can improve the performance and SEO of your website.
- Automatic Code Splitting: Next.js automatically splits your code into small chunks, which helps to reduce the initial load time of your website and improve the user experience.
- Hot Code Reloading: Next.js supports hot code reloading, which allows you to see changes in your code without having to manually refresh the page.

## What is Medusa?


[Medusa](https://github.com/medusajs/medusa) is an open source, [Node.js-based](https://medusajs.com/blog/nodejs-ecommerce-backend/), composable commerce engine. It has an amazing developer experience and endless customization options for ecommerce businesses looking to scale.


Medusa has three components: Medusa Server, Medusa Admin, and Medusa Storefront. The Medusa server can be integrated with any [frontend](https://medusajs.com/blog/which-frontend-framework-you-should-pick-for-your-ecommerce-storefront/) technology of your choice, thereby making it easy for developers to use different frontend technology while building their online stores.


![](/images/g1f2PTuDo3.png)


Medusa has essential ecommerce features such as an admin dashboard, a multi-payment option, manual orders, [multi-currency support](https://medusajs.com/blog/multi-currency-ecommerce/), a shopping cart, products and image optimization, an SEO-friendly interface, and more.


## Why use Medusa?

- Accessible Codebase: As an open source commerce engine, Medusa has all its codebase available on its official GitHub Repository, making it more accessible for developers.
- Headless Architecture: Medusa is based on Node.js and separates the frontend from the backend. It also separates the admin panel from the backend. Making changes in one part, either backend, admin, or storefront doesn’t affect the other. This will help developers know where to focus when fixing a bug.
- Strong Community Support: Medusa provides 24/7 community support through its Discord channel.

## What is Stripe?


[Stripe](https://stripe.com/payments) is a payment processing platform that provides a simple, secure way for businesses to accept payments online. It offers a range of tools and services for processing transactions, including support for credit and debit card payments and other forms of payment such as Apple Pay and Google Pay. 


Stripe provides a comprehensive set of APIs and libraries that make it easy for developers to integrate its payment processing capabilities into their websites and applications.


## Why use Stripe?

- Secure Payments: Stripe uses industry-standard security measures to ensure that all transactions are secure and compliant with regulations.
- Scalability: Stripe can handle large numbers of transactions and can easily scale to meet the needs of growing businesses.
- Robust Feature Set: Stripe offers a variety of features, including subscriptions, recurring payments, and fraud detection, which can help businesses streamline their payment process.

## Prerequisites


Before starting this tutorial, ensure you have the following ready:

- [Node.js](https://nodejs.org/en/) (v14 or later)
- [Stripe](https://dashboard.stripe.com/register) account (with API keys ready)
- [Git](https://git-scm.com/download/win) installation
- [Vercel](https://vercel.com/signup) account

## Creating a Medusa Project


A Medusa project is composed of the server, storefront, and admin. All these will be installed using a single command line.


In your terminal, run the following command:


```bash
npx create-medusa-app
```


While the above command is running, you’ll be asked to enter the name of the directory you want the project to be installed. You can either leave the default value `my-medusa-store` or enter a new name.


![](/images/_5__-cCPuc.png)


Next, choose the Medusa server starter. The Medusa server is created from a starter template. By default, it is created from the `medusa-starter-default` template. So choose `medusa-starter-default` to enable you to follow up with this project.


![](/images/fu1-omnp2p.png)


Doing this will install the server under the directory `my-medusa-store/backend`. It will also create an SQLite database inside that directory with demo data seeded into it.


After choosing the Medusa starter, the next prompt will ask you to choose the storefront starter. Choose Next.js Starter which is what you will use for this project storefront.


![](/images/Wg6kQfoo08.png)


Once you are successfully done with the above, you can follow the code block below to navigate around your store server, admin, and storefront:


```bash
## Medusa API
cd my-medusa-store/backend
medusa develop

## Medusa Store Admin
cd my-medusa-store/admin
npm start

## Medusa Storefront
cd my-medusa-store/storefront
npm run dev
```


> Note: Each folder (backend, admin, and storefront) has its own Git history.


## Install and Configure Stripe Medusa Plugin in Medusa Backend


The _Stripe Medusa plugin_ will enable Stripe payment to work on this project and also create a channel for your project to communicate with Stripe APIs.


Before you start, navigate to your `backend` directory using the following command:


```bash
cd my-medusa-store/backend
```


In the root of your backend, run the following command to install the Stripe plugin:


```bash
npm install medusa-payment-stripe
```


Next, you need to add  STRIPE API KEY and STRIPE WEBHOOK SECRET to your `.env` file:


```text
STRIPE_API_KEY=example_API_key_xxxxx
STRIPE_WEBHOOK_SECRET=example_WEBHOOK_key_xxxxx
```


In the above, replace `example_API_key_xxxxx` and `example_WEBHOOK_key_xxxxx`  with the keys gotten from your [Stripe dashboard](https://dashboard.stripe.com/test/apikeys).


>  Note: Stripe webhook secret is not necessary to add in development. You can skip it if you wish.


Next, you need to add configurations for your Stripe plugin. In `medusa-config.js`, add the following at the end of the `plugins` array:


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


### Test Medusa Server


If you’ve completed the above processes, start your store server with the command below:


```bash
medusa develop
```


You can navigate to `localhost:9000/store/products/` to see available products in your store.


![](/images/wpc0t7B9Cx.png)


The image you see above represents a sample response containing your store products. You should see something similar. 


### Enable Stripe Payment Provider in a Region


Regions in Medusa are used to manage the markets where you will operate within. You can manage and add multiple countries in a region. You can also manage shipping options and payment providers.


Before you start, navigate to your `admin` directory and start your admin using the following command:


```bash
cd my-medusa-store/admin
npm start
```


Ensure your _backend server_ is still running, then `localhost:7000` on your browser to access your admin page.


![](/images/jEDbcC1C-3.png)


If you completed the steps above successfully, then you should a page similar to the image above.


Medusa seeded your database with a demo admin that you can log in with. The email is `admin@medusa-test.com`, and the password is `supersecret`.


If you log in with the demo admin login details, you will have access to your admin dashboard.


The next step is to add Stripe Payment to your Regions, simply follow the steps below:

1. Go to _Settings → Regions_.

	![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/472bf4c1-d91d-46d2-b726-1cadb1a247fe/v3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230213%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230213T110018Z&X-Amz-Expires=3600&X-Amz-Signature=e308a3ec24493582598242a6977260db3f45402c0efa7d160d51f47cba5baaaf&X-Amz-SignedHeaders=host&x-id=GetObject)

2. Click on the region you want to edit from the _Regions_ section.

	![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ddcfedf7-57e6-406a-9bc2-d1d2399352b6/v5.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230213%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230213T110019Z&X-Amz-Expires=3600&X-Amz-Signature=4dca2981c0c2f4c98f2e2cd2b2cf4e5ca499b7ba2bc8faedeab94fb6c7cfa3a1&X-Amz-SignedHeaders=host&x-id=GetObject)

3. Click on the three-dot icon at the top right of the selected region and click on _Edit Region Details_.

	![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5eec7f88-1d3f-48c4-bd65-c55e8bd6e833/v4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230213%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230213T110019Z&X-Amz-Expires=3600&X-Amz-Signature=645b0977ee63066addf0c465ce20df813f6a44e10b335d7f9d531ca332b1d6be&X-Amz-SignedHeaders=host&x-id=GetObject)

4. Select Stripe as the payment provider.

	![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5c75a93f-47f3-444f-9331-e7a580fa01fa/v6.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230213%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230213T110019Z&X-Amz-Expires=3600&X-Amz-Signature=198b6042c3e068e628d8a82c4faaaf89bfd48a60b2a9acc36ed7b58c9956227f&X-Amz-SignedHeaders=host&x-id=GetObject)


Once done with step 4, you can click on the _Save and close_ button to save.


Repeat these steps to add Stripe Payment to other regions.


## Test Next.js Storefront


Before testing, switch to the _storefront_ directory and rename the template environment variable file to use environment variables in development:


```bash
cd my-medusa-store/storefront
mv .env.template .env.local
```


Then, add Stripe public key to your Next.js storefront.


In your `.env.local` file (or the file you’re using for your environment variables), add the following variable:


```text
NEXT_PUBLIC_STRIPE_KEY=<YOUR_PUBLISHABLE_KEY>
```


Make sure to replace `<YOUR_PUBLISHABLE_KEY>` with your [Stripe Publishable Key](https://dashboard.stripe.com/test/apikeys).


Lastly, ensure your Medusa server is running, then run the command below:


```bash
npm run dev
```


After a few seconds of running the above command, navigate to `localhost:8000` on your browser to see your Next.js ecommerce storefront homepage.


![](/images/E8hs-Y9FPW.png)


Scroll down to select a product from the featured products on the homepage.


![](/images/ZHq8Kj_jV7.png)


Click on a product to view the single product page where you can add items to your cart.


![](/images/lvIQbEiKXl.png)


If you click on _My Bag_ at the top right of your store, you will view the cart review page of your store.


![](/images/DgX0cqiaiz.png)


Click on _GO TO CHECKOUT_ to see your _Checkout_ page, where you will be asked to input your delivery information.


![](/images/zPqTSovL81.png)


After a successful payment, you’ll see the _Order Receipt_ Page.


![](/images/gvTskvtMmE.png)


## Deployment to Vercel


After testing your store, the next thing is to deploy your store backend, admin, and storefront using Vercel.


### Deploying Medusa Backend


Medusa has already provided different clear documentation on how to host Medusa Server in different hosting servers.


You check [Medusa Server Deployment Guide](https://docs.medusajs.com/deployments/server/) to deploy your backend to any server of your choice. 


### Deploying Medusa Admin Panel


You can easily deploy your Medusa Admin on Netlify by following Medusa [Admin Deployment Guide](https://docs.medusajs.com/deployments/admin/deploying-on-netlify).


### Deploying Next.js Storefront


In deploying your Next.js Storefront, you will handle this using Vercel.


Deploying Next.js storefront in Vercel can be done using [Vercel CLI](https://vercel.com/guides/deploying-nextjs-with-vercel#vercel-cli) or [Vercel for Git](https://vercel.com/guides/deploying-nextjs-with-vercel#vercel-for-git). For this tutorial, you can deploy using Vercel for Git, using the steps below as a guide.


> Note: You should have the backend URL ready because it will be needed.

1. Push your storefront project to a GitHub repository.
2. On your Vercel dashboard, click on the _import_ button to import a new project.

![](/images/yWx4piUvZP.png)

1. Enter the name of your project in the _Project Name_ field.

![](/images/A_IWNWORjQ.png)

1. Add the environment variables: `NEXT_PUBLIC_MEDUSA_BACKEND_URL` and `NEXT_PUBLIC_STRIPE_KEY`.

	![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9143761c-b974-4ac6-bed3-fa4ed1b1fb57/h7.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230213%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230213T110020Z&X-Amz-Expires=3600&X-Amz-Signature=c7c4b411f85211cd57536f3dd75e9e0ade57a1479d4fef3e522a56305e11df68&X-Amz-SignedHeaders=host&x-id=GetObject)


	When configuring your environment variable, ensure you set the backend URL with your production server (for example:  `https://my-medusa-server.com`) and your live Stripe public key.

2. Click on _deploy_ to start the deployment process.

	![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f2f12206-e043-404d-b25e-7e2c0141cae6/h5.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230213%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230213T110020Z&X-Amz-Expires=3600&X-Amz-Signature=e62c8e85a2528294ea18debae097c17bc71533eaba06c8f50652777de5d1fd51&X-Amz-SignedHeaders=host&x-id=GetObject)


Once the deployment process is completed, your storefront is ready. You can visit the domain link to view your storefront.


![](/images/GACOSnofMR.png)


> Note: Before testing, ensure you update your server’s `STORE_CORS` environment variable with the new Vercel URL to avoid CORS issues. You can check [CORS configurations](https://docs.medusajs.com/usage/configurations#storefront-cors) on Medusa documentation.


## Conclusion


In this tutorial, you learned how to build a Vercel ecommerce site using Next.js, Medusa,  and Stripe. You’ve gone through the steps of setting up Medusa Server, Medusa Admin, and Medusa Next.js Storefront.


You can also add various features to your store, like [Algolia](https://docs.medusajs.com/add-plugins/algolia) search engine service, [Mailchimp](https://docs.medusajs.com/add-plugins/mailchimp) email marketing service for newsletters, [Segment](https://docs.medusajs.com/add-plugins/segment) data platform for collecting analytics, and many more.


You can learn more about Medusa commerce engine from [Medusa’s Documentation](https://docs.medusajs.com/introduction).


> Should you have any issues or questions related to Medusa, then feel free to reach out to the Medusa team via [Discord](https://discord.gg/medusajs).

