#Microservices

1. What is spring cloud?
    1. Provides cloud to quickly build common patterns in distributed systems
    2. Configuration Management —> spring cloud config server
    3. Dynamic scale up and down
        1. Naming server —> Eureka
        2. Ribbon —> Client side load balancing
        3. Feign —> Easier Rest Clients
    4. Visibility and monitoring
        1. Zipkin Distributed Tracing
        2. Netflix api gateway
    5. Fault tolerance
        1. Hystrix
2. What is 12 factor app?
    1. It is a methodology for building software as a service apps that
        1. Use declarative formats for setup automation, to minimise time and cost for new developers
        2. Have a clean contract with underlying operating systems, offering maximum portability between execution environments
        3. Are suitable for deployment  on modern cloud platforms
        4. Minimize divergence between development and production, enabling continuous deployment for maximum agility
        5. And can scale up without significant changes to tooling. 
    2. The factors are
        1. Codebase
            1. One codebase tracked in revision control, many deploys
        2. Dependencies
            1. Explicitly declare and isolate dependencies
        3. Config
            1. Store config in environment
        4. Backing services
            1. Treat backing services as attached resources
        5. Build, release, run
            1. Strictly separate build and runs stages
        6. Processes
            1. Execute the app as one or more stateless process
        7. Port binding
            1. Export services via port binding
        8. Concurrency
            1. Scale out via the process model
        9. Disposability
            1. Maximize robustness with fast startup and graceful shutdown
        10. Dev/Prod parity
            1. Keep development, staging and production as similar as possible
        11. Logs
            1. Treat logs as event streams
        12. Admin processes
            1. Run admin/management tasks as one-off processes
3. Server side load balancing
    1. Can be achieved by utilisation of Netflix Zuul
    2. Is also known as JVM based router
    3. It is also regarded as a load balancer by Netflix
    4. Zuul can be integrated with other type of Netflix services that are known as Hystrix
    5. Can also be used to manage routing tables and effective balancing of load across the system
4.  Use of Netflix Hystrix
    1. Hystrix is meant for tolerance of various types of faults that are commonly present in Eureka. By tolerating various kinds of faults, service discovery can be made easier within the realm of Microservices
    2. Is also known as an error tolerance and latency library
    3. Main purpose of Hystix is to make sure that it isolates the access points
    4. On the other hand, Using the access points, remote systems can be easily reached
    5. It also makes sure that it restricts the widespread use of 3rd party libraries as well as services
    6. It makes sure that application run in an efficient manner
    7. It is quite effective in prohibiting failures that frequently takes place in distributed systems that are quite complex in nature
5. Aspects of using spring profile
    1. It allows the users in the process of registering various beans.
    2. The registration process of beans is always dependent on various ways by which the application has been executed
6. Key Principles of microservices are
    1. Single responsibility principle :
        1. It states that any class or module in micro services should have a single responsibility
        2. Having multiple responsibility lead to tight coupling and result in fragile design that are hard to evolve and can break into unexpected ways upon changing
    2. Loose coupling:
        1. Dependencies between services are minimised though loose coupling
    3. Fault tolerance
        1. Microservices will be necessarily built fault-tolerant so that failures on the side of its collaborating services will have less impact on its own SLA
    4. Infrastructure automation:
        1. Each service is built by embedding all dependencies and running as standalone
    5. Deployment:
        1. Microservices are platform agnostic. It implies the services designed and deployed independently without affecting others
7. Types of Microservices
    1. Stateless microservices
        1. Are building blocks of distributed systems
        2. They don’t maintain a session state between requests
        3. If any service is removed, it won’t affect the overall performance logic for the service
    2. Stateful microservices
        1. Less preferred in real life
        2. They maintain session information in the code
        3. And when more than two services interact with each other, they keep a service request. State
8. Advantages of micro services
    1. Are easily scalable:
        1. Since the services are separate, you can easily scale the needed ones at the required times instead of complete application
    2. Reduces downtime through fault isolation
        1. Large apps can remain unaffected for single module failure
    3. Smaller and faster deployments
        1. Can be deployed independently, enabling continuous improvement and faster updates
    4. Ease of understanding
        1. Developers can easily understand functionality of a service
