Java 8 features


1. forEach() method in itterable interface
    1. When we need to traverse through a collection we need to create an iterator. In Java 8 we have a forEach() method which can be used. It takes a Consumer object as an argument. 
2. Default and static methods in Interfaces
    1. We can use default  and static keyword to create interfaces with method implementation
    2.  Now since it is similar to abstract class and we cannot have multiple inheritance, we need to create a class which will implement both interfaces and override the implemented method of both interfaces
    3. For clarity Interfaces are not allowed to have object default methods
3. Functional Interfaces and lambda expressions
    1. Functional Interface is an interface with @FunctionalInterface annotation and only one abstract method. It can have n number of default of static method since they will be implemented
    2. The annotation is a facility to avoid accidental addition of abstract methods in functional interfaces
    3. One of the major benefits of the functional interface is the possibility to use lambda expression to instantiate them. We can do same using anonymous class
    4. Lambda function are also called as arrow functions
    5. Type of functional interfaces
        1. Function and BiFunction: Takes one type of argument and returns another type of argument. It contains apply() method. eg: map, mapToInt, toArray, reduce
        2. Predicate: Takes one type of argument and returns a boolean value. It has test() method. Eg: filter, anyMatch, allMatch, noneMatch
        3. Consumer: It takes one type of argument and returns nothing
        4. Supplier: Represents a functional interface that supplies value of some sort. Eg: collect 
4. Java stream API for Bulk Data operations on collections
    1. Java.util.stream has been added to perform filter/map/reduce like operations
    2. Stream API allows sequential as well as parallel execution
    3. Stream uses internal iteration where java framework is in control of the iteration instead of external iteration where client code is in control of the iteration
    4. Collection is an. In-memory data structure to hold values and before we start using collection, the values should be populated. Whereas a java Stream is a data structure that is computed on demand
    5. Java Stream doesn’t store data it operates on the source data structure and produce pipelined data that can be used to perform specific operation.
    6. Java streams are consumable, so there is no way to create a reference to stream for future use. Since data is on-demand it is not possible to use stream multiple times
5. Java Time API
    1. Java.time package streamlines the process of working with time in java
    2. The Time API prefers menus over integer constants for months and days of the week
6. Collection API improvements
    1. Iterator default method forEachRemaining(Consumer action) to perform the given action for each remaining element until all elements have been processed or the action throws an exception
    2. Collection default method removeIf(Predicate filter) to remove all of the elements that satisfy the given predicate
    3. Collection spliterator() method returning Spliterator instance that can be used to traverse elements sequentially or parallel
    4. Map replaceAll(), compute(), merge() methods
    5. Collections framework is the architecture to represent and manipulate data in java in a standard way
    6. Collection interface is the root of the collection hierarchy. A collection represents a group of objects known as its elements. The java platform doesn’t provide any direct implementations of this interface.
7. Concurrency API improvements
    1. ConcurrentHashMap compute() forEach(), forEachEntry(), forEachKey(), forEachValue(), merge(), reduce(), search() methods
    2. CompletableFuture that may be explicitly completed
    3. Executors newWorkStealingPool() method to create a work-stealing thread pool available processors as its target parallelism level
8. Method reference
    1. Method reference is used to refer method of functional interface. Each time when you are using lambda expression to just refer a method you can use method references
