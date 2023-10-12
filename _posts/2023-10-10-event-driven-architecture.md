---
layout: post
title: Event Driven Architecture
categories: [System Design]
---

In Event Driven Architecture, flow of messages/data from one service to another is done using events.This architecture focuses more on scalability and is flexible enough to add/remove more components.

![](/images/event-driven.png)

### Why to use Event-Driven Architecture
Usually we have REST driven API used commonly for systems where REST handles request Synchronously, i.e for each request to the system user have to wait for the reply till the system processes the request. It can work well at the intial stage but as system grows and no. of request increases, it becomes very difficult to maintain the performance and thus overall responsiveness of system decreases. For example lets say user is placing the order now the process of creating order will go through many checks and validations, so if we use synchronous way then it is not good user experience for user to make him wait for response back while the whole request is getting processed, and for user it is not necessary to know the internal functionality of system. But if we do it asynchronously once user has placed the order we can just give him acknowledged message back in response saying order is placed successfully and process the other things separately. This way he doesn't have to wait for the response and it counts in good user experience also. This is where event-driven systems becomes usefull on every user action we can trigger an event which just sends back ack message back and do the rest of the process simultaneously.

Also when we build system architecture event-driven then if there are multiple services functioning then none of them needs to be dependent on the other services to perform any action or each of them need not to be aware of the functionality of other services. As each of them communicate using the events and whichever event particular service is subscribed to once that get generated then that particular service will perform any action. This makes both the development and deployment easier.


### Key Components of Event Driven Architecture are:

- Events: Events are generally considered as change in state of the system.

- Event Producer: These are the components that generate the events which are sent to the broker/event bus. These producers can be other systems, databases, user interface etc.

- Event Consumer: These are the components that recieve the events from broker and trigger some action to these events which can be like processing data or acknowledging the state change or emitting other events etc. 

- Event Channels/Broker: These are the channels/broker using which events are transmitted/communicated from producers to consumers. These can be streams, messaging queues.

- Event Handler: These are responsible for processing the recieved events. They are defined as set of rules withing the system which can perform certain action on recieving events, or execute any buisness logic.

### How to identify events
As mentioned above events are generally referred to change in state. When you think of events these can be derived from simple use cases to how it will process withing the service. Example lets assume user purchased a product. Now before making purchase there can be many events that can happen like user views the catalog which can be event, adding/removing product from cart, liking the product, applying the promo code if available these all can be events which can get triggered from separate services as all are changing the state of the system from one state to another.    


### Protocols used in event-driven architecture
- **Web Sockets** : WebSockets are a communication protocol that enables real-time, two-way communication between a client (typically a web browser) and a server over a single, long-lived connection. They are designed to provide low-latency, full-duplex communication, making them ideal for applications that require real-time updates or interactive features

- #### Here's how WebSockets work:
	1.WebSocket Handshake: The process begins with a standard HTTP handshake. The client sends an HTTP request to the server, including a special Upgrade header with the value "websocket." The server, if it supports WebSockets, responds with an HTTP 101 "Switching Protocols" status code, indicating the upgrade is accepted.
	2.WebSocket Connection Establishment: Once the handshake is successful, the connection is "upgraded" from an HTTP connection to a WebSocket connection. The key feature here is that this connection remains open and persistent, unlike traditional HTTP connections, which are stateless and short-lived.
	3.Bi-Directional Communication: After the WebSocket connection is established, both the client and server can send messages to each other at any time without waiting for a request-response cycle. This allows real-time, bidirectional communication.
	4.Heartbeats and Keep-Alive: To maintain the connection, WebSockets often use "ping" and "pong" messages, which are lightweight signals to confirm that the connection is still active. This helps ensure the connection remains open, even if there is no active data transfer.

- **Pub-Sub**:  The Pub/Sub (Publish/Subscribe) model is a messaging pattern used in distributed systems to enable communication between different components or services in a decoupled and scalable way. In a Pub/Sub system, there are three main components: publishers, subscribers, and a message broker.