9. Disadvantages of microservices
    1. High Operational overhead:
        1. Microservices are frequently deployed on their containers or VM, causing an increase in VM wrangling work
    2. Perceptibility:
        1. As we know, microservices contain minimal services to deploy and maintain. It becomes tough to monitor the problems within in
    3. Configuration management:
        1. As it contains several small services, there is a great need to manage all services configurations across various environments
    4. Debugging
        1. It becomes difficult for developer to check very. Service of architecture for an error. And debugging can be complicated
    5. Automating the components:
        1. Automate the entire cycle of build, deployment to monitoring becomes more complicated
    6. Consistency:
        1. Maintaining data consistency between services is a challenging task
    7. Testing:
        1. Testing the interaction between services becomes more complicated
    8. Communication between services is complex:
10. Microservices tools
    1. Docker
        1. An open source tool that allows building and deploying apps using containers. 
        2. Developers can run application as a single package using these containers
        3. Provides a static background to run thus avoiding deployment issues
    2. Kubernetes:
        1. Kubernetes, as an fine orchestrates the entire process of thousands of services
    3. Jaeger
        1. It is open source end to end distributed tracing tool.
        2. Monitors distributed transactions, helps in performance optimisation and finds the dependencies between services
    4. Hystrix:
        1. Hystix is a fault tolerance library developed to isolate access points to remote systems, services and 3rd party libraries
        2. It is error tolerance and latency library
        3. We can use Hystrix to ensure that an application runs efficiently and avoids the kind of failures that occur in distributed systems
    5. AWS lambda
        1. This tool supports infrastructure less servers for microservices builds and user charged on the Pau per use rate. 
        2. Mostly we use this till for hosting REST or API service in combination with AWS API gateway
    6. Fluent
        1. Fluent provides a single logging layer and simplifies this issue. 
        2. Logs can be also be connected and integrated onto a data source
    7. Promethus
        1. Is a monitoring tool used to detect the strange patterns of microservices
        2. Check if everything is working fine.
        3. It is a time series data store
        4. Collects metrics from an application and displays it in a graphical format
    8. Grafana:
        1. Provides analytics and monitoring into different visualisation like graphs, charts etc
    9. Nginx
        1. It acts as a reverse proxy
        2. It acts as a single point entry through which all api calls are made
    10. Logstash
        1. Is an open source tool used for checking the logs. It allows you to stash, centralise and transform data of microservices
    11. RabbitMQ
        1. This tool employed patterns to interact between microservices and also scale the application simultaneously. 
        2. Using this tool, you can connect microservices to solve problems of distributed systems
    12. Apache Kafka
        1. Is a distributed stream processing platform used for data processing or API calls
        2. It is an event queue system
        3. All transactions are processed via the event queue, thus avoiding the web like random interactions between different services.
        4. Renders a MS architecture robust and clean
    13. MongoDB
        1. It is open source document based distributed DB
    14. Elasticsearch: 
        1. it is a full-text search engine
    15. Jenkins
        1. It is an automation tool that enables CICD
11. What is restful
    1. Represntational State Transfer (REST) web services is an architectural style that helps computer systems to communicate over the internet.
    2. These web services make microsevices easier to understand and implement
12. Three types of tests for microservices
    1. At the bottom level test
        1. We can perform a general test like performance and unit tests
        2. These are entirely automated tests
    2. At the middle level,
        1. We can perform exploratory tests like stress tests and usability test
    3. At the top level
        1. We can conduct acceptance tests which are mostly fewer in numbers
        2. It also helps stakeholders to know about different software features
13. What are client certificates
    1. Is a digital certificate used to make authenticated requests to a remote server. It is termed as client certificate
14. Use of PACT in microservices
    1. It is an open source tool which allows testing interactions between service providers and consumers
    2. However, it is separate from the contract made
    3. This increases reliability of the MS applications
    4. Each PACT is a collection of interactions
    5. It can be used to implement customer driven contracts in MS
15. What is OAuth
    1. OAuth means open authorisation protocol. This protocol allows you to access the client application on HTTP for third-party providers.
    2. It helps to share resources stored on one site with another site without the need for their credentials
16. What is End to End MS testing
    1. Validates every process in the workflow is functioning correctly.
    2. It also ensures that the system works together as a whole and satisfies all requirements
17. Why are containers used in microservices
    1. Containers are easiest and effective method to manage the Microservice based application. It also helps you to develop individually.
    2. Docker allows you to encapsulate your MS in a container image along with its dependencies
18. Semantic monitoring in MS
    1. Running a subset of the applications automated tests against the live production system
    2. These results are monitored and alerts are generated in case of failure
    3. It also detects the faulty service layer and corresponding MS instance, all at the same flow.
    4. This approach allows for faster triaging and reduces the meantime to repair
    5. Combine automated testes with monitoring of the application. It allows you to find out reasons why your business in not getting profits
