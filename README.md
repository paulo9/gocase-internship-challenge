# Gocase - Backend Challenge

First of all, thank you very much for accepting our challenge. Here at **Gocase**, we value the ability to deliver simple, elegant and functional code. There are always unexpected situations that will arise, and our design must be malleable to handle the turns and obstacles along the road, without over-engineering. Our small challenge tries to identify if you have the abilities we value to join our Engineering Team.

You may find that some of our instructions are quite vague, it's intentional and you must use your best judgement to decide how to handle the unknowns. If you need further assistance, please contact us!

## What should I do?

We're trying to build a simple REST API using Ruby on Rails. Our purpose is to create a platform to receive **Purchase Orders** from other systems, group them on **Batches** and follow the Orders in the **production pipeline** until the dispatch.

Other systems may control when an Order or a Batch is ready to move to the next stage using a few endpoints to signal progress on the production pipeline.

## Entities

### Order

An Order is composed by the data needed to produce and dispatch a purchase by a client. It's composed of the following properties:

- Reference (e.g. BR102030)
- Purchase Channel (e.g. Site BR)
- Client Name (e.g. Rogerio Lima)
- Address (e.g. Rua Padre Valdevino, 2475 - Aldeota, Fortaleza - CE, 60135-041)
- Delivery Service (e.g. SEDEX)
- Total Value (e.g. R$ 123.30)
- Line Items (these are the instructions needed to produce the items, it does not follows an strict structure, e.g. [{sku: case-my-best-friend, model: iPhone X, case type: Rose Leather}, {sku: powebank-sunshine, capacity: 10000mah}, {sku: earphone-standard, color: white}] )
- Status: ready (a new order, ready to be produced), production (waiting to be printed), closing (already produced, waiting to be sent), sent (on the way to the client).

### Batch

A Batch is a group of Orders following the same production pipeline. Before starting producing the Orders, an operator will take all available orders that are ready and group them on a Batch. It's composed of the following properties:

- Reference (e.g. 201803-54)
- Purchase Channel (e.g. Site BR)
- A group of orders.

### A few more details

- Different Purchase Channels have different priorities. For that reason, we can't mix Orders from different Purchase Channels in the same Batch.
- Every Delivery Service has a different schedule. For that reason, we dispatch Orders of the same Delivery Service together.
- It's only necessary to create those two entities in our design. For brevity, you can just use Strings to represent stuff that in a real-life situation is clearly another entity. As always, feel free to create additional classes if you feel the need.

## Actions

Now we need a few endpoints to allow the other systems to interact with our platform. Our platform will set the architecture, and the other systems will adapt to our design decisions.

### Create a new Order

We need an endpoint where other systems can input data for an Order. I imagine that they need to know somehow if the Order is valid and if it was persisted correctly.

### Get the status of an Order

After purchasing our products, our customers are often very anxious about the production status of their Orders. We do our best to give updates as real-time as possible. Sometimes they lose the Reference, but we can find it using their names. Just be careful about our long-time recurring clients, they may have many Orders in our platform.

### List the Orders of a Purchase Channel

Sometimes we need to review what's in the production pipeline. We may want to restrict our listing to a single state (e.g. We need to know all the Orders in closing for the Iguatemi Store Purchase Channel).

### Create a Batch

We need a way to create a Batch and pass those Orders to the production status. We should input the Purchase Channel and receive back the Reference of the created Batch along with the number of Orders that were included.

### Produce a Batch

After the printing is done, we need a way to tell our platform to pass a Batch from production to closing.

### (Bonus) Close part of a Batch for a Delivery Service

We also need a way to input a Batch and a Delivery Service and those Orders should be marked as sent.


## What stack should I use?

- Ruby on Rails;
- Git;
- Any gem, as you see fit;
- Postgres;
- It's not necessary to have full suite of tests, but it would be nice to have a couple of them.

## How can I submit it?

Create a git repository with your solution and texts and give us the path to access it. It can be a public GitHub repository or something else if you prefer. If for some reason you didn't have enough time to complete all the requirements, add a brief description of how would you handle the missing features. 😊

## What is under evaluation?

- Does the solution satisfy the requirements and it works correctly?
- Does the solution can elegantly handle bad input and edge cases?
- How did you designed your solution? Is it organized and flexible to modify or extend?
- Is your code clean and easy to understand?
- Does the implementation follow established best practices?

We don't expect that everything will be perfect, but we value a lot if you can identify where you're lacking and where you can improve. Again, thank you very much for accepting our challenge and good luck! 🏎
