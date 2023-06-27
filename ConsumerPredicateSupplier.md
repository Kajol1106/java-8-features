# Consumer, Predicate and Supplier : 

## Consumer :

- in-built functional interface
- can be used in all contextes where an object needs to be consumed i.e. taken as input and some operation is to be performed on the object without returning any result
- it contain one abstract method and one default method
- void accept(T t);
- Example :
```
public class ConsumerDemo {	
	public static void main(String[] args) {
		/*
		Consumer<Integer> consumer = (t)-> System.out.println("Printing consumer : "+t);
		consumer.accept(45);
		*/
		
		//for each accept the consumer object
		List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
		list.stream().forEach((t)-> System.out.println("Printing consumer : "+t));
	}
}
```


## Predicate :

- used for conditional check
- where you think, we can use these true/false returning functions in day to day programming we should choose Predicate
- It contain only one abstract method that's why no need to implement we can use lambda expression
- boolean test(T t);
- Example :
```
public class PredicateDemo{
	/*
	@Override
	public boolean test(Integer t) {
		if(t%2==0) {
			return true;
		}
		else {
			return false;
		}
	}
	*/
	
	public static void main(String[] args) {
		/*
		Predicate<Integer> pre =(t) -> {
			if(t%2==0) {
				return true;
			}
			else {
				return false;
			}
		};
		*/
		/*
		Predicate<Integer> pre =t -> t%2==0;
		System.out.println(pre.test(4));
		*/
		
		//filter method will accept the predicate
		List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6);
		list.stream().filter(t -> t%2==0).forEach(t-> System.out.println("Even "+t));
	}
}
```

## Supplier :

- can be used in all contexts where there is no input but a output is expected
- T get();

