# Streams

* functional - does not change its source and does does not store items, streams conveys elements from source trough a pipeline of computational operations.
* unbounded - while it stream can be short-circuited to be finite, it also can be unbounded

**ways to obtain streams:**
* Collection  - via methods `stream()`, or `parallelStream()`
* Array - via  `Arrays.stream(Object[])`
* Stream - static classes  `Stream.of(Object[])`, `IntStream.range(int, int)` or `Stream.iterate(Object, UnaryOperator)`
* file lines - `BufferedReader.lines()`
* file paths -  Files
* random numbers - `Random.ints()`
* others

**Streams operations are divided into:**
intermediate
* `Stream.filter`, or `Stream.map`
* lazy - return another instance of stream
terminal
* `Stream.forEach`, or `intStream.sum`
* eager - traverse the stream and produce a result or side effect

**Intermediate operations can be:**
* stateless - filter and map, retain no state from previously seen element when processing a new element -- each element can be processed independently of operations on other elements.
    * could be processed on a single pass trough the data
* stateful - may incorporate state from previously seen elements when processing new elements.
    * all elements must be processed before producing result
    * might require multiple passing trough the dataset

they are combined together to create a pipeline. Each pipeline can be used only once.

## Parallelism
Streams facilitate parallel execution by reframing the computation as a pipeline of aggregate operations, rather than as imperative operations on each individual element.

By default each created stream is serial. Parallel stream needs to be explicitly specified.

**ways to obtain parallel stream:**
* Collection - `Collection.parallelStream()`
* IntStream.range(int, int) returns `BaseStream` which can be parallelised with BaseStream.parallel()

```
int sumOfWeights = widgets.parallelStream()
                          .filter(b -> b.getColor() == RED)
                           .mapToInt(b -> b.getWeight())
                           .sum();
```

`isParallel()` - is used to distinguish parallel from serial stream

Invoking terminal operation executes stream in serially or in parallel depending on operations that are invoked. If result of operation such as `findAny()` would be 

# Reference
- https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html
