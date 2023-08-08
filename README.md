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

An operating model is the set of people, processes and tools that underlies the system. It shapes all the decision making and work that we do when we build software.

In this chapter, we will cover the relationship between teams and microservices implementations with introduction of a tool called Team Topologies.

According to Melvin Conway's finding in the [article](https://www.melconway.com/Home/pdf/committees.pdf), we can paraphrase the main thesis, called "Conway's Law":

> Any organization that designs a system (defined broadly) will produce a design whose structure is a copy of the organization's communication structure. (Attributed to Fredertick Brooks)

There are 3 people factors that have the biggest impact on a microservices system: team size, team skills, and interteam coordination.

If we go too far towards team independence and autonomy, we’ll introduce systemlevel inefficiencies and misalignment with organizational goals. If we introduce too much coordination, we risk bogging the whole system down and losing the benefits of highly changeable microservices. The challenge is to strike the right balance between independent work and coordinated efforts. That takes some experimentation and continuous tuning of your team design.

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

1. Establish a system design team. This is a group of people that who can shape the vision and behavior of the system. It designs team structures, establishes standards, incentives, and "guardrails" as well as continually improves the system.
2. Create a microservices team template for future teams.
3. Define platform teams.
4. Add enabling and complicated-subsystem teams.
5. Add key consumer teams.

