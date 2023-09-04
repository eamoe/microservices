# Microservices

## Preface

The list of required tools:

* Docker
* Redis
* MySQL
* GitHub
* GitHub Actions
* Terraform
* AWS
* kubectl
* Helm
* Argo CD

## Chapter 1: Toward a Microservices Architecture

In the early 2010s, the term *microservices* emerged as a way to describe a new style of software architecture.

Microservices done well enable making software changes faster and safer at scale. Faster and safer means more agility for the business. The agility translates into better outcomes for the business and the organization.

The trick to unlocking all that value is to have the right architecture in place to support the services. It needs to reduce system costs without diminishing the value of independent services. To build that architecture it is necessary to make important decisions early. Those decisions will span methods, processes, teams, technologies, and tools. They'll also need to work together to form an emergent, optimized whole. A good way to build a system like this is through evolution.

According to James Lewis and Martin Fowler's [article](https://martinfowler.com/articles/microservices.html) on microservices from 2014:

> an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms... built around business capabilities and independently deployable by fully automated machinery.

Another definition for microservices from the book *Microservice Architecture* by Irakli Nadareishvili, Ronnie Mitra, Matt McLarty, and Mike Amundsen:

> A microservice is an independently deployable component of bounded scope that supports interoperability through message-based communication. Microservice architecture is a style of engineering highly automated, evolvable software systems made up of capability-aligned microservices.

While there are lots of potential benefits to microservices, the best reason to build software this way is to reduce the coordination costs.

## Chapter 2: Designing a Microservices Operating Model

An operating model is the set of people, processes and tools that underlies the system. It shapes all the decision-making and work that we do when we build software.

In this chapter, we will cover the relationship between teams and microservices implementations with the introduction of a tool called Team Topologies.

According to Melvin Conway's finding in the [article](https://www.melconway.com/Home/pdf/committees.pdf), we can paraphrase the main thesis, called "Conway's Law":

> Any organization that designs a system (defined broadly) will produce a design whose structure is a copy of the organization's communication structure. (Attributed to Frederick Brooks)

There are 3 people factors that have the biggest impact on a microservices system: team size, team skills, and inter-team coordination.

If we go too far towards team independence and autonomy, we’ll introduce system-level inefficiencies and misalignment with organizational goals. If we introduce too much coordination, we risk bogging the whole system down and losing the benefits of highly changeable microservices. The challenge is to strike the right balance between independent work and coordinated efforts. That takes some experimentation and continuous tuning of your team design.

According to the Team Topology, there are 4 team types:
* Stream-Aligned
* Enabling
* Complicated-Subsystem
* Platform

Also, there are 3 interaction modes:
* Collaboration
* Facilitating
* X-as-a-service

To create a team design and Team Topology, we can follow this step-by-step approach:

1. Establish a system design team. This is a group of people who can shape the vision and behavior of the system. It designs team structures, establishes standards, incentives, and "guardrails" as well as continually improves the system.
2. Create a microservices team template for future teams. Microservices teams are expected to own one or more microservices independently. That ownership includes running the service and releasing a continuous stream of improvements, fixes, and changes as needed.
3. Define platform teams. We can instantiate a cloud platform team that offers network, application, and deployment infrastructure to the rest of the organization as a service.
4. Add enabling and complicated-subsystem teams. We can introduce a specialized release team that embodies the complicated-subsystem team type. In this case, microservices teams deliver a built and tested container. However, a microservices team may deploy its own services directly into a production environment.
5. Add key consumer teams. These could be mobile application development teams, web development teams, or even third-party organizations. In this model, the main consumer of the microservices system is the API team which is responsible for exposing the microservices to other development teams.

## Chapter 3: Designing Microservices: The SEED(S) Process

The microservices design system here is a top-down, multistep methodology, and a collection of reusable processes, where each later step evolves from a previous one. Due to its evolutionary nature, it is called Seven Essential Evolutions of Design for Services or SEED(S).

The SEED(S) process provides a repeatable, reliable, and battle-tested methodology for designing service interfaces that are user-friendly and robust.

