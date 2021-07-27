
1. Spring Core IOC (Inversion of control)
    1. Spring context library
    2. Two parts
        1. Application context
        2. Bean factory
    3. AnnoationConfigApplicationContext is used majorly now days. It is java based configuration
    4. Context.getBean(“class”)
    5. Spring configuration file
        1. A XML file which mainly contains the classes information and describes how these classes are configured to each other. 
    6. Inversion of control (IOC) container
        1. Spring container uses Dependency Injection for managing the application components by creating objects, writing them together along with configuring and managing their overall life cycles.
        2. XML, java code, or annotations can be used
    7. Dependency Injection
        1. The main idea of DI is that you don’t have to create objects but you just have to describe how they should be created
        2. Constructor vs setter DI
            1. In constructor injection, partial injection is not allowed whereas it is allowed in setter injections
            2. The constructor injection doesn’t override the setter property, whereas same is not true for setter injection
            3. Constructor injection creates a new instance if any modification is done. Creation of new instance is not possible in setter injection
            4. In case where bean has many properties constructor injection is preferred. If it is less setter injection is preferred
    8. Spring beans
        1. Objects forming backbone of application and managed by IOC container
        2. Spring beans are instantiated, configured, wired and managed by IOC container
        3. Beans are created using configuration metadata
    9. Bean wiring
        1. When beans are combined together within the spring container, they are said to be wired
        2. The spring container should know what beans are needed and how the beans are dependent on each other while wiring beans. This is given by XML/Annotations/Java code
    10. Limitations of auto-wiring
        1. Overriding possibility
            1. Dependencies are specified using <constructor-arg> and <property> settings which overrides auto wiring
        2. Data types restriction: primitive data type and string classes cannot be auto wired
2. Spring boot
    1. Spring vs spring boot
        1. Spring framework provides multiple features like dependency injection, data binding, aspect oriented programming (AOP), data access, and many more that helps easier development of web applications where as spring boot helps in easier usage of spring framework by simplifying and managing various loosely coupled blocks of spring which are tedious and have a potential to become messy
        2. It doesn’t requires an application container and it helps in monitoring several components and configures them externally
    2. Features
        1. Spring boot CLI
        2. Starter dependency
        3. Spring initialiser
        4. Auto configuration
        5. Spring actuator
        6. Logging and security
    3. @SpringBootApplication
        1. @COnfiguration + @EnableAutoConfiguration + @ComponentScan
    4. Sources of external configuration
        1. Command line properties
        2. Application properties
        3. Profile specific properties
            1. Application-{profile}.properties file
    5. To exclude a package without using base packages filter
        1. Use exclude attribute while using @SpringBootApplication
    6. To disable specific auto-configuration class
        1. Use exclude attribute with @EnableAutoConfiguration
    7. To disable default web server
        1. In application properties file mention spring.main.web-application-type=none
    8. @RequestMapping
        1. This provides routing information and informs spring that any HTTP request matching the URL must be mapped to respective method
    9. @RestController
        1. This is applied to a class to mark it as a request handler thereby creating Restful web services using spring mvc. This annotation adds the @ResponseBody and @Controler annotation to class
    10. @Lookup
        1. A method annotated with @Lookup tells spring to return an instance of the method's return type when we invoke it
        2. Spring will override our annotated menthod and use our method's return type and parameters as arguments to BeanFactory.getBean
        3. Useful for
            1. Injecting a prototype bean into a singleton bean (Similar to provider)
                eg:
                @Component
                @Scope("prototype")
                public class Address{

                }
                @Component
                public class Person{
                    //members, variables etc

                    @Lookup
                    public Address getAddress(){
                        return null;
                    }
                    //getters, setters etc
                }
            2. Injecting dependency procedurally
                eg:
                   @Component
                    @Scope("prototype")
                    public class Address{
                    
                        private String area;

                        public Address(String area){
                            //set fields
                        }

                        //getters and setters

                    } 

                    public abstract class PersonnServices{

                        @Lookup
                        protected abstract Address getAddress(String area);
                    }

                    At runtime, spring will implement the method in the same way with a couple of additional tricks
                    First, note that it can call a complex constructor as well as inject other spring beans, allowing us to treat Address a bit more like spring-aware method
                    It does this by implementing getAddress with a call to beanFactory.getBean(Address.class,area)
                    Second, we can sometimes make the @Lookup annotated emthod abstract
                    Using abstract is a bit nicer than a stub but we can only use it when we don't component-scan or @Bean-manage the surrounding bean
        4. Limitations
            1. @Lookup annotated method like getAddress must be concrete when the surrounding class like Person is component-scanned. This is because component scanning skips abstract beans
            2. @Lookup annotated method won't work at all when the suurrounding class is @Bean-managed
            In such circumstances we need to use Provider as an alternative
