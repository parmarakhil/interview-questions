#Spring boot

1. @AutoConfiguration
    1. Allows for configuration classes to be scanned dynamically
    2. Usually based off jars loaded on class path
    3. Driven off of spring.factories
    4. Can be controlled using
        1. @AutoConfigureBefore
        2. @AutoConfigureAfter
    5. Conditional Loading
        1. @ConditionalOnClass
        2. @ConditionalOnBean
        3. @ConditionalOnProperty
        4. @ConditionalOnMissingBean
    6. Properties
        1. Preconfigured default properties for auto configuration classes
        2. @EnableConfigurationProperties specifies the default property set
        3. Can always be overridden
    7. Application type based
        1. Web application
        2. Not web app
    8. Resource based
    9. File based
2. Configuring Spring
    1. Property based configuration
        1. Application property or yaml provide basic configurations for basic applications
        2. Environment variables
        3. Command line injections
        4. Cloud configurations eg config server, vault, consul
    2. Bean configuration
        1. Adding beans to the default application class for demo applications
        2. Adding beans to separate configuration classes
        3. Importing XML based configurations
        4. Component scanning
3. Profiles
    1. Flex configuration based on environment
    2. Valuable in real world, multi env deployment
    3. Valuable for live vs cold prod domains as well
    4. Application.yml
        1. Spring boot provides xml supports natively
        2. Allows properties to flex by profile among other things
        3. Spring.profiles is key
        4. Other ways to trigger configs based on profile
        5. Engaging profiles
            1. Spring.profiles.active
            2. You can also inject via command line or env
4. Tomcat
    1. Default includes embedded tomcat server
    2. Can use undertow or jetty if preferred
    3. Default configuration
5. Json Marsheller
    1. With spring web you get the Jackson JSNON marshaller
    2. Useful for restful web services
    3. Automatic marshalling and unmarshalling in web flows
6. Logging framework
    1. SLF4J included
    2. Spring boot builds its own loggers
    3. Leverage properties to modify log levels
    4. log4J can be configured
7. Spring libraries
    1. Spring boot auto Configuration
    2. Starters for tomcat, logging, boot
    3. Spring libraries include core, AOP, beans, context, expression
    4. Spring web and webmvc
    5. SnakeYAML to read xml
    6. Validators (java and hibernate)
8. Servlets, Filters and listeners
    1. Spring boot auto configures the default servlet for all responses at “/“
    2. Any class of these types that are beans will be registered to embedded container
    3. Additional ServletContext can only be loaded through the ServletContextIntializer interface
9. Property based config
    1. Server.address, server.port
    2. Session based configs
    3. Error page path
10. Compression
    1. Server.compression.enabled = true
    2. Response must be 2048 bytes to compress by default
    3. Default response types of text/html, text/xml etc
11. TLS/SSL
    1. Native SSL support via property management
    2. Most common embedded servlet change
    3. Requires a java keystone that contains the certificate
    4. Properties used to configure
12. Spring MVC
    1. Spring boot provides default configurations for spring MVC
    2. Simple paradigm based on model-view-controller
    3. Template engine starter provides view resolvers
    4. Static file resolvers build in as well
13. Spring MVC root
    1. Leverages the same MVC pattern as web apps for restful
    2. The view is the supported mime type
    3. Json and xml for restful services
    4. SOAP is possible in a contract first model
14. Devtools
    1. Allows reloading of the application context while the application is running
    2. Triggered from class path changes
    3. Only for development purposes
    4. Does not impact class loading
15. Jar files
    1. Produces a fat jar
    2. Default behaviour is Jar packaging
    3. Executable
    4. Registrable with systems or init.d
16. War files
    1. Spring boot supports war files
    2. Executable and traditional (types)
    3. Modify build (set maven packaging to war)
    4. Exclude spring-boot-starter-tomat from spring-boot-starter-web
17. Running a spring boot application
    1. Jar file
        1. Java -jar command
        2. Shell scripts
        3. *nix systems or init.d
        4. Cloud ecosystem
    2. War files
        1. Install to web application server
18. Spring data
    1. DataSources
        1. When properly configured, you will Get a DataSource object
        2. Can only have one database auto configured
        3. Datasource can be injected if needed
        4. Spring boot will configure repositories for spring data
19. Spring security
    1. Basic security
        1. Spring security gives you basic authentication on all endpoints except common ignored ones
        2. Username and password is printed in logs
    2. Form based
        1. Full support for forms based authentication
        2. Create extension of WebSecurityConfigurerAdapter
        3. Use @EnableWebSecurity
        4. Backend with database or in memory
    3. OAuth2
        1. Full support for OAuth2, server, client
        2. Default implementation @EnableOAuth2Client
        3. @EnableAuthorizationServer
        4. Resource server : @EnableResourceServer
    4. Password should be hashed not encrypted
    5. SHA-1 should be considered owned
    6. BCrypt is an industry standard and should be used for form-based authentication
20. Asynchronous messaging
    1. Can reduce strain on your system
    2. RabbitMQ is efficient system for sending and receiving async messages
    3. Producing messages
        1. Spring provides Rabbit template
        2. Default config in spring boot
        3. Provide the exchange and queue name
        4. Post the message as an object or string
    4. Consuming messages
        1. Spring provides “listener” implementations
        2. Responds to messages on the queue and executes some logic
        3. Based on the same paradigm as the producer
    5. Property based configuration
21. Actuator
    1. Provides insights into your running applications
    2. Provides configuration settings, usually through JMX
    3. Allows you to monitor your running application
    4. Out of the box web functionality
        1. Health endpoint
            1. Provides status of applications
            2. Provides status of dependencies
        2. Info endpoint
            1. Provides customisable point for information
    5. JMX functionality
        1. Beans - listing of all beans in application context
        2. Env - listing of the state of the environment
        3. Headdump/threaddump - memory dumps
        4. Mappings - listing of web url mappings
        5. Metrics - Micrometer metrics
    6. To define exposures
        1. Management.endpoint.jmx.exposure.exclude/include
        2. Management.endpoint.web.exposure.exclude/include
    7. Spring security should be enabled for endpoints specially admin endpoints
