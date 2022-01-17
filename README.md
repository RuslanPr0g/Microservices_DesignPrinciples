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

# Five design principles for microservices
The five basic principles of microservice application design are:
- A microservice has a single concern.
- A microservice is discrete.
- A microservice is transportable.
- A microservice carries its own data.
- A microservice is ephemeral.

## 1. A microservice has a single concern
Having a single concern means that a microservice should do one thing and one thing only. For example, if the microservice is intended to support authentication, it should do authentication only. This means that its interface should expose only access points that are relevant to authentication. And internally, the microservice should have authentication behavior only. For example, there should be no side behavior such as providing employee contact information in the authentication response.

Having a single concern makes the microservice easier to maintain and scale. Having a single concern also goes hand-in-hand with the next principle.

## 2. A microservice is discrete
A microservice must have clear boundaries separating it from its environment. Another way to think about this principle is that a microservice must be well-encapsulated. This means that all logic and data relevant to a microservice's single concern must be encapsulated into a single deployment unit. Examples of units for discrete deployment are a Linux container, a WebAssembly binary, a .NET DLL, a Node.js package, and a Java JAR file, to name a few.

Also, a discrete microservice is hosted in a distinct source control repository and is subject to its own CI/CD (continuous integration/continuous delivery) process. The microservice becomes part of a larger application after deployment. But from development through testing and on to release, each microservice is isolated from all other microservices. When a microservice is discrete, it becomes easily transportable, which is the next principle we'll cover.

