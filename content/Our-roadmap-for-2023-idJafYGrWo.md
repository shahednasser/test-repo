---

<details>
  <summary>Scorecard</summary>


> ⚠️ This should not be edited by the author.


[Content Quality](05a50394-45a2-4ec0-907b-48c6cfc07700)



  </details>


As [Medusa](https://github.com/medusajs/medusa) is an open source solution, it’s important for us to include the community in our plans for upcoming features. For that reason, we included a specific section in our [GitHub Discussions that shares our Roadmap](https://github.com/medusajs/medusa/discussions/categories/roadmap).


This opens a discussion with the community and allows us to get direct feedback or new ideas for each planned feature. This also allows us to constantly give updates on the progress of those features, ensuring transparency and collaboration with our community.


In this article, we want to share some features from our Roadmap for 2023. Feel free to share your thoughts after reading through this.


## Roadmap Plans


At Medusa, we strive to implement high quality and advanced features for our community and ecommerce businesses. We have a broad vision of the features that we want to implement, and the direction we want Medusa to move into.


For that reason, when you look at our [Roadmap on GitHub](https://github.com/medusajs/medusa/discussions/categories/roadmap), you’ll find that there are items with different labels such as “backlog” or “planned”. Although we hope and strive towards shipping these features quickly, we value quality over quantity.


So, this article only covers the items on the Roadmap labeled “started”, as these are guaranteed to be shipped in 2023.


## Our Roadmap for 2023


### Nested Categories


Medusa currently allows merchants to organize their products by Collections to be used in storefronts or for internal business logic. For example, they can be used for controlling whether discounts can be applied to a group of products.


In the near future, we will introduce an additional way to manage your product hierarchy and create better experiences for your customers. Nested Categories will allow you to define category hierarchies like Women’s > Bottoms > Skirts to better organize product navigation on storefronts.


Furthermore, adding the same product to multiple categories will be possible, enabling better merchandising functionality right within the Medusa dashboard.


As always with Medusa, you own your data and can extend and customize the behavior of our APIs. This is also the case with Nested Categories, which will enable developers to create enhanced search and browsing experiences while adding a new, powerful reporting dimension to your product catalog.


![](//atnXFNwWYr.png)


### **Payment Processor API**


One of Medusa’s core strengths is its composable architecture, which allows integrating it with the best-in-breed tools that accelerate ecommerce growth.


From the beginning, offering the best payment option to your customers at any time has been a core feature of Medusa. Medusa already allows merchants to attach as many payment processors — such as Stripe, PayPal, and Klarna — as they want and, with powerful multi-regional logic, control which options are shown to the customer at checkout.


With our new Payment Processor API, we will unlock even more capabilities and make it easier for plugin developers to create integrations with payment processors worldwide.


Simultaneously, the new Payment Processor API will enable better support for RMA flows requiring payments. We recently released Order Editing, which allows merchants to modify orders after they have been placed.


Edits can result in discrepancies between the order total and paid total, and with the new Payment Processor API, we are making it simpler to collect payments for differences.


### **EventBus Modules**


Medusa emits hundreds of events that plugins use to send transactional emails, automate tedious tasks, and reliably integrate systems in your stack. 


The existing event system uses Redis with BullMQ to enable Pub/Sub functionality. Many larger implementations will, however, already have an event architecture in place.


With the new EventBus Modules, it will be possible to integrate your existing events architecture directly into Medusa.


This will enable new EventBus providers like RabbitMQ, Kafka, or Amazon SQS, and improve Medusa’s compatibility with microservice architectures.


### Automated API specs and typing


Medusa’s API reference is automated to ensure that the documentation is always up-to-date with the core API. As part of our dedication to [improving our documentation](https://medusajs.com/blog/how-we-improved-our-documentation/), we are enhancing how we document the API with code and simultaneously creating new automations to generate our client library.


This will remove inconsistencies between server logic, documentation, and client library support. 


We will, furthermore, be able to eliminate the current dependency on `@medusajs/medusa` in our client library, which will help reduce the bundle size of storefront implementations. 


### Multi-Warehouse API


As businesses expand into new markets and open physical stores, supply chains and logistics become much more complex. Without the right tools to manage the many moving parts, orders can get lost, and stock issues start to pile up. 


Medusa already enables great integrations with OMS and IMS systems. But we are now adding a more sophisticated inventory layer that allows Medusa to support businesses with multiple distribution centers or retail stores natively.


Merchants can manage inventory across locations within Medusa and connect locations to sales channels to control stock availability.  Furthermore, we will introduce allocations to ensure safety stock and avoid overselling. This will give merchants a clear picture of their inventory at any given point. 


The new feature will enable a wide range of new experiences for customers, such as buy-online-pick-up-in-store or reserve-online-try-in-store flows. Developers will also get an excellent new API that can be used to optimize fulfillment, build POS experiences, and further push the boundaries of what can be done within digital commerce.


![](//G9VcfjPSg3.png)


### Medusa Admin extensibility


One of Medusa’s principles is to build strong defaults that make it quick and easy to get started, and simultaneously offer a fantastic developer experience that enables customizations and extensions to make Medusa your bespoke commerce engine.


We have followed that principle diligently in our backend implementations until now. But our Admin dashboard has long been more locked and harder to customize. We are prioritizing changing that very soon.


Our first step will be to move our admin dashboard to an NPM package that can spin up with your Medusa server. This will improve the developer experience when building with Medusa, as you will no longer have to clone the admin project, merge updates, or start it separately from your Medusa server.


![](//6iiyLWOJUI.png)


Additionally, we will follow semantic versioning of the admin package to avoid version mismatches between the admin application and the core medusa package.


The next step hereafter will open up extension areas in the admin dashboard to add custom UI elements like buttons, cards, or entire pages. Custom elements can be created in your local project or shipped with plugins to package server and admin functionality easily.


## Conclusion


As mentioned earlier, this Roadmap overview includes only the features we started implementing. There are more upcoming features and enhancements in our Roadmap, which you can check out in our [GitHub Discussions](https://github.com/medusajs/medusa/discussions/categories/roadmap).


What features are you excited for? And what features do you think we should include in our Roadmap?


> Should you have any issues or questions related to Medusa, then feel free to reach out to the Medusa team via [Discord](https://discord.gg/F87eGuwkTp).

