---
title: Inspired by Git: How we Designed our Order-Editing Feature
date: 2023-01-26
---

[Medusa’s](https://github.com/medusajs/medusa) Order API supports order editing capabilities that equip merchants and developers with the tooling necessary to reduce manual work and offer a great customer experience.


Designing this seemingly simple functionality proved to be a complex task that was solved with inspiration from the world's most-used developer tools.


This article covers how we adopted principles from the Git version control system and GitHub in our Order Editing API design. You can read the product announcement here. 


## Understanding Order Editing


Before going over the design behind this feature, we need to understand its constraints. Let’s dive into what it means to edit an order in Medusa.


When an order is placed, it is in its base state from a customer and store administrator point of view. Generally, the next steps for orders from here are fulfillment, shipping, and payment capturing.


Sometimes a change in the order might be required first. Several scenarios could lead to this; the customer changed their mind about their purchase, the inventory management system was out of sync with the physical stock, or the merchant wants to add a complimentary item due to long processing time.


A naive solution would allow store administrators to modify order items directly. However, this could have serious consequences. Order history is lost or becomes misleading, potential unresolved payment discrepancies arise, and stale order data remain in integrated services, such as analytics providers.


Aside from ensuring data consistency in your underlying dependencies, you also want to offer a good customer experience. Instead of changing things directly, you want to give customers full control and confidence by allowing them to confirm a change before it is completed. Supporting these cases spawns the need to introduce an intermediate pending step for the edits you make to an order.


It should be clear that editing an order is not as straightforward as updating the quantity of a line item. There are many use cases and dependencies to consider to ensure data is consistent across all systems in your stack and that customers get the best experience.


## Building an API with git-like flow of events


As we started to plan the feature, it became apparent that we were building a subset of the functionality from a version control system with a pull request-like mechanism for editing an order.


The goal was to allow users to change the original state of their order with an approval-staged flow without losing its history. A Git-like system with the management capabilities offered by GitHub.


We were excited to realize that a developer-centric pattern from our daily work could directly apply to our API design.


We can see the following resemblance between the order-editing flow and a git-like system:

- Order placed → Main branch
- Store administrator initiates an order edit → Branches out from main
- Store administrator makes changes to order edit → Pushes commits to branch
- Store administrator submits an order edit → Opens a pull request to main
- Customer confirms an order edit → Reviewer approves the pull request

We even extended the capabilities of the API with additional functionality as a result of using the Git + GitHub analogy:

- Store administrator force completes an order edit → Core maintainer force merges a pull request
- Customer requests an additional item → Reviewer requests changes to the pull request

Our feature had a functional requirement of having an intermediate step between initializing the edit and committing the changes. In this state, you can create multiple edits to the order without applying them. This is similar to pushing commits to a branch while a feature is in work-in-progress, except we only allow one commit for each order edit. More on that later.


### Design


Now let’s turn to implementation specifics to see how the analogy took shape in our data layer. 


There are two database models worth highlighting: `OrderEdit` and `OrderItemChange`:


```text
// order-edit.ts

OrderEdit
- id
- order
- changes
- internal_note
- items

// order-item-change.ts

OrderItemChange
- id
- original_line_item
- line_item
- type (add, remove, update)
```


Only properties relevant to the Git analogy are included above. If you wish to explore the models more in-depth, you can find them [here](https://docs.medusajs.com/references/entities/classes/OrderEdit).


The `OrderEdit` model holds the modifications you want to make to your order. It references the original order, stores an internal note, and contains a list of edits. When an `OrderEdit` is created, all items from the Order are copied to the `OrderEdit`.


The edits are represented as one or more `OrderItemChange` records. There are three types of changes: Add, Remove and Update. The purpose of each should be clear. When an edit is created, we store a copy of the original item to ensure full visibility of the history when these changes are eventually applied.


You might have already drawn the parallels to Git. The above data modeling is comparable to how branches, staged changes, and commits work. The `OrderEdit` is your branch diverging from the main one, and the `OrderItemChange` records are your staged changes ready to be pushed.


Together, they constitute the commit with a message and hold the information capable of showing a diff of the changes.


### Limitations to the analogy


Not all aspects of a traditional version control system apply to our feature. Whereas Git is excellent at facilitating seamless collaboration among an indefinite number of users, our feature is limited to one active order edit at a time. Only one branch aside from the main one.


This is to guard businesses against unwanted situations arising from multiple ongoing edits and outbound payment links. An example would be that customers accidentally pay for the wrong order edit. We built the logic to eliminate potential merge conflicts.


And finally, we don’t offer a way for merchants to roll back the changes when first committed. The changes made to an Order are irreversible. No `git revert`. 


## Demo


Enough talking. Let’s see it in action.


[image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1dffa01b-2b0d-4e45-8034-7427bdccf006/order-editing-2.mp4?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230127%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230127T120516Z&X-Amz-Expires=3600&X-Amz-Signature=75577bb62a3755ed233c308466b7bbe1ecf0c82e4e7010eb16422da36d8106a0&X-Amz-SignedHeaders=host&x-id=GetObject)


## Conclusion


Designing our Order Editing API was especially exciting, as it allowed us to apply existing concepts from our daily work to solve a problem for our users. The API we built provides a great developer experience by using familiar concepts while abstracting away the complexity for our merchants in the admin system.


For concrete API examples of the full order editing flow, see our how-to documentations on:

- [Edit an order as an administrator](https://docs.medusajs.com/references/entities/classes/OrderEdit)
- [Implement order-editing on the storefront](https://docs.medusajs.com/advanced/storefront/handle-order-edits)
