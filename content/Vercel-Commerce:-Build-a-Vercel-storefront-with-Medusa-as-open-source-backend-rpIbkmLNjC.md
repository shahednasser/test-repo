
## Introduction


[Medusa](http://medusajs.com) is an open source headless ecommerce platform that allows you to get an ecommerce store up and running with a minimum amount of work, working as an alternative to Shopify. 


Medusa has three (3) core parts: Medusa Server, Medusa Storefront, and Medusa Admin. What is really good about Medusa is the fact that you can customize each and every component of Medusa according to your requirements. You’re also not locked in; you can deploy your Medusa store on any infrastructure.


Unlike other ecommerce platforms like Shopify, where your store will be hosted by Shopify itself, Medusa allows you to host your store yourself and customize it to your taste.


At the end of this guide, you will be able to spin up a new Medusa store, use the prebuilt next.js commerce template and deploy it on [Vercel](https://vercel.com/docs).


## What is Vercel Commerce?


[Vercel ](http://vercel.com)is a leading platform where you can deploy frontend applications. There are several pros to using Vercel to deploy the Medusa storefront. 


Sites deployed in Vercel can be loaded very fast compared to all other deployment services; this is very important for an ecommerce site because fast loading times lead to better rank in search engines.


This tutorial uses Next.js, a framework that does server-side rendering. Server-side rendering (SSR) means pre-rendering pages in the server beforehand and sending them to the client. This will contribute towards the initial loading speed of the website.


## Prerequisites


To use Medusa, you need to have Node.js installed on your local computer. If you don’t have it already, you can download it from the [official Node.js website](https://nodejs.org/en/). You would also need a [GitHub and ](https://github.com)[Vercel ](http://vercel.com)accounts.


Lastly, you should have the Medusa server deployed. You can follow this [guide](https://docs.medusajs.com/admin/quickstart/) to do that.


### Prepare Medusa Next.js Storefront


Now that you have the Medusa server ready, you can start preparing the storefront. You can start by building your own storefront using the [Medusa storefront API](https://docs.medusajs.com/api/store), but this tutorial uses the [official Next.js Starter provided by Medusa](https://github.com/medusajs/nextjs-starter-medusa), which is a starter kit for high-performance ecommerce sites.


To install the storefront, go to your preferred directory and run:


```bash
npx create-next-app -e https://github.com/medusajs/nextjs-starter-medusa medusa-storefront
```


This will create a new Next.js project with the Medusa Next JS starter code. Change to the newly created directory and rename the `.env.template` file:


```bash
cd medusa-storefront
mv .env.template .env.local
```


## Deployment on Vercel


At the end of this section, you will know all about deploying your Medusa storefront on Vercel.


### **Push Storefront to GitHub**


Before deploying your storefront to Vercel, you have to upload your code to GitHub. Go to [GitHub ](https://github.com)and create a new repository with your preferred name.


Go back to the terminal and run the following commands inside the folder containing Medusa storefront:


```bash
git remote add origin <REPO_URL>
git push -u origin main
```


Make sure to replace the `<USER>` and `<REPO>` placeholders with your real values. After completing this step, your code should be uploaded to GitHub; you can confirm this by going to the GitHub repository page.


### Vercel Deployment


Now that everything else is ready, all you have to do is deploy the storefront on Vercel.


Once you’re inside the Vercel dashboard, click on the _Add New_ button and choose _Project_ from the menu.


![](//XkRO2Zty7w.png)


This creates a Vercel project. Next, choose _Continue with GitHub_ to grant access to your GitHub account or the specific repository you want to deploy.


![](//Ygx1wIIBvt.png)


From the repository list, choose the repository you want to deploy and click on _Import_.


![](//rHJV7n-UXt.png)


### Environment Variable Configuration on Vercel


Before deploying, you have to set the environment variables in Vercel. In Vercel _Configure Project_ page section, expand _Environment Variables_ and you will see a page similar to the one below. 


![](//qDlpILLVXd.png)


Now, add your environment variables one by one to these input boxes. To do that, open the `.env.local` file inside your project folder and for each line of that file, input the part before `=` sign to the name and the part after `=` to the value.


If you’re not using any payment processors or search services, you would only be required to enter one environment variable: `NEXT_PUBLIC_MEDUSA_BACKEND_URL`. This is where you should input the deployed Medusa server URL. Enter the corresponding information in the environment variable settings and click on _Deploy_.


### Add Server Environment Variables


You need to copy your storefront’s URL that you will find under Domains on the Vercel project page and add it under the environment variable, `STORE_CORS`, of your Medusa server instance. This will make sure that no CORS errors will occur.


Visit the default store domain, you will see Medusa storefront working with all the products being displayed (which means the connection to backend is successful).


## Testing Storefront After Deployment


After a few seconds, you will see that the deployment has been completed and the storefront is up and running.


![](//RKq6ppjkjS.png)


## Conclusion


Now, you should have a clear understanding of Vercel commerce. Once you have deployed the storefront, you can focus on making the storefront better. 

- Read [this guide](https://docs.medusajs.com/starters/nextjs-medusa-starter) to know more about the storefront template you used.
- Read [this guide](https://docs.medusajs.com/add-plugins/stripe/) to learn how to integrate Stripe into your store
- Check out this [documentation](https://docs.medusajs.com/) to learn all sorts of things you can do with Medusa.

> Should you have any issues or questions related to Medusa, then feel free to reach out to the Medusa team via [Discord](https://discord.gg/F87eGuwkTp).

