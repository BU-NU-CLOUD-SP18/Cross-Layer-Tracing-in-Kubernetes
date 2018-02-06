# Cross-Layer-Tracing-in-Kubernetes
Cross-Layer Tracing in Kubernetes

## Vision & Goals
We will implement end-to-end tracing for Kubernetes on the data-plane. This includes instrumenting one or more subsystems within the Kubernetes structure.  As data-plane features become a part of the flow and behavior of an application, implementing trace points within them allows for a cross-layer, enabling a complex and deeper understanding of an application’s behavior.  If issues come up in a distributed cluster operated by Kubernetes, tracing is an idea method to resolve said issues.

## Users/Personas of the Project
This project is meant to assist the users of the Kubernetes platform in identifying issues like latency, performance of particular machine, bottlenecks etc.  in their distributed cluster.  Users include large companies, who have made tracing the de facto method to debug and analyze distributed applications.

## Scope & Features
We will be instrumenting the services section of Kubernetes with trace points such that we will be able to get information about the behavior of the distributed system as a whole. Specifically we will focus on the data-plane portion of Kubernetes.  The data-plane is the portion of commands which do not focus on the orchestration of deployment tasks, but rather focus on functionalities.

## Solution Concept
Below are the components of our design:
●	Container: A container provides an isolated environment with a unique namespace in which an app can run with its environment. Apps can only use the resources defined in this namespace.
●	Kubernetes: a container orchestrator, where tracing will be implemented.Kubernetes is an open-source platform designed to automate deploying, scaling, and operating application containers; a container deployment orchestrator.  
●	Tracing: Every request has Its own label, we name it as ‘TraceID’. When a specific  request call an API in a components of a system, we can create a event labeled by its ‘TraceID’. By collecting these events, we get a ‘thread’ of movement of  this specific request.
●	Jaeger: a distributed tracing used for monitoring microservices-based distributed systems.
●	Services: A microservice; an abstraction which defines a set of Kubernetes pods and a policy to access them.
●	Ingress: A collection of rules that allow inbound connections to reach the cluster services.
●	HotRod: a sample application that has had tracing implemented by Jaeger.
●	OSProfiler: Another tracing implementation that may be used.

## Acceptance Criteria
Implement end to end tracing for n number of requests to a distributed system containing at least n number of machines in parallel through the Kubernetes data-plane.

## Release Planning
Short Term Goals: 
●	Get Kubernetes on our laptops.
●	Create and run applications in containers
●	Implement HotRod using Jaeger. 
●	Tutorials on Kubernetes and Tracing.



