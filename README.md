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

## 3. A microservice is transportable
A transportable microservice can be moved from one runtime environment to another with little effort. Perhaps currently, the optimal form of a transportable microservice is a Linux container image.

Usually, a Linux container image is hosted in an image repository such as Red Hat Quay.io. The container image can be targeted to any destination from that image repository, so a variety of applications can use the image. This is all possible because the microservice is encapsulated into a discrete deployment unit that can be transported to any destination. The encapsulation removes from developers all tasks except configuration and deployment.

Transportable microservices also make them easier to use in an automated or declarative deployment process.

## 4. A microservice carries its own data
A microservice should have its own data storage mechanism that is isolated from all other microservices. The only way data can be shared with other microservice is by way of a public interface that the microservice publishes.

This principle imposes some discipline on data sharing: For instance, the particular data schema used by each microservice has to be well-documented. The design rules out behind-the-scenes hanky-panky that makes data hard to access or understand.

The principle that a microservice carries its own data is hard for many developers to accept. The common argument against a microservice carrying its own data is that the principle leads to a proliferation of data redundancy.

For example, imagine an e-commerce application. That application might have a microservice that manages customer profile information. The application has another microservice that handles purchases. When the principle that every microservice carries its own data is in force, it's quite possible that the purchases microservice might have data that is redundant with the customer profile microservice. Such data redundancy goes against the grain of developers who embrace the DRY principle (Don't Repeat Yourself).

On the other hand, developers who embrace the carry-their-own data principle understand the benefits and have adjusted accordingly. When a microservice carries its own data, any strange behavior is confined within the microservice.

When microservices try to share data, one microservice can make a change that causes a side effect in another microservice. This is fundamentally a bad way of doing business.

One of the key benefits of a microservice carrying its own data is that it enforces all of the other principles. This is particularly important when it comes to the final principle: That a microservice is ephemeral.

## 5. A microservice is ephemeral
The principle that a microservice is ephemeral means that it can be created, destroyed, and replenished on demand on a given target easily, quickly, and with no side effects. The standard operating expectation is that microservices come and go all the time, sometimes due to system failure and sometimes due to scaling demands.

This scenario is common in a Kubernetes environment that uses the Horizontal Pod Autoscaler (HPA) to accommodate scaling demands. The HPA creates and destroys containers according to momentary demands. Each time a container is created, an IP address is assigned dynamically. There are even situations where port numbers will be assigned dynamically too. Such are the impacts of ephemeral computing.

As a result, this principle that a microservice is ephemeral has two basic implications. The first is that developers need to create microservices that are good citizens in the application domain. This means implementing graceful startup and shutdown behavior within the microservice.

The second implication is that when programming their microservices, developers rely on runtime configuration settings to define external dependencies. This hand-off to an external configuration differs greatly from creating a monolithic application, where most dependencies are known at design time and are baked into the code. In microservice development, they're not. Instead, developers rely upon dynamic configuration to establish dependencies that are both internal and external to the microservice.

As strange as it might sound, coding to an ephemeral environment requires developers to accept that there are "known unknowns" that will be apparent at runtime. Hence, the need to program accordingly.