19. What is CDC
    1. Consumer driven contract
    2. It is a pattern for developing g mciroservices so that external systems can use them
20. What are reactive extensions in microservices
    1. Also called Rx
    2. It is a design pattern which allows collecting results by calling multiple services and then compile a combined response.
    3. Rx is a popular tool in distributed systems which works exactly opposite to legacy flows
21. Explain continuous monitoring
    1. A method used for searching compliance and risk issues associated with a company’s operational and financial environment
    2. It contains human, processes, and working systems which support efficient and actual operations
22. Strategies of microservices deployment
    1. Multiple service Instance per Host:
        1. Run single or multiple instances of the application on single/multiple physical/virtual host
    2. Service Instance per host:
        1. Run a service instance per host
    3. Service Instance per container:
        1. Run each service instance in its respective container
    4. Serverless deployment
        1. Package the service as a zip file and upload it to the lambda function. The lambda function is a stateless service that automatically runs enough micro-services to handle all requests
23. Difference between cohesion and coupling
    1. Coupling: It is the relationship between module A and another module B. Any module can be highly coupled, loosely coupled and uncoupled with other modules.
        1. The best coupling is loose coupling achieved through interfaces.
    2. Cohesion: It is relationship between 2 or more parts within a module. If a module has high cohesion, it means the the module can perform a certain task with utmost efficiency on its own. Without communication with other modules. High cohesion enhances the functional strength of a module
    3. Loose coupling and high cohesion is key to MS design
24. What are the problems solved by spring cloud
    1. Network issues, latency overhead, bandwidth issues, security issues and other issues with distributed systems
    2. Redundancy issues that occur in distributed systems
    3. Balancing the distribution of load between resources like network links, CPU, clusters etc
    4. Performance issues because of operational overhead
    5. Service discovery issues to ensure smooth communication between services in a cluster
25. Distributed Transaction
    1. Distributed Transaction has two or more network hosts that are engaged. 
    2. Transactions are handled by a transaction manager that takes care of developing and handling transactions. If the transaction involves more than one peer, transaction managers of each peer communicate with each other using subordinate or superior relationships
    3. Same way. Resources are also handled by the resource manager that also coordinate with the distributed transaction coordinator for transaction atomicity and isolation
26. What is end to end testing
    1. Testing technique used to test the entire flow of an application using a business transaction. Since several components are involved in microservices architecture, these tests can cover the gaps during a unit or integration testing. It also gives end to end  confidence, ensures that the network parameters are appropriately configured and helps MS to evolve
    2. Steps
        1. Define what you expect from e2e testing
        2. Define the scope of system to be tested
        3. Perform authentication in a test environment
        4. Choose a testing framework that addresses most of the issue
        5. Test Asynchronous flaws
        6. Automate Testing
27. Mike Cohn’s test pyramid
    1. The pyramid helps maximise automation at all levels of testing. 
    2. The pyramid indicates that while unit tests are faster and more isolated, UI tests which are at highest levels, take time and focus on integration
    3. Slower —> UI Testing —> Integration
    4.                    Service Testing
    5. Faster —> Unit Testing —> Isolation
    6. Two points that can be derived are
        1. Define tests with different granularity
        2. The higher in the level you get, the fewer tests you should have
28. Implement spring security
    1. Add spring-boot-starter-security in pom
    2. Create a spring config class that will override the required method while extending the WebSecurityConfigurerAdapter to achieve security in the application
29. What is actuator
    1. The actuator brings production ready features into an application
    2. It is mainly used to expose operational information about the running application’s health, metrics, info, dump, enc etc
    3. It uses http endpoints or JMX beans to interact with it
30. What is contract testing
    1. Ensures that explicit and implicit contracts of microservices architecture works as expected
    2. There are two perspectives to contract to test
        1. Consumer
        2. Provider
    3. The consumer is the (application) entity using th MS, and the provider is the (application) entity providing the service
    4. Such services work under predefined specifications and contract testing ensures so
31. Mock vs. stub
    1. Mock:
        1. A mock is generally a dummy object where certain features are set into it initially. Its behaviour mainly depends on these features which are then tested
    2. Stub:
        1. Is an object that helps in running the test. It functions in a fixed manner under certain conditions. This hard-coded behaviour helps the stub to run the test