- #### Here's how the Pub/Sub model works:
	1.Publishers: Publishers are entities or components that generate messages or events. These messages could be notifications, updates, data changes, or any other kind of information. Publishers are responsible for sending these messages to the message broker without needing to know who or what will receive them. They "publish" messages to specific channels or topics.
	2.Subscribers: Subscribers are entities or components that express an interest in receiving specific types of messages. They subscribe to one or more channels or topics. Subscribers are completely unaware of the publishers. They only receive messages that match their subscribed channels or topics.
	3.Message Broker: The message broker acts as an intermediary between publishers and subscribers. It receives messages from publishers and delivers them to the appropriate subscribers based on their subscriptions. The message broker maintains a list of subscribers and the channels or topics they are interested in. When a message is published on a channel or topic, the message broker ensures that it reaches all interested subscriber

- **Event Streams**: Event streams, often referred to as event sourcing or event logs, are a fundamental concept in the domain of distributed systems and data processing. They represent a sequence of discrete events that have occurred over time. Event streams are commonly used for various purposes, including real-time data processing, event-driven architectures, and auditing

- #### Here's how event streams work:
	1.Events: Events are discrete occurrences or updates that happen within a system. These events can represent a wide range of activities, such as user actions (e.g., clicks, sign-ins), system changes (e.g., configuration updates), or sensor data (e.g., temperature readings). Each event is typically represented as a structured piece of data.
	2.Event Log: Events are appended to an event log, which is essentially a time-ordered, immutable, and append-only data structure. The event log serves as a historical record of all events that have occurred within a system. Events are appended to the log as they happen, and once an event is added, it cannot be modified or deleted.
	3.Event Stream Processing: Event streams can be processed in real-time or batch mode. Event stream processing involves reading events from the event log and taking actions based on the information contained in those events. This processing can include aggregations, analytics, notifications, or triggering other actions in response to specific events.

- **Web Hooks** : Webhooks are a way for web applications to provide real-time data to other applications or services. They enable one application to notify another application or service about events or updates in near real-time. Webhooks are widely used for various purposes, such as triggering actions in response to events, data synchronization, and integrations between different software systems

- #### Here's how webhooks work:
	1.Setup and Registration: To use webhooks, the receiving application or service (the webhook consumer) provides a URL endpoint where it can receive HTTP POST requests. This URL is typically provided to the sending application (the webhook provider). The webhook provider needs to know where to send data when an event occurs.
	2.Event Occurs: An event, such as a user signing up, a payment being made, a new comment being posted, or any other event defined by the webhook provider, occurs in the provider's system. This could be a user action, a change in data, or any other trigger.
	3.Notification: When the event occurs, the webhook provider generates a payload containing information about the event and sends an HTTP POST request to the URL endpoint provided by the webhook consumer. This payload is typically in JSON format and includes data related to the event.
	4.Webhook Consumer Processing: The webhook consumer receives the HTTP POST request with the event data. It processes the payload and takes actions based on the information provided. These actions could include updating its database, sending notifications, or triggering other processes.
	5.Acknowledgment: After processing the payload successfully, the webhook consumer may respond to the webhook provider with a status code (usually 2xx) to confirm that it has received and processed the data. This acknowledgment helps ensure the webhook provider that the event notification was successfully delivered

### Key Benefits of Event Driven Architecture:
- Loosely Coupled: Components are usually not aware of each other existence and how other components functions as they mainly communicate using events. This allows to make changes to one service and deploy them without affecting the other services.  

- Asynchronous: Processing of events happens asynchronously, so that other components do not have to wait for the response back which increases the responsiveness of system 

- Scalable: Event Driven systems are usually designed to handle large chunks of data and can handle increasing no of requests.

- Flexible: New components can be added or removed as per the requirement which will not effect the overall architecture.
