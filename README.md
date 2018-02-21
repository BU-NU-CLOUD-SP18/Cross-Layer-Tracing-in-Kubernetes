# Cross-Layer-Tracing-in-Kubernetes
The aim of this project is to add trace points to applications running in Kubernetes and understand applications' behavior by end-to-end tracing.

## Concepts and components of the project
●	Container: A container provides an isolated environment with a unique namespace in which an app can run with its environment. The environment satisfies a description of a set of resources required by an app. App can only use the resources defined in this namespace and doesn’t know what is outside its container.

●	Kubernetes: Kubernetes is an orchestration system coordinating a highly available cluster of computers for deploying, scaling and managing containerized components of a distributed application in a datacenter. It makes these applications agnostic and isolated from other containers deployed on the same node e.g. machine. 

What Kubernetes does:

1.It allocates resources to containers to have them meet the required description

2.It offers a unique namespace to each container

3.It can scale in & scale out an application and make replication) when required

4.Provides an abstraction through which each container is able to communicate with the outside world

●	Control plane & Data plane: The decision making part of Kubernetes which decides what has to be done with each containers according to its description. Data Plane is the part which enforces all of control plane’s decisions and it allows applications to remain agnostic to their surroundings.

●	Tracing: Tracing is a method to to understand the performance/correctness of deploying distributed applications. When an app makes a request, it will generate a unique request ID and we name it as ‘Traceing ID’. Tracing ID propagate through the system with the request. Every time the request calls a component of the system, an event labeled by request's traing ID is triggered. If we collect all the events and sort them into different requests by tracing ID, we will see series of events like 'threads' belongs to different requests, from which we can understand apps' behavior.

Three steps of tracing:

1.Adding trace points to datapath:  

2. Tracing ID propagation: By collecting tracing points and sort, we get a ‘thread’ of movement of  this specific request.

●	Jaeger: a distributed tracing used for monitoring microservices-based distributed systems.

●	Services: A microservice; an abstraction which defines a set of Kubernetes pods and a policy to access them.

●	Ingress: A collection of rules that allow inbound connections to reach the cluster services.

●	HotRod: a sample application that has had tracing implemented by Jaeger.

●	OSProfiler: Another tracing implementation that may be used.


## Vision & Goals
We will implement end-to-end tracing for Kubernetes on the data-plane. This includes instrumenting one or more subsystems within the Kubernetes structure.  As data-plane features become a part of the flow and behavior of an application, implementing trace points within them allows for a cross-layer, enabling a complex and deeper understanding of an application’s behavior.  If issues come up in a distributed cluster operated by Kubernetes, tracing is an idea method to resolve said issues.

## Users/Personas of the Project
This project is meant to assist the users of the Kubernetes platform in identifying issues like latency, performance of particular machine, bottlenecks etc.  in their distributed cluster.  Users include large companies, who have made tracing the de facto method to debug and analyze distributed applications.

## Scope & Features
We will be instrumenting the services section of Kubernetes with trace points such that we will be able to get information about the behavior of the distributed system as a whole. Specifically we will focus on the data-plane portion of Kubernetes.  The data-plane is the portion of commands which do not focus on the orchestration of deployment tasks, but rather focus on functionalities.


## Acceptance Criteria
Implement end to end tracing for n number of requests to a distributed system containing at least n number of machines in parallel through the Kubernetes data-plane.

## Release Planning
Short Term Goals: 

●	Get Kubernetes on our laptops.

●	Create and run applications in containers

●	Implement HotRod using Jaeger. 

●	Tutorials on Kubernetes and Tracing.
