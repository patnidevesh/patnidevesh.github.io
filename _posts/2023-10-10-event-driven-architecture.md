---
layout: post
title: Event Driven Architecture
categories: [System Design]
---

In Event Driven Architecture, flow of messages/data from one service to another is done using events.This architecture focuses more on scalability and is flexible enough to add/remove more components.

![](/images/event-driven.png)

## Key Components of Event Driven Architecture are:

- **Events**: Events are generally considered as change in state these can be user actions like add/delete of item, or can be notifications from the other system .These events are used to communicate within system and can act as an state identifier or they can also transport messages across other services.

- **Event Producer**: These are the components that generate the events in form of messages to the broker/event bus. These producers can be other systems, databases, user interface etc.

- **Event Consumer**: These are the components that recieve the events from broker and respond to these events by executing the specific actions like processing data or acknowledging the state change or emitting other events etc. 

- **Event Channels/Broker**: These are the channels/broker using which events are transmitted/communicated from producers to consumers. These can be streams, messaging queues.

- **Event Handler**: These are responsible for processing the recieved events. They are defined as set of rules withing the system which can perform certain action on recieving events, or execute any buisness logic.

## Advantages of Event Driven Architecture:

- **Loosely Coupled**: Components are usually not aware of each other existence and how other components functions as they mainly communicate using events. This allows to make changes to one service and deploy them without affecting the other services.  

- **Asynchronous**: Processing of events happens asynchronously, so that other components do not have to wait for the response back which increases the responsiveness of system 

- **Scalable**: Event Driven systems are usually designed to handle large chunks of data and can handle increasing no of requests.

- **Flexible**: New components can be added or removed as per the requirement which will not effect the overall architecture.