3. Spring MVC
    1. Spring MVC is request driven framework
    2. The MVC Model-View-Controller architecture separates and provides loose coupling between different aspects of the application- input logic (Model), business logic (controller) and UI logic (view)
    3. DispatcherServlet in MVC
        1. Spring MVC is built around a central servlet called DispatcherServlet that handles all HTTP requests and responses
        2. It seamlessly integrates the IOC container and allows you to use each feature of spring in a easier manner
        3. The dispatcher servlet contacts handler mappings to call the appropriate controller for processing the request on receiving. 
        4. The controller calls appropriate service methods to set or process the model data.
        5. The service processes the data and returns the view name to the dispatcher servlet. 
        6. Dispatcher servlet then takes help of view resolver and picks up the defined view for the request.
        7. Once the view is decided, the dispatcher servlet passes the model data to view where it is finally rendered to browser
    4. View resolver pattern
        1. It is a J2EE pattern which allows the application to dynamically choose technology for rendering the data on the browser
        2. The view resolver has the information of different views
        3. The controller returns the name of the view which is then passed to view resolver by dispatcher servlet for selecting appropriate view technology and then data is displayed
        4. The default ViewResolver used in spring mvc is InternalResourceViewResolver
    5. Validations
        1. By using JSR-303 annotations and any reference implementation
        2. Implementing org.springframework.validation.Validator interface and developing customisable validations
    6. ContextLoadListener
        1. The ContextLoadListener loads and creates the application context, so developer need not write explicit code to create it
        2. The application context is where spring bean resides. 
        3. The lifecycle of application context is tied to the lifecycle of the servlet context by using context loader listener
    7. Model
        1. Model is a reference to have the data for rendering
        2. It is always created and passed to the view in spring MVC. 
        3. Any attributes set on the injected model would be preserved and passed to the view
    8. To get servletcontext and servlet config objects in a spring bean
        1. Two ways
            1. Implementing spring-aware interfaces
            2. Using @Autowired annotation on those beans

	
4. Spring AOP
    1. In AOP key unit is aspects or concerns which are nothing but stand alone modules in the application
    2. Scattered aspects are called cross-cutting concerns eg logging, truncation
    3. A cross cutting concern is a concern that could affect the whole application and should be centralised in one location in code as much as possible for security and modularity purposes
    4. 2 ways to implement 
        1. Using XML configuration file
        2. Using AspectJ annotation style
    5. Advice
        1. Advice is implementation of cross cutting concern can be applied to other modules of the spring application.
        2. Types
            1. @Before
                1. Advice executes before a join point. If it throws exception the join point flow won’t proceed
            2. @AfterReturning
                1. This advice is executed after a join point completes normally
            3. @AfterThrowing
                1. This advices is to be executed if a method exits by throwing an exception
            4. @After
                1. This advice is to be executed regardless of the means by which a join point exists
            5. @Around
                1. Surrounds a join point such as method invocation
        3. Spring AOP proxy pattern
            1. A proxy pattern is a well used design pattern where a proxy is an object that looks like another object but adds special functionality to it behind the scenes
    6. Join Point
        1. Is any point in your program such as field access, method execution, exception handling
        2. Spring framework supports method execution join point only
    7. Pointcut
        1. Expression language of spring AOP
    8. Aspect
        1. Is a class in spring AOP that contains advices and join points
    9. Introduction
        1. Represents introduction of new fields and methods for a type
    10. Target object
        1. Is a proxy object that is advised by one or more aspects
    11. Interceptor
        1. Is a class like aspect that contains one advice only
    12. Weaving
        1. Is a process of linking aspects with other application
        2. Spring perform weaving at runtime
    13. AOP implementation
        1. Spring AOP
        2. Apache AspectJ
        3. JBoss AOP
5. Spring JDBC
    1. JDBC Template class
        1. Is the primary api through which we can access database operations logic that we’re interested in
            1. Creation and closing of connections
            2. Executing statements and stored procedure calls
            3. Iterating over the results and returning results
    2. Spring DAO
        1. Data Access object is spring’s support provided to work with data access technologies like JDBC, Hibernate and JPA in a consistent and easy way
