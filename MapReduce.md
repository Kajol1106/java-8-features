### map(), reduce()
  - Map_Reduce is a functional programming model it serves our 2 purpose
  - Map -> Transforming data
  - Reduce -> Aggregating data (combine elements of a stream and produces a single value)
  - ex., Stream : [2, 1, 3, 4, 5, 6] sum of numbers present in stream?

1. map() :
  - Transform Stream<Object> to Stream of int


2. reduce() :
   - combine stream of int and produce the sum result
   - T reduce(T identity, BinaryOperator<T> accumulator);
   - identity is a initial value of type T
   - accumulator is a function for combining two values
   - Integer sumResult = Stream.of(2, 3, 4, 5, 6).reduce(0, (a, b)-> a+b);
   - Identity : 0 which is nothing initial value
   - Accumulator : (a, b)-> a+b function
