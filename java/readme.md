1. Java annotations
    1. Java annotation is metadata about the program embedded in the program itself.
    2. We can specify annotation availability to either compile time or runtime
    3. Creating custom annotation is similar to writing an interface, except that the interface keyword is prefixed with @ symbol. We can declare methods in annotations
        1. Annotation methods can’t have parameters
        2. Annotation method return types are limited to primitives eg String, Enum
        3. Java annotation methods can have default values
        4. Annotations can have meta annotation attached to them. Eg: @Documented, @Target, @Inherited, @Retention, @Repeatable


2. Java generic class
    1. If we don’t use generics we can end up in ClassCastException at runtime
    2. We can define our own classes with generic type. A generic type is a class or an interface that is parameterised over types. We use angle brackets (<>) to specify the type parameter
    3. Most commonly used type parameter names are:
        1. E —> Element
        2. K —> Key (used in Map)
        3. N —> Number
        4. T —> Type
        5. V —> Value (used in map)
    4. We can specify type while calling these methods or we can invoke them like a normal method. This facility is called type inference
    5. To declare a bounded type parameter, list the type parameter’s name, followed by extends keyword, followed by its upper bound
    6. Java generics supports multiple bounds also, I.e <T extends A & B & C> in this A can be class or interface. If A is a class then B & C should be interface. We can’t have more than one class in multiple bounds
    7. To declare a lower bounded we have to use super keyword eg: List< ? Extends Integer> not list can have Integer, Number and Object


3. Autoboxing in Java
    1. Converting a primitive data type into an object of corresponsding wrapper class is called auto boxing
    2. Java compiler applies auto boxing when a primitive value is
        1. Passed as a parameter to a method that expects an object of the corresponding wrapper class.
        2. Assigned to a variable of corresponding wrapper class


4. Unboxing in java
    1. Converting an object of wrapper type to its corresponding primitive data type is called unboxing
    2. Java compiler applies unboxing when an object of a wrapper class is
        1. Passed as a parameter to a method that expects a value of the corresponding primitive type
        2. Assigned to a variable of corresponding primitive type


5. Threads in java
    1. A Process  is a self contained environment and it can be seen as a program or application. A program contains multiple processes inside it. JRE runs a single process which contains different classes and programs as processes
    2. Thread can be called a light weight process. Thread requires less resources to create and exists in the process. Thread share process resources
    3. Every java application has atleast one thread. 
    4. Multithreading refers to two or more threads executing concurrently in a single program. A single core processor can execute only one thread at a time and time slicing is the OS feature to share processor time between different processes and threads
    5. Java provides two ways to read a thread
        1. Implementing java.lang.Runnable interface
        2. Extending java.lang.Thread class
    6. To make a class runnable, we can implement java.lang.Runnable interface and provide implementation of run() method. To use this class as a Thread, We need to create a Thread object by passing object of this runnable class and then call start() method to execute the run() method in a separate thread
    7. Once we start any thread, its execution depends on the OS implementation of time slicing and we cannot control their execution. However we can set threads priority but even then it doesn’t guarantee 
    8. If your class your class provides more functionality rather than just running as Thread, you should implement runnable interface. 
    9. If your class only goal is to run as Thread, you can extend Thread class


6. Thread safety in java
    1. Multi threading can cause data inconsistency because updating any field value is not an atomic process
    2. Synchronisation is the easiest and widely used tool for thread safety
    3. Use of atomic wrapper classes from java.util.concurrent.atomic package eg: AtomicInteger
    4. Use of locks from java.util.concurrent.lock package
    5. Use of thread safe collection classes
    6. Using volatile keyword with variables to make every thread read the data from memory, not from thread cache


