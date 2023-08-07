# Microservices

## Preface

The list of requried tools:

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

## Chapter 1: Toward a Microcervices Architecture

In the early 2010s, the term *microservices* emerged as a way to describe a new style of software architecture.

Microservices done well enable making software changes faster and safer at scale. Faster and safer means more agility for the business. The agility translates into better outcomes for the business and the organization.

The trick to unlocking all that value is to have the right architecture in place to support the services. It needs to reduce system costs without diminishing the value of independent services. To build that architecture it is necessary to make important decisions early. Those decisions will span methods, processes, teams, technologies, and tools. They'll also need to work together to form an emergent, optimized whole. A good way to build a system like this is through evolution.

According to James Lewis and Martin Fowler's [article](https://martinfowler.com/articles/microservices.html) on microservices from 2014:

> an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms... built around business capabilities and independently deployable by fully automated machinery.

Another definition for microservices from the book *Microservice Architecture* by Irakli Nadareishvili, Ronnie Mitra, Matt McLarty, and Mike Amundsen:

> A microservice is an independently deployable component of bounded scope that supports interoperability through message-based communication. Microservice architecture is a style of engineering highly automated, evolvable software systems made up of capability-aligned microservices.

While there are lots of potential benefits to microservices, the best reason to build software this way is to reduce the coordination costs.
