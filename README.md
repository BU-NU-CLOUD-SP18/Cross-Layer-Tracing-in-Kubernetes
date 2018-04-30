# Cross-Layer-Tracing-in-Kubernetes
The aim of this project is to add trace points to applications running in Kubernetes and understand applications' behavior by end-to-end tracing.

## Change in plan
As we find that Nginx takes response of Kubernetes external traffic, Our MVP changes to tracing Nginx with Jaeger. 

## Instructions of the project:
1. Create a cluster on MOC: https://github.com/BU-NU-CLOUD-SP18/Cross-Layer-Tracing-in-Kubernetes/blob/master/instructions/Instruction%20of%20create%20a%20cluster%20on%20moc.md
2. Deploy Kubernetes on MOC cluster: https://github.com/BU-NU-CLOUD-SP18/Cross-Layer-Tracing-in-Kubernetes/blob/master/instructions/Instruction%20of%20install%20Kubernetes%20on%20MOC.md
3. Set up Jaeger on MOC instance and show GUI on local computer: https://github.com/BU-NU-CLOUD-SP18/Cross-Layer-Tracing-in-Kubernetes/blob/master/instructions/Install%20Jaeger%20on%20MOC%20node.md
4. Kubernetes logging: https://github.com/BU-NU-CLOUD-SP18/Cross-Layer-Tracing-in-Kubernetes/blob/master/instructions/Kubernetes%20logging.md
5. Containerize an application and make it a service in Kubernetes cluster: https://github.com/BU-NU-CLOUD-SP18/Cross-Layer-Tracing-in-Kubernetes/blob/master/instructions/Containerize%20an%20application%20and%20make%20it%20a%20service.md%20on%20MOC%20cluster.md


## Concepts and components of the project
●	Tracing: Tracing is a method to understand the performance/correctness of deploying distributed applications. When an app makes a request, it will generate a unique request ID and we name it as ‘Traceing ID’. Tracing ID propagate through the system with the request. Every time the request calls a component of the system, an event labeled by request's tracing ID is triggered. If we collect all the events and sort them into different requests by tracing ID, we will see series of events like 'threads' belongs to different requests, from which we can understand apps' behavior.

Three steps of tracing:

1.Adding trace points to datapath: Let commponents on datapth be 'tracable'. 

2.Tracing ID propagation: Figure out a method to make sure tracing ID can propagate though layers.

3.Huge repository storage to store tracing information: Massive tracing information will be generated so we need huge storage to hold them.

●	Open tracing: Since developers and engineers have started to trade in the old monolithic systems for today’s microservice architectures tasks that were easy before have become difficult. Modern day distributed tracing systems aim to address these issues but they do so using application level instrumentation using incompatible APIs. Open Tracing aims to address these issues using consistent, vendor neutral APIs for popular platforms.

●	Jaeger: Jaeger is a distributed tracing system released as open source by Uber Technologies. It can be used for monitoring microservices-based distributed systems. Jaeger backend, Web UI, and instrumentation libraries have been designed from ground up to support the OpenTracing standard.

   Jaeger tracing example
        
   HotRod: a sample application that has had tracing implemented by Jaeger.
        Tutorial link: https://medium.com/opentracing/take-opentracing-for-a-hotrod-ride-f6e3141f7941
        ![alt text](https://github.com/BU-NU-CLOUD-SP18/Cross-Layer-Tracing-in-Kubernetes/blob/master/images/screen_shot_2018-04-29_at_10.42.08_pm.png)
        ![alt text](https://github.com/BU-NU-CLOUD-SP18/Cross-Layer-Tracing-in-Kubernetes/blob/master/images/Screen%20Shot%202018-04-29%20at%2010.43.02%20PM.png)

●	Distributed system: A distributed system is a network that consists of autonomous computers that are connected using a distribution middleware. They help in sharing different resources and capabilities to provide users with a single and integrated coherent network. The computers interact with each other in order to achieve a common goal.

●	Kubernetes: Kubernetes is an orchestration system coordinating a highly available cluster of computers for deploying, scaling and managing containerized components of a distributed application in a datacenter. It makes these applications agnostic and isolated from other containers deployed on the same node e.g. machine. 

![alt text](https://github.com/BU-NU-CLOUD-SP18/Cross-Layer-Tracing-in-Kubernetes/blob/master/images/kube%20arch.png)
![alt text](https://github.com/BU-NU-CLOUD-SP18/Cross-Layer-Tracing-in-Kubernetes/blob/master/images/kube%20arch2.png)

What Kubernetes does:

1.It allocates resources to containers to have them meet the required description

2.It offers a unique namespace to each container

3.It can scale in & scale out an application and make replication) when required

4.Provides an abstraction through which each container is able to communicate with the outside world

●	Container: A container provides an isolated environment with a unique namespace in which an app can run with its environment. The environment satisfies a description of a set of resources required by an app. App can only use the resources defined in this namespace and doesn’t know what is outside its container.

●	Services: A microservice; an abstraction which defines a set of Kubernetes pods and a policy to access them.

●	Ingress: Typically, services and pods have IPs only routable by the cluster network. All traffic that ends up at an edge router is either dropped or forwarded elsewhere. Conceptually, this might look like:

                                                       Internet
                                                          |
                                                     ------------
                                                     [ Services ]

●	Control plane: The Control Plane maintains a record of all of the Kubernetes Objects in the system, and runs continuous control loops to manage those objects’ state. At any given time, the Control Plane’s control loops will respond to changes in the cluster and work to make the actual state of all the objects in the system match the desired state that you provided.

● Data plane: The decision making part of Kubernetes which decides what has to be done with each containers according to its description. Data Plane is the part which enforces all of control plane’s decisions and it allows applications to remain agnostic to their surroundings.

●	End to end tracing: End to End (e2e) Tracing is to follow the execution of requests infrastructure along the entirety of its  “PATH” of propagation (including its dataplane), to provide detailed tracing for capacity planning and performance analysis

## Vision & Goals
We will implement end-to-end tracing for Kubernetes on the data-plane. This includes instrumenting one or more subsystems within the Kubernetes structure. As data-plane features become a part of the flow and behavior of an application, implementing trace points within them allows for a cross-layer, enabling a complex and deeper understanding of an application’s behavior.  If issues come up in a distributed cluster operated by Kubernetes, tracing is an idea method to resolve said issues.


## Scope & Features
We will be instrumenting the services section of Kubernetes with trace points such that we will be able to get information about the behavior of the distributed system as a whole. Specifically we will focus on the data-plane portion of Kubernetes.  The data-plane is the portion of commands which do not focus on the orchestration of deployment tasks, but rather focus on functionalities.

## User story
### MVP
tracing Nginx 
### User story
●	A developer would be able to debug and analyze their deployed distributed applications.

●	Kubernetes developers can look into which requests are present in a particular data plane at some time T.

●	Performance of a node can be determined.

●	Cloud providers and data centers

## Challenges
● Figure out Kubernetes datapath.

● Configure Nginx to add tracing points.




