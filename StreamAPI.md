### Stream API :
- used to process collections of objects.
- It is a sequence of objects that supports varioous methods which can be pipelined to produce the desired result
- it is not a data structure instead it takes input from the Collections, Arrays or I/O channels
- it don't cange the original data structure, they only provide the result as per the pipelined methods.

  #### why we need stream ?
  - functional programming
  - code reduce
  - bulk operation

  #### Methods :
  
  1. Filter => for conditional check
  - Example :
```
public class FileterDemo {
	public static void main(String[] args) {
		List<String> list = Arrays.asList("Ram", "Prabhakar", "Kajol", "Kapil");
		/*
		 //traditional way
		for(String s: list) {
			if(s.startsWith("K")) {
				System.out.println(s);
			}
		}
		*/
		list.stream().filter(s-> s.startsWith("K")).forEach(t-> System.out.println(t));
		
		Map<Integer, String> names = new HashMap<>();
		names.put(1, "Kajol");
		names.put(2, "Ram");
		names.put(3, "Prabhakar");
		names.put(4, "Sagar");
		names.entrySet().stream().filter(k-> k.getKey()%2==0).forEach(obj-> System.out.println(obj));		
	}
}

```


  2. forEach => for iteration
  - Example :
```
public class ForEachDemo {
	public static void main(String[] args) {
		List<String> list = Arrays.asList("Ram", "Prabhakar", "Kajol");
		/*
		//traditional way
		for(String s: list) {
			System.out.println(s);
		}
		*/
		
		//using foreach - it will accept the consumer object
		list.stream().forEach((s)-> System.out.println(s));
		
		Map<Integer, String> names = new HashMap<>();
		names.put(1, "Kajol");
		names.put(2, "Ram");
		names.put(3, "Prabhakar");
		names.put(4, "Sagar");
		names.forEach((key, value)-> System.out.println(key+" : "+value));
		names.entrySet().stream().forEach(obj-> System.out.println(obj));
	}
}
```