7. Synchronisation in java
    1. JVM guarantees that a synchronised code will be executed by only one thread at a time. Synchronized keyword is used, internally it uses locks on Object or class to make sure only one thread is executing the code
    2. Java synchronisation works on locking and unlocking of resources before any thread enters into synchronised code. In the meantime other threads are in wait state
    3. We can use synchronised keyword in two ways. 
        1. Synchronise the entire method
        2. Create synchronised block
    4. If method is synchronised it locks the object, if method is static it locks the class
    5. It is always good to use synchronised block to lock only sections of method that needs synchronization
    6. While creating a synchronised block we need to provide the resource on which lock will be acquired it can be class or Object field of class
    7. synchronized(this) will lock the object before entering the block
    8. You should use lowest level of locking. When we lock an object, it acquires a lock on all files of the object
    9. Synchronisation provides data integrity on cost of performance
    10. It works only in same JVM.
    11. It can lead to deadlocks
    12. Cannot be used for constructors and variables
    13. We should not use any object that is maintained in constant poll. Eg: string uses string pool
    14. Strings are safe for multi threading it doesn’t require synchronisation


8. ThreadLocal in java
    1. Used to create thread local variables. All threads of an object shares its variables. So variables is not thread safe
    2. Every thread has its own ThreadLocal variable and they can use its get() and set() method to get the default value or change its value local to thread
    3. ThreadLocal in java8 has withInital() method that takes supplier as an argument.


9. Thread Pool in java
    1. It managers the pool of worker threads
    2. It contains a queue that keeps tasks waiting to get executed
    3. Java thread pool manages the collection of runnable threads
    4. Executors provide factory and support methods for Executor interface to create the thread pool in java
    5. Executors is a utility class that also provides useful to work with ExecutorService, ScheduledExecutorService, ThreadFactory and Callable classes through various factory methods
    6. ExecutorService will run your threads, we can create a fixed-size thread pool. If inputs threads are less then size then extra threads will wait till there is a space for you to run
    7. ExecutorService is the interface which allows us to execute tasks on threads asynchronously . The executor is responsible of maintaining a poll of threads and assigns them tasks. It also provides the facility to queue up tasks until there is a free thread available if the number of tasks is more than the threads available.
    8. Executor Service methods
        1. execute() method takes in a runnable object and performs its task asynchronously. After making the call to execute method, we call the shutdown method which blocks any other task to queue up in executorService
        2. submit() method takes in a runnable task and returns a Future object. This object can be used to check the status of Runnable whether it has completed execution or not
        3. invokeAny() method takes a collection of Callable objects or objects of classes implementing Callable. This method returns the future object of the callable object which gets successfully executed first
        4. invokeAll() method takes in a Collection of callable objects having tasks and return a list of future objects containing the result of all the tasks
    9. To Shut down ExecutorService
        1. Once we are done with out tasks given to ExecutorService, then we have to shutdown because ExecutorService performs the task on different threads. If we don’t shut down the Executor Service the threads will keep running and JVM won’t shutdown
        2. shutdown() method
        3. shutdownNow() method
        4. awaitTermination() method


10. Java Callable and Future
    1. Java callable is similar to runnable interface but it can return any Object and able to throw Exception
    2. Since callable tasks run in parallel, we have to wait for the returned object
    3. The Callable tasks return Future Object, We can find out the status of the Callable task and get the returned object.
    4. It provides get() method which will wait for the Callable to finish and then return the result
    5. Cancel method to cancel the associated Callable task
    6. There are isDone and isCancelled methods to find out current status of associated Callable task


11. Java Heap space
        1. Java heap space is used by java runtime to allocate memory to Objects and JRE classes. Whenever we create an object it is always created in heap space
        2. Garbage Collection runs on heap memory to free the memory used by objects that don’t  have any reference. Any object created in heap space has global access and can be reference from anywhere of the application


12. Java Stack Memory
    1. Java stack memory is used for the execution of thread. 
    2. They contain method-specify values that are short lived and references to other objects in the heap that is getting referred from the method
    3. It is always referred in LIFO (Last In First Out) order. Whenever a method is invoked, a new block is created in stack memory for the method to hold local primitive values and reference to other objects in the method
    4. As soon as the method ends, the block becomes unused and becomes available for the next method. 
    5. Stack memory size is very less compared to Heap memory
    6. Heap memory is used by all parts of the application whereas stack memory is used by one thread of execution
    7. Whenever an object is created it is stored in heap memory and stack memory holds a reference to it
    8. Stack memory only contains local primitive variables and reference variables to objects in heap space
    9. Objects stored in the heap are globally accessible whereas stack memory can’t be accessed by other threads
    10. Memory management in stack is done in LIFO manner and is complex in heap memory because its used globally
    11. Stack memory is short lived whereas heap memory livers from the start till the end of the application
    12. We use -Xms to define startup size and -Xmx for max size of heap memory and -Xss for stack memory size
    13. When stack memory is full it throws stack overflow error and when heap memory is full it throws OutOfMemory Exception
    14. Stack memory size is very less and is fast


