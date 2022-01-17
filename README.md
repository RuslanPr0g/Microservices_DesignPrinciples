# Microservices Design Principles
Microservices are becoming increasingly popular to address shortcomings in monolithic applications.

# What is a monolithic application?
The term monolithic applies to tightly integrated applications where it is hard to change one function without also recoding other parts of the application. Components in a monolithic application might be distributed among many machines, but they remain highly dependent on one another. Not only does the addition of a new feature have ripple effects throughout the code, but deploying the change requires retesting and redeploying the entire application. These upgrades can be labor-intensive and hazardous, particularly when an application has hundreds of thousands or even millions of users.

When IT departments had the luxury of releasing software every six months, this type of upgrade process was tolerable. But modern business demands force releases to happen weekly, daily, or even more often, so the labor and risk inherent in upgrading monolithic applications become untenable.

Something has to change. That change is the transformation to the microservices-oriented application (MOA).

# What is a microservices-oriented application?
An MOA breaks its logic into small, well-encapsulated services that are distributed over several computing devices in a loosely coupled manner. Each service lives at a distinct IP address on the network and exposes a public interface that is language-agnostic. The most popular type of language-agnostic interface is a REST API, but other models for communication exist. Microservices also generally get deployed as containers when it's time to go live.

Typically, some mechanism behind the scenes coordinates the microservices to create a unified application experience. Because each microservice is well-encapsulated, its code can be updated quickly with minimal side effects. This makes maintenance easier and scaling faster.

The benefits of an MOA can be significant, but they come with a price. You need to know a thing or two about microservice design to implement an MOA effectively—you can't make it up as you go along.
