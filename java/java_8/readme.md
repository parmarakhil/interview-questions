# Java 8 features


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
    Java Streams
    7. There are many ways to create a stream, once created the instance will not modify its source therefore allowing creation of multiple instances from a single source
        1. Empty stream
            1. Use the empty() method 
                1. Stream<String> emptyStream= Stream.empty();
        2. Stream of collection
            1. Stream<String> streamOfCollection = myCollection.stream();
        3. Stream of array
            1. Stream<String> streamOfArray=Stream.of(“a”,”b”,”c”);
            2. Stream<String> streamOfArrayFull =  Arrays.stream(myArray);
            3. Stream<String> streamOfArrayPart =  Arrays.stream(myArray,1,3);
        4. Stream.builder()
            1. When builder is used the desired type should be additionally specified in the right part of the statement
                1. Stream<String> streamBuilder = Stream.<String>builder().add(“a”).add(“b”).add(“c”).build();
        5. Stream.generate()
            1. The generate() method accepts a supplier<T> for element generation. As the resulting stream is infinite, the developer should specify the desired size
                1.  Stream<String> streamGenerated = Stream.generate(() -> "element").limit(10);
        6. Stream.iterate()
            1. The first element of resulting stream is the first parameter of the iterate() method
                1.  Stream<Integer> streamIterated = Stream.iterate(40, n -> n + 2).limit(20);
        7. Stream of primitives
            1. As Stream<T> is a generic interface and there is no way to use primitives as a type parameter with generics, 3 special interfaces were created. IntStream, LongStream, DoubleStream
            2.  IntStream intStream = IntStream.range(1, 3);
            3.  LongStream longStream = LongStream.rangeClosed(1, 3);
            4. range(int startInclusive, int endExclusive)
            5. rangeClosed(int startInclusive, int endInclusive);
        8. Stream of string
            1.  IntStream streamOfChars = "abc".chars();
            2.   Stream<String> streamOfString = Pattern.compile(", ").splitAsStream("a, b, c");
        9. Stream of file
            1.  Path path = Paths.get("C:\\file.txt");
            2. Stream<String> streamOfStrings = Files.lines(path);
            3. Stream<String> streamWithCharset =   Files.lines(path, Charset.forName("UTF-8"));
    8. Referencing a stream
        1. We can instantiate a stream and have an accessible reference to it, as long as only intermediate operations are called. 
        2. Executing a terminal operation makes a stream inaccessible
        3.  Stream<String> stream =   Stream.of("a", "b", "c").filter(element -> element.contains("b"));
        4. Optional<String> anyElement = stream.findAny();
        5. This will work fine
        6. Optional <String> firstElement = stream.findFirst(); 
        7. This will throw IllegalStateException as once a terminal operation is used. The stream is closed
        8. Java 8 streams can’t be reused
    9. Stream pipeline
        1. To perform a sequence of operations over the elements of data source
        2. We need three parts source, intermediate operations and a terminal operation
        3. A stream by itself is worthless, the user is interested in the result of terminal operation
        4. We can only use one terminal operation per stream
    10. Lazy Invocation
        1. Intermediate operations are lazy
        2. They will be invoked only if it is necessary for the terminal operation execution
        3.  List<String> list = Arrays.asList(“abc1”, “abc2”, “abc3”); counter = 0; Stream<String> stream = list.stream().filter(element -> {    wasCalled();    return element.contains("2");  });
        4. There the filter method won’t be called even once. The reason why is missing of terminal operation
    11. Order of Execution
        1. From performance point of view, the right order is one of the most important aspects of chaining operations in stream pipeline
        2.  long size = list.stream().skip(2).map(element -> {    wasCalled();     return element.substring(0, 3); }).count();
        3. The intermediate operations which reduce the size of the stream should be placed before operations which are applying toe act element
    12. Stream Reduction
        1. Stream has many terminal operations which aggregate a stream to a type or a primitive eg: sum(), count(), min(), sum()
        2. If custom implementation is needed we can use reduce() and collect() methods
        3. The reduce() method
            1. There are 3 variations of this method which differs by their Signatures and returning types
            2.  identity – the initial value for an accumulator, or a default value if a stream is empty and there is nothing to accumulate
            3.  accumulator – a function which specifies the logic of the aggregation of elements. As the accumulator creates a new value for every step of reducing, the quantity of new values equals the stream's size and only the last value is useful. This is not very good for the performance.
            4.  combiner – a function which aggregates the results of the accumulator. We only call combiner in a parallel mode to reduce the results of accumulators from different threads.
            5.  OptionalInt reduced =  IntStream.range(1, 4).reduce((a, b) -> a + b);
            6.  int reducedTwoParams =  IntStream.range(1, 4).reduce(10, (a, b) -> a + b);
            7.  int reducedParallel = Arrays.asList(1, 2, 3).parallelStream().reduce(10, (a, b) -> a + b, (a, b) -> {       log.info("combiner was called");    return a + b; });
            8. To make a combiner work, a stream should be parallel
        4. The collect() method
            1. It accepts an argument of type Collector
            2.   List<Product> productList = Arrays.asList(new Product(23, "potatoes"), new Product(14, "orange"), new Product(13, "lemon"),  new Product(23, "bread"), new Product(13, "sugar"));
            3.  Converting a stream to the Collection (Collection, List or Set): List<String> collectorCollection = productList.stream().map(Product::getName).collect(Collectors.toList());
            4.  Reducing to String: String listToString = productList.stream().map(Product::getName) .collect(Collectors.joining(", ", "[", "]"));
            5. The joiner() method can have from one to three parameters (delimiter, prefix, suffix). The most convenient thing about using joiner() is that the developer doesn't need to check if the stream reaches its end to apply the suffix and not to apply a delimiter. Collector will take care of that.
            6. Processing the average value of all numeric elements of the stream: double averagePrice = productList.stream().collect(Collectors.averagingInt(Product::getPrice));
            7.  Processing the sum of all numeric elements of the stream: int summingPrice = productList.stream().collect(Collectors.summingInt(Product::getPrice));
            8.  The methods averagingXX(), summingXX() and summarizingXX() can work with primitives (int, long, double) and with their wrapper classes (Integer, Long, Double). One more powerful feature of these methods is providing the mapping. As a result, the developer doesn't need to use an additional map() operation before the collect() method.
            9.  Collecting statistical information about stream’s elements: IntSummaryStatistics statistics = productList.stream().collect(Collectors.summarizingInt(Product::getPrice));
            10. By using the resulting instance of type IntSummaryStatistics, the developer can create a statistical report by applying the toString() method. The result will be a String common to this one “IntSummaryStatistics{count=5, sum=86, min=13, average=17,200000, max=23}.”
            11. It is also easy to extract from this object separate values for count, sum, min, and average by applying the methods getCount(), getSum(), getMin(), getAverage(), and getMax(). All of these values can be extracted from a single pipeline.
            12. Grouping of stream’s elements according to the specified function: Map<Integer, List<Product>> collectorMapOfLists = productList.stream().collect(Collectors.groupingBy(Product::getPrice));
            13. In the example above, the stream was reduced to the Map, which groups all products by their price.
            14. Dividing stream’s elements into groups according to some predicate: Map<Boolean, List<Product>> mapPartioned = productList.stream().collect(Collectors.partitioningBy(element -> element.getPrice() > 15));
            15. Pushing the collector to perform additional transformation: Set<Product> unmodifiableSet = productList.stream().collect(Collectors.collectingAndThen(Collectors.toSet(),  Collections::unmodifiableSet);
    13. Parallel Streams
        1. The api allows to create parallel streams
        2. If source is collection or array, parallelStream() method can be sued
        3. If source is something else parallel() method can be used
        4. Under the hood, the api uses ForkJoin framework to execute operations in parallel.
        5. When to use parallel stream
            1. Must be used only with stateless, non-interfering and stateless operations
            2. A stateless operation is an operation in which the state of one element does not affect other element
            3. A non-interfering operationn is an operation in which data source is not affected
            4. An associative operation is an operation in which the result is not affected by order of operands
            5. They should be used when the output of the operation is not needed to be dependent on the order of elements present in source collection
            6. Parallel streams can be used in case of aggregate functions
            7. Parallel streams quickly iterate over the large sized collections
            8. Parallel streams can be used if developers have performance implications with he sequential streams
            9. If the environment is not multi threaded, then parallel stream creates thread and can affect the new requests coming in
        6. Performance implications
            1. Since each sub-stream is a single threaded running and acting on the data, it has overhead compared to sequential stream
            2. Inter thread communication is dangerous and takes time for coordination
        7. Parallel stream internally uses Fork-Join framework
        8. The Fork-Join framework is in charge of splitting the. Source data between worker threads and handling callback on task completion
        9. Arrays or array list are best for parallel streams, followed by Treemap and hashes, the worst is linked list       
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
    7. The hashMap internal working was also improved by using a binary tree inplace of linkedlist when the hashmap reaches certain threshold usually 75%
7. Concurrency API improvements
    1. ConcurrentHashMap compute() forEach(), forEachEntry(), forEachKey(), forEachValue(), merge(), reduce(), search() methods
    2. CompletableFuture that may be explicitly completed
    3. Executors newWorkStealingPool() method to create a work-stealing thread pool available processors as its target parallelism level
    4. It provide atomic classes such as AtomicInteger, Atomic operations are performed in a single unit of task without interference from other operations. Atomic operations are necessity in multi-threaded environment to avoid data inconsistency
    5. Lock interface provides more extensive locking operations that can be obtained using synchronized methods and statements. They allow more flexible structuring, may have quite different properties and may support multiple associated Condition objects. The advantages are
        1. It is possible to make them fair
        2. It is possible to make a thread responsive to thread interruptions while waiting on a Lock object
        3. It is possible to try and acquire a lock but return immediately or after a timeout if the lock can't be acquired
        4. It is possible to acquire and release locks in different scopes and in different orders
    6. java.util.concurrent.BlockingQueue is a Queue that supports operations that wait for the queue to become non-empty when retrieving and removing an element, and wait for space to become available in the queue when adding an element. BlockingQueue doesn’t accept null values and throw NullPointerException if you try to store null value in the queue. BlockingQueue implementations are thread-safe. All queuing methods are atomic in nature and use internal locks or other forms of concurrency control. BlockingQueue interface is part of the Java collections framework and it’s primarily used for implementing the producer-consumer problem.
    7. Callable interface in concurrency package that is similar to Runnable interface but it can return any Object and able to throw Exception. The Callable interface uses Generics to define the return type of Object. Executors class provide useful methods to execute Callable in a thread pool. Since callable tasks run in parallel, we have to wait for the returned Object. Callable tasks return java.util.concurrent.Future object. Using Future we can find out the status of the Callable task and get the returned Object. It provides the get() method that can wait for the Callable to finish and then return the result.
    8. FutureTask is the base implementation class of Future interface and we can use it with Executors for asynchronous processing. Most of the time we don’t need to use FutureTask class but it comes real handy if we want to override some of the methods of Future interface and want to keep most of the base implementation. We can just extend this class and override the methods according to our requirements.
    9. Java Collection classes are fail-fast which means that if the Collection will be changed while some thread is traversing over it using iterator, the iterator.next() will throw ConcurrentModificationException. Concurrent Collection classes support full concurrency of retrievals and adjustable expected concurrency for updates. Major classes are ConcurrentHashMap, CopyOnWriteArrayList and CopyOnWriteArraySet
8. Method reference
    1. Method reference is used to refer method of functional interface. Each time when you are using lambda expression to just refer a method you can use method references