13. JVM memory model
    1. Memory is physically divided into two parts
        1. Young generation
        2. Old generation
    2. The Young generation is the place where all the new objects are created. When. The young generation is filled, garbage is performed. The garbage collection is called Minor GC. 
    3. Young generation is divided into three parts
        1. Eden memory
        2. Survivor memory
        3. Most of the newly created objects are located int the Eden memory space
        4. When eden space is filled with objects, Minor GC is performed and all the survivor objects are moved to one of the survivor spaces
        5. At a time, one of the survivor space is always empty
        6. Objects that are survived after many cycles of GC, are moved to the old generation memory space. Usually 
    4. Memory management in Java - Old generation
        1. Contains object that are long lived and survived after many rounds of minor GC. 
        2. Garbage collection in it is called Major GC  and usually takes a longer time
    5. All garbage collections are “Stop the World” events because all application threads are stopped until the operation completes
    6. Minor GC is very fast and application doesn’t gets affected by this
    7. Major GC should be minimised because it will make your application unresponsive for the garbage collection duration. 
    8. The duration taken by garbage collector depends on the strategy used for garbage collection. 


14. Reflection in java
    1. Java reflection provides ability to inspect and modify the runtime behaviour of application 
    2. It has a few drawbacks
        1. Poor performance: Since it resolves the types dynamically, it involves processing like scanning the class path to find the class to load, causing slow performance
        2. Security Restrictions: reflection requires permissions that might not be available for the system running under security manager. 
        3. Security issues: Using reflection we can access part of code that we are not supposed to. Eg: we can access private fields and modify it
        4. High Maintenance:: Code is had to understand and debug also any issue with the code can’t be found at compile time
    3. JVM instantiates an immutable instance of java.lang.Class

15. Serialization & Deserialization in java
    1. Serialization allows us to convert an Object to stream that we can send over the network or store in a file or DB.
    2. Deserialization is the process of converting Object stream to actual Java object to be used in our program. 
    3. We need to implement serialisable interface
    4. It is a marker interface and has not fields or method to implement
    5. If you want a property to not be serialised use transient keyword
    6. Also static variables are not serialised as they are at class level
    7. Some changes in class that doesn’t affect deserialisation process
        1. Adding new variables to class
        2. Changing the variables from transient to non-transient
        3. Changing variables from static to non-static
    8. If we want to maintain integrity of data we can use Externalizable interface. writeExternal() and readExternal() methods
    9. To have more control we have
        1. readObject(ObjectInputStream): if this method is present ObjectInputStream will use this method
        2. writeObject(ObjectOutputStream): if this method is present ObjectOutputStream will  be used
        3. writereplace() if this method is present then after serialisation process this method is called and object returned is serialised to the stream
        4. readResolve(): if present, after deserialisation process this method is call to return final object to caller program
    10. If the parent class does not implement serialisable then we need to use readObject() and writeObject() methods to capture the state of parent object


16. Java Thread dump 
    1. Useful to analyse bottlenecks and deadlocks
    2. If you are analysing application for slowness you must use a profiler
    3. To avoid deadlocks
        1. Avoid nested locks
        2. Lock only what is required
        3. Avoid waiting indefinitely: use join() method with a certain time period

17. Immutable class
    1. Immutable objects are instances whose state doesn’t change after it has been initialised 
    2. Benefits
        1. Good for caching purposes because you don’t have to worry about the value changes
        2. It is inherently thread safe
    3. To create immutable class
        1. Declare the class a final so it can’t be extended
        2. Make all fields private so that direct access is not allowed
        3. Don’t provide setter methods for variables
        4. Make all mutable fields final so that its value can be assigned only once
        5. Initailise all fields via a constructor performing deep copy
        6. Perform cloning of objects in the getter methods to return a copy rather than the actual object reference