The 7 steps of the SEED(S) process are:
1. Identifying actors. Too many APIs are simply exposures of some database tables over HTTP or an attempt to provide direct networked access into application internals, via remote procedure calls (RPCs). Such approaches often struggle in delivering for customer needs and achieving business goals. Each actor must be *specific*, more so than *precise*. Actors must be defined in context. Having a company-wide "portfolio" of actors that are reused for each application design is more than an indicator of trouble. As models, actor definitions first and foremost represent the needs, pain points, and behaviors inherent to each actor archetype.
2. Identifying jobs that actors have to do. As Theodore Levitt said: "People don't want to buy a quarter-inch drill. They want a quarter-inch hole!" Job Stories provide a great format for conversations with subject matter experts and actual customers, but they are not convenient for deriving actual technical requirements. Rather, we need to translate them into a more developer-friendly format, which is what the next few sections of the SEED(S) process are all about.
3. Discovering interaction patterns with sequence diagrams. For complex interactions, a linear list of Job Stories will not be able to sufficiently support the design effort. Instead, you will want to draw an interaction diagram, using UML diagrams as in this case.
4. Deriving high-level actions and queries based on jobs to be done (JTBDs) and the interaction patterns.
5. Describing each query and action as a specification, with an open standard (such as the OpenAPI Specification (OAS) or GraphQL schemas). Each Job Story can be translated into multiple queries and actions, and a resulting query or action may combine multiple Job Stories as its source. Microservices interconnections do not have to be RESTful APIs. Other popular choices include GraphQL, gRPC, and asynchronous event communications.
6. Getting feedback on the API specification. Show the draft design of the endpoints to the client developers who will be asked to use these APIs and services, and collect their feedback.
7. Implementing microservices.

## Chapter 4: Rightsizing Your Microservices: Finding Service Boundaries

In this chapter, we look deep into the methodology for the effective analysis, modeling, and decomposition of large domains (Domain-Driven Design), explain the efficiency benefits of using Event Storming for domain analysis, and introduce the Universal Sizing Formula, a guidance for the effective sizing of microservices.

