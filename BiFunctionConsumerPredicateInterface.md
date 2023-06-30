### BiFunction, BiConsumer, BiPredicate Interface :

1. Function vs BiFunction
- Function :
```
@FunctionalInterface
public interface Function<T, R> {
  R apply(T t);
}
```

  - BiFunction :
```
@FunctionalInterface
public interface BiFunction<T, U, R> {
  R apply(T t, U u);
}
// T - 1st argument
//U - 2nd argument
// R - 3rd argument

//Example :
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.function.BiFunction;
import java.util.function.Function;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class BiFunctionDemo implements BiFunction<List<Integer>, List<Integer>, List<Integer>>{
	
	@Override
	public List<Integer> apply(List<Integer> list1, List<Integer> list2) {
		return Stream.of(list1, list2)
				.flatMap(List::stream)
				.distinct()
				.collect(Collectors.toList());
	}

	public static void main(String[] args) {
		BiFunctionDemo biFunction = new BiFunctionDemo();
		List<Integer> list1 = Arrays.asList(9, 2, 3, 4);
		List<Integer> list2 = Arrays.asList(4, 5, 6, 7);
		System.out.println("Traditional approach : "+ biFunction.apply(list1, list2));
		//Traditional approach : [1, 2, 3, 4, 5, 6, 7]
		
		
		//Using annonymous appraocah means without implementing directly use
		BiFunction<List<Integer>, List<Integer>, List<Integer>> biFunction1 = new BiFunction<List<Integer>, List<Integer>, List<Integer>>() {

			@Override
			public List<Integer> apply(List<Integer> list1, List<Integer> list2) {
				return Stream.of(list1, list2)
						.flatMap(List::stream)
						.distinct()
						.collect(Collectors.toList());
			}		
		};
		System.out.println("Using annonymous function : "+biFunction1.apply(list1, list2));
		
		/*
		//using lambda 
		BiFunction<List<Integer>, List<Integer>, List<Integer>> biFunction2 = (l1, l2)-> {
				 return Stream.of(l1, l2)
						.flatMap(List::stream)
						.distinct()
						.collect(Collectors.toList());		
		};
		System.out.println("Using lambda : "+biFunction2.apply(list1, list2));	
		*/
		
		//using above we will not get list in sorted order. after performing biFunction we can sort through the Function and apply using andThen()
		BiFunction<List<Integer>, List<Integer>, List<Integer>> biFunction2 = (l1, l2) -> {
			return Stream.of(l1, l2)
					.flatMap(List::stream)
					.distinct()
					.collect(Collectors.toList());
		};
		
		Function<List<Integer>, List<Integer>> sortedFunction = (lists)-> lists
				.stream()
				.sorted()
				.collect(Collectors.toList());
		System.out.println("Using lambda : " + biFunction2.andThen(sortedFunction).apply(list1, list2));
		
		
		//perform some operation on map
		Map<String, Integer> map = new HashMap<>();
		map.put("Kaju", 90000);
		map.put("Raju", 40000);
		map.put("Faiju", 10000);
		map.put("Shailu", 80000);
		map.put("Kaje;", 30000);
		
		BiFunction<String, Integer, Integer> biFunctionMap = new BiFunction<String, Integer, Integer>() {
			@Override
			public Integer apply(String key, Integer value) {
				return value+1000;
			}		
		};
		map.replaceAll(biFunctionMap);	//replaceAll method accept the BiFunction object
		System.out.println("Perform operations on Map using annonymous function approach : "+map);
		
				
		BiFunction<String, Integer, Integer> biFunctionMap1 = (key, value) -> value+2000;
		map.replaceAll(biFunctionMap1);	//replaceAll method accept the BiFunction object
		System.out.println("Perform operations on Map using lambda approach : "+map);
	}	
}

```

2. Consumer vs BiConsumer
- Consumer :
```
@FunctionalInterface
public interface Consumer<T> {
  void accept(T t);
}
```

  - BiConsumer :
```
@FunctionalInterface
public interface BiConsumer<T, U> {
  void accept(T t, U u);
}

//Example :
import java.util.HashMap;
import java.util.Map;
import java.util.function.BiConsumer;

public class BiConsumerDemo implements BiConsumer<String, Integer>{

	@Override
	public void accept(String i1, Integer i2) {
		System.out.println("Input 1 : "+i1+" Input 2 : "+i2);
	}
	
	
	public static void main(String[] args) {
		//traditional approach using implements
		BiConsumerDemo biConsumer = new BiConsumerDemo();
		biConsumer.accept("Kajol", 1234567);
		
		
		//using annonymous function
		BiConsumer<String, Integer> biConsumer2 = new BiConsumer<String, Integer>() {
			@Override
			public void accept(String t, Integer u) {
				System.out.println(t+ " "+u);
			}		
		};		
		biConsumer2.accept("Welcome", 123);
		
		
		//using lambda expression
		BiConsumer<String, Integer> biConsumer3 = (t, u) -> System.out.println(t+ " "+u);		
		biConsumer3.accept("Welcome Kajol", 123);
		
		// perform some operation on map
		Map<String, Integer> map = new HashMap<>();
		map.put("Kaju", 90000);
		map.put("Raju", 40000);
		map.put("Faiju", 10000);
		map.put("Shailu", 80000);
		map.put("Kaje;", 30000);
		map.forEach(biConsumer2); //we have to pass biconsumer object in foreach
	}

}

```


3. Predicate vs BiPredicate
- Predicate :
```
@FunctionalInterface
public interface Predicate<T> {
  boolean test(T t);
}
```

  - BiPredicate :
```
@FunctionalInterface
public interface BiPredicate<T, U> {
  boolean test(T t, U u);
}

//Example :
import java.util.function.BiPredicate;

public class BiPredicateDemo implements BiPredicate<String, String>{

	@Override
	public boolean test(String s1, String s2) {
		return s1.equals(s2);
	}
	
	public static void main(String[] args) {
		//using traditional approach
		BiPredicateDemo biPredicate1 = new BiPredicateDemo();
		System.out.println(biPredicate1.test("kaju", "kaju"));	//true
		
		//by using annonymous function
		BiPredicate<String, String> biPredicate2 = new BiPredicate<String, String>() {
			@Override
			public boolean test(String s1, String s2) {
				return s1.equals(s2);
			}			
		};
		System.out.println(biPredicate2.test("Ram", "ram"));	//false
		
		//using lambda expression
		BiPredicate<String, String> biPredicate3 = (s1, s2) -> s1.equals(s2);			
		System.out.println(biPredicate3.test("Ram", "ram"));	//false
		
		
		//there is some another methods also present 
		BiPredicate<String, String> equalsPredicate = (s1, s2) -> s1.equals(s2);
		BiPredicate<String, String> lengthPredicate = (s1, s2) -> s1.length()==s2.length();
		
		//and() will check both condition are true or not
		boolean andOp = equalsPredicate.and(lengthPredicate).test("kk", "kk");
		System.out.println(andOp);	//true
		andOp = equalsPredicate.and(lengthPredicate).test("kk", "kajol");
		System.out.println(andOp);	//false
		
		boolean orOp = equalsPredicate.and(lengthPredicate).test("kk", "kk");
		System.out.println(orOp);	//true
		orOp = equalsPredicate.and(lengthPredicate).test("kk", "kajol");
		System.out.println(orOp);	//false		
	}
}

```