6. Spring 5
    1. Reactive programming
        1. Reactive programming is all about non-blocking, event-driven applications that scale with a small number of threads, with back pressure being a key ingredient that aims to ensure producers don’t overwhelm consumers
        2. Benefits
            1. Increased utilisation of computing resources on multi-core and multi cpu hardware
            2. Increase performance by reducing serialisation
        3. Reactive programming is event driven in contrast to reactive systems which are message driven.
        4. Reactive programming doesn’t mean we are building a reactive systems which is architectural style
        5. Reactive systems Characteristics
            1. Responsive
            2. Resilient 
            3. Elastic
            4. Message driven
    2. Spring web flux
        1. Is spring’s reactive stack web framework and is alternative to spring MVC
        2. The entire stack is non blocking
        3. Webflux framework in spring 5 uses Reactor as its async foundation. This provides two core types
            1. Mono to represent a single async value
            2. Flux to represent a stream of async value
            3. Both implement publisher interface defined in reactive streams specification
    3. Webclient and WebTestClient
        1. Webclient is a component in the new web reactive framework that can act as a reactive client for performing non blocking http-request. 
        2. Being a reactive client it can handle reactive streams with back pressure and it can take full advantage of lambda. 
        3. Can work on both sync and async scenarios
    4. Disadvantage of using reactive streams
        1. Troubleshooting is difficult
        2. Limited support for reactive data stores
7. Spring data JPA
    1. Orphan removal
        1. If target entry in one-to-one or one-to-many is removed from the mapping, then remove operation can be cascaded to the target entity. Such target are known as orphan and the orphanRemoval attribute can be used to specify that orphaned entities should be removed
    2. Persistence life cycle of an object
        1. Transient: the object us declared using new keyword. Doesn’t contain any identifier in the database
        2. Persistence: an object is associated with session and either saved to a dabs or retrieved from the database. When an object remains in the persistence state, it contains a row of the database and consists of an identifier value
        3. Detached: The object enters into a detached state when the hibernate session is closed. The changes made to detached objects are not saved to the database
    3. Types of identifier generation
        1. Automatic ID generation:
            1. Application doesn’t care about the kind of id generation and hand over this task to the provider. Default is auto
        2. Id generation using a table: the identifier can be generated using database table
        3. ID generation using a database sequence 
            1. To customise the database sequence name, we can use the JPA @SequenceGenerator annotation
        4. Id generation using a database identity:
            1. Whenever a row is inserted into the table, a unique identifier is assigned to the identity column that can be used to generate the identifiers for the objects
    4. Properties of an entity
        1. Persistability : if object is stored in the database and can be accessed anytime
        2. Persistent Identity: when object identity is stored in a database then it is represented as persistence identity. This object identity is equivalent to the primary key in the database
        3. Transactionality: 
        4. Granularity: Entities should not be primitives, primitive wrappers or built in objects with single dimensional state
    5. Constraints on an entity class
        1. The class must have a no-args constructor
        2. The class can’t be final
        3. The class must be annotated with @Entity annotation
        4. The class must implement a serialisable interface if value passes an empty instance as a detached object
    6. Java collections (List, Set, Map) are used to persist the object of wrapper classes and String
    7. Cascade types
        1. Persist :
            1. If parent entity is persisted then all its related entity will also be persisted
        2. Merge:
            1. If parent entity is merged, then all its related entity will also be merge
        3. Detach:
            1. If parent entity is detached, then all its related entity will also be detached
        4. Refresh:
            1. If the parent entity is refreshed then all its related entity will also be refreshed
        5. Remove
            1. If parent entity is relied then all its related entity Will also be removed
        6. All
            1. All above operations
    8. Criteria API
        1. The criteria api is a specification that provides type-safe and portable criteria queries written using java programming language APIs. It is alternative method for defining JPA queries. 
8. Session management
    1. Is the process of securely handling multiple requests to a web based application from a single user
    2. A session is a series of HTTP requests and transactions created by the same user
    3. Session handling can be done in following ways
        1. Cookies
            1. Is a data sent from website and saved by the user’s web browser on the user’s computer as the user browses
        2. Hidden form field
            1. Is a hidden data which will not be shown to user and can not be modified. 
            2. However, when the user submits the form, hidden data would be sent
        3. URL Rewriting
            1. Is a method of modifying the URL parameters
        4. HttpSession
            1. Enables data to be associated with individual visitors
    4. In a distributed system we manage session by
        1. Sticky session
            1. In this type of session, load balancer would always route same client request to same node.
            2. But here if the node goes down, session would also be gone
        2. Session Replication
            1. To overcome sticky session problem, session replication replicates session data to multiple servers.
            2. So in case node goes down, session data would always be available with other nodes
        3. Session data in persistent datastore
            1. In this session would not be stored in server memory, instead, it will be store in DB with unique ID called session ID
9. To Instantiate a class from a third-party library as spring bean
    1. Use @Configuration on class and then @Bean on method which will create the bean
10. Exception handling using RestControllerAdvice
    1. Rest API developer will have 2 requirements related to error handling
        1. Common place for error handling
        2. Similar error response body with proper HTTP status code across APIs
    2. We have to create a class and annotate it with @RestControllerAdvice
    3. Then we need to create method for each type of exception handling
    4. Annotate these methods with @ExceptionHandler( value = ExceptionType.class)
    5. ExceptionHandler can be used in a single controller also but that will limit the method usage to that controller