Sizing based on the lines of code would be a poor measurement as well as functional edges. According to [Lewis and Fowler](https://martinfowler.com/articles/microservices.html#OrganizedAroundBusinessCapabilities), microservices should be "organized around business capabilities," not technical needs.

Microservices is primarily about minimization of coordination costs, in a complex, multiteam environment, to achieve harmony between speed and safety, at scale.

Whether you are working on a greenfield project or decomposing an existing monolith, the approach should be to start with only a handful of services and slowly increase the number of microservices over time. If this leads to some of your microservices initially being larger than in their target state, it is OK. You can split them up later.

As Sam Newman introduced in his book [Building Microservices](https://www.oreilly.com/library/view/building-microservices/9781491950340/), we should strive for such a sign that the resulting services are:

* Loosely coupled (unaware and independent of each other with a limited number of different types of runtime calls)
* Highly cohesive (features present in a service should be highly related, while unrelated features should be encapsulated elsewhere. This way, if we need to change a logical unit of functionality, we should be able to change it in one place, minimizing the time to release that change)
* Aligned with business capabilities (if our boundaries are closely aligned with the boundaries of business capabilities, it would naturally follow that the first and second design requirements, above, are more easily satisfied)

The software design methodology known as Domain-Driven Design (DDD) significantly predates microservices architecture. It was introduced by Eric Evans in 2003, in his book [Domain-Driven Design: Tackling Complexity in
the Heart of Software](https://www.oreilly.com/library/view/domain-driven-design-tackling/0321125215/). The main premise of the methodology is the assertion that, when analyzing complex systems, we should avoid seeking a single unified domain model representing the entire system. Rather, as Evans said in his book:

> Multiple models coexist on big projects, and this works fine in many cases. Different models apply in different contexts.

Once Evans established that a complex system is fundamentally a collection of multiple domain models, he made the critical additional step of introducing the notion of *bounded context*. Specifically, he stated that:

> A Bounded Context defines the range of applicability of each model.

Different contexts can use the same words. For example, the term account carries significantly different meanings in the identity and access management, customer management, and financial accounting contexts of an online reservation system.

DDD is complex and it is a team sport. Because of that, it is very difficult to practice.

However, there's a shortcut invented by Alberto Brandolini. It is a fun, lightweight, and inexpensive process called Event Storming, which heavily based and inspired by the concept of DDD but help us find bounded contexts in a manner of hours instead of weeks or months.

Bounded contexts are a good starting point for rightsizing microservices. We have to be cautious, however, do not assume that microservice boundaries are synonymous with the bounded contexts from DDD or Event Storming. They are not. As a matter of fact, microservice boundaries cannot be assumed to be constant over time. They evolve over time and tend to follow an increasing granularity of microservices as the organizations and applications they are part of mature.

To achieve a reasonable sizing of microservices, we should:

* Start with just a few microservices, possibly using bounded contexts.
* Keep splitting as the application and services grow, being guided by the needs of coordination avoidance.
* Be on the right trajectory for decreasing coordination. This is vastly more important than the current state of how “perfectly” you get service sizing.

## Chapter 5: Dealing with the Data

There can be several reasons why we may not be able to make a deployment of our microservices independent, but in the context of data management, the most common offender is co-ownership of a data space by multiple microservices. Such co-ownership can compromise their loose coupling and our ability to independently deploy code.

In monolith architectures, sharing of data is a common practice. In typical legacy systems, even in the more modular, service-oriented architecture (SOA) ones, code components co-own data across multiple services as a regular practice. It is actually very much expected—shared data is a primary pattern of integrating various modularized parts of a larger system.

In a microservices architecture, independent deployability is emphasized as a core value and consequently, data sharing is prohibited — microservices are never allowed to co-own responsibility for a data space in a database. It should be very clear which microservice owns any dataset in the database, or as we commonly state the principle: microservices must own (embed) their data. However, embedding Data Should Not Lead to an Explosion in the Number of Database Clusters.

One way to prevent accessing the same data by multiple microservices is to use a delegate service which works like a proxy between those microservices and the database.

Another option is using shared spaces, such as data lakes which can enable multiple access to data with read-only permissions.

The third possible option is to use sagas (action-compensation pattern).

The Event Sourcing pattern helps to avoid data-sharing. It defines an approach to handling operations on data that's driven by a sequence of events, each of which is recorded in an append-only store. Application code sends a series of events that imperatively describe each action that has occurred on the data to the event store, where they're persisted.

To improve performance while using event sourcing, we can apply rolling snapshots. It just requires finding *natural time points* for the domain and aligning snapshots with them.

To work with events, we need to create an event store. The interface of an event store needs to support three basic functions:

* The ability to store new events and assign the correct sequence so we can retrieve events in the order they were saved
* The capability to notify event subscribers who are building projections about new events they care about and enable the Competing Consumers pattern
* The ability to get N number of events after event X for a specific event type, for reconciliation flows; i.e., recalculation in case projection is lost, compromised, or doubted.

Event Sourcing and CQRS (Command Query Responsibility Segregation) can help us avoid data sharing between microservices in sophisticated cases where you require data joins across service boundaries, but they come with a cost of complexity. We should always consider other, simpler approaches, such as the delegate service, before we resort to Event Sourcing, for a particular microservice.

## Chapter 6: Building an Infrastructure Pipeline

In order to reduce the work that our microservices teams need to do, we’ll need to make it easy for teams to move their code from local workstations onto a hosted infrastructure. So we’ll need to lower the barrier for teams to be able to provision environments and deploy their services into a hosted system. We’ll need to make it cheap and easy to create a new environment and provide the right kit to make releases safe and easy.

In practice, achieving those goals is difficult if you don’t have a good way of improving the way you make changes to the infrastructure itself. If we can reduce the effort cost of building and changing the infrastructure, we’ll be able to deliver new environments more easily and put more focus on improving the infrastructure to meet our system goals.

Building software in the DevOps way helps you reduce the time it takes to make changes to your applications, without introducing additional risk. When you do it right, it gives you both change speed and change safety at the same time.

We’ll use three concepts from the DevOps world in our infrastructure platform:
* Immutable infrastructure
* IaC - Infrastructure as Code
* CI and CD

An object is immutable if it can’t be changed after it’s created. The only way to update an immutable object is to destroy it and create a new one.

## Chapter 7: Building a Microservices Infrastructure

Setting up the right infrastructure is vital to getting the most out of your microservices system. Microservices give us a nice way of breaking the parts of our application into bite-sized pieces. But we’ll need a lot of supporting infrastructure to make all those bite-sized services work together properly.

Containers make it easy for us to build microservices that run predictably across environments as a self-contained unit. But, containers don’t know how to start themselves, scale themselves, or heal themselves when they break. Containers work great in isolation, but a lot of operations work is required to manage them in productionlike environments. That’s where Kubernetes comes in. Kubernetes is a container orchestration tool developed by Google. It solves the problems of working with containers at scale. Kubernetes provides a tool-based solution for deploying, scaling, observing, and managing container-based applications.

GitOps is an operational framework that takes DevOps best practices used for application development such as version control, collaboration, compliance, and CI/CD, and applies them to infrastructure automation.

Argo CD is a GitOps tool that facilitates the work of deploying Kubernetes applications.

## Chapter 8: Developer Workspace

One thing you should certainly avoid is every team creating a pipeline for their microservice in their own way, without any consistency with the codebases of other microservices. Creating a new microservice should be a quick and predictable process. Ideally, it should be a templated process in which the majority of things are fully automated.

Robust CI/CD pipelines are crucial, but just as important is how the local development workspace is set up and what practices teams use for creating code.

When trying to introduce any organizational standards, it’s useful to clarify and agree on goals, so people can relate to the “why” of the process before they are presented with the actual mechanics, the “how” and “what” of it.

We can use the following three high-level goals as a starting point:

* Code can be set up in a short time frame (for example, in under an hour)
* New microservices can be created quickly, easily, and predictably (providing well-thought-out templates for each of the standard tech stacks is a powerful way of achieving such consistency and high quality, while also increasing development speed)
* Quality control must be automated

Based on these goals, we can derive a set of fundamental guidelines for a developer workspace setup.

### 10 Workspace Guidelines for a Superior Developer Experience

1. **Make Docker the only dependency** - The “works for me” syndrome plagues many developer teams. It’s essential that anybody be able to easily create the same environment. As such, elaborate, manual setups should be banned.
2. **Remote or local should not matter** - Setup should work regardless of whether a developer runs code on their own laptop or on a cloud server via an IDE’s remote development/SFTP plug-ins.
3. **Ensure a heterogeneous-ready workspace** - A good setup should accommodate multiple microservices written in multiple programming languages, using multiple data storage systems.
4. **Running a single microservice and/or a subsystem of several ones should be equally easy** - Let’s say an airline reservation system is implemented as three microservices. A developer should be able to check out any particular microservice individually and work on it, or check out an entire subsystem of interacting microservices (the reservation system implementation) and work on that. Both of these tasks should be very easy.
5. **Run databases locally, if possible** - For the sake of isolation, for any database system’s local, Docker-ized alternatives should be provided, and it should be trivial to switch over to cloud (e.g., AWS) services via a configuration change.
6. **Implement containerization guidelines**
7. **Establish rules for painless database migrations**
8. **Determine a pragmatic automated testing practice** - We advocate for a measured, pragmatic approach to automated testing, one that balances developer experience with quality metrics and accommodates the differing personal preferences of various developers on the team.
9. **Branching and merging**

    * All development should happen on feature and bug branches.
    * Merging of a branch to the main branch should not be allowed without all tests (including integration tests in a temporary integration cluster spun up for the branch) passing on that branch.
    * The status of the test runs (after each commit/push) must be readily visible for code reviewers during pull requests.
    * Linting/static analysis errors should prevent code from being pushed to a branch, and/or merged into the main branch.
10. **Common targets should be codified in a makefile** - Every code repository (and generally there should be one repository per microservice) should have a makefile that makes it easy for anybody to work with the code, regardless of the programming language stack used. This makefile should have standard targets, so that no matter what codebase, in whatever language the developer clones, they should know that by running *make run* they can bring that codebase up, and by running *make test* they can run automated tests.

We recommend defining and implementing the following standard targets for your microservice makefiles:

* **start**: Run the code.
* **stop**: Stop the code.
* **build**: Build the code (typically a container image).
* **clean**: Clean all caches and run from scratch.
* **add-module**
* **remove-module**
* **dependencies**: Ensure all modules declared in dependency management are installed.
* **test**: Run all tests and produce a coverage report.
* **tests-unit**: Run only unit tests.
* **tests-at**: Run only acceptance tests.
* **lint**: Run a linter to ensure conformance of coding style with defined standards.
* **migrate**: Run database migrations.
* **add-migration**: Create a new database migration.
* **logs**: Show logs (from within the container).
* **exec**: Execute a custom command inside the code’s container.

Generally, we do not recommend using local Kubernetes for everyday coding. Docker and Docker Compose can complete most containerization-related tasks more easily and they have more straightforward tooling for building container images. Kubernetes excels in orchestrating a runtime fleet of containers, which is rarely needed in a Dev environment, but is crucial for environments such as production, preproduction, staging, performance testing, etc. However, in some circumstances, you may want to use Kubernetes locally.

## Chapter 8: Developing Microservices

Let’s assume that an Event Storming session that you conducted for a flight management software product identified two major bounded contexts:
* Flights management
* Reservations management

In the initial stages it pays off to design microservices in a coarse-grained way. Thus, our first two microservices can be *ms-flights* and *ms-reservations*.

Now we need to use the SEED(S) design process for them. According to the first step of the SEED(S) methodology, we need to identify various actors. For our purposes, we’ll assume the following actors:
* The customer trying to book the flight
* The airline’s consumer app (web, mobile, etc.)
* The web APIs that the app interacts with
* The flights management microservice: ms-flights
* The reservations management microservice: ms-reservations