32. Reactive extensions 
    1. Reactive extensions is a design approach through which results are collected by calling multiple services in order to compile a combined response.
    2. Known as Rx, these calls cab be synchronous or asynchronous
33. Spring batch
    1. Is an open source framework for batch processing - execution of a series of jobs
    2. Spring batch provide classes and APIs to read/write resources, transaction management, job processing statistics, job restart and partitioning techniques to process high volume data
34. Tasklet & Chunk
    1. The tasklebt is a simple interface with one method to execute.
    2. A tasklebt can be used to perform single tasks like running queries, deleting files etc
    3. In spring batch, the tasklebt is an interface that can be used to perform unique tasks like clean or set up resources before or after any step execution
    4. Chunk:
        1. Spring batch uses a ‘Chunk Oriented’ processing style within its most common implementation. 
        2. Chunk Oriented Processing refers to reading the data one at a time and creating chunks that will be written out, within a transaction boundary
35. Exception handling
    1. Add @ResponseStatus for exceptions that you write
    2. For all other exceptions, implement an @ExceptionHandler method or @ControllerAdvice class or use an instance of SimpleMappingExecutionResolver
    3. For controller specific exceptions, add @ExceptionHandler methods to your controller
    4. Point to be noted is that @ExceptionHandller methods on the controller are always selected before those on any @ControllerAdvice instance.
36. Access restful microservices
    1. Each MS needs to have an interface
    2. Can be accessed in two ways
        1. Using a REST template that is load balanced
        2. I am using multiple MS
37. How do independent MS communicate with each other
    1. HTTP for traditional request-response
    2. Websockets for streaming
    3. Brokers for Server programs running advanced routing algorithms
    4. For message brokers, RabbitMQ, Nats, Kafka etc can be used
38. Security testing in MS
    1. Code scanning:
        1. In order to ensure that every line of code is bug free and can be replicate
    2. Flexibility:
        1. The security protocols should be flexible as per requirements of the system
    3. Adaptability:
        1. Security protocols should be adaptable to malicious intrusions
39. Idempotence
    1. Refers to the repeated performing of a task even tough the end result remains the same
    2. It is mostly used as a data source or a remote service in a way that. When it receives the instruction more than once, it processes the instruction only once
40. Reports and dashboard in MS env
    1. Find which MS support which resource
    2. Find out the service that are impacted whenever changes in components are made
    3. Provide an easy point of access for documentation purpose
    4. Review versions of the deployed components
    5. Obtain compliance from the components
41. Statemachine
    1. Each MS owning its database is an independently deployable program
    2. This enables creation of state machines by which we can specify different states and events for a particular MS
42. WebMVC test automation use
    1. Used for unit testing of spring MVC applications, where test objective is focused on MVC components
    2. @WebMvcTest(value= ToTestController.class, secure = false)
    3. In this only ToTestController will be launched no other controller or mapping will be launched
43. Features of MS
    1. Decoupling
    2. Componentization
    3. Business capabilities
    4. Autonomy
    5. Continuous delivery
    6. Responsibility
    7. Decentralised governance
    8. Agility
44. Practice to design MS
    1. Separate data store for each MS
    2. Treat servers as stateless
    3. Keep code at similar maturity level
    4. Separate build for each MS
    5. Deploy into containers
45. Domain driven design
    1. Focuses on core domain logic
    2. Finds complex design on models of the domain
    3. Constantly collaborate with domain experts to improve application model and to resolve domain related issues
    4. Need
        1. Mapping to domain
        2. Reduced complexity
        3. Testability
        4. Maintainability
        5. Knowledge rich design
        6. Brings business & service together
        7. Context focussed
        8. Ubiquitous language
46. Ubiquitous language
    1. It is a common language used by developers and users of a specific domain through which the domain can be explained easily
    2. The Ubiquitous language has to be crystal clear so that it brings all the team members on the same page and also translates in such a way that machine can understand
47. Bounded context
    1. Is a central pattern in domain driven design.
    2. It is the focus of DDD’s strategic design section which is all about dealing with large models and teams. 
    3. DDD deals with large models buy dividing them into bounded contexts and being explicit about their inter-relationships
48. Conway’s law
    1. Any organisation that design a system (defined broadly) will produce a design whose structure is a copy if the organisation’s communication structure
49. DRY
    1. Don’t Repeat yourself
    2. It basically promotes the concept of reusing the code.
    3. This results in developing and sharing the libraries which in turn result in tight coupling
50. Cross functional testing
    1. Is a verification of non functional requirements I.e those requirements which cannot be implemented like normal feature
