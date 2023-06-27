# java-8-features
### Lambda Expression : 
- with lambda expression we don't have to need method name and return type
- also you don't need to implement interface if there is only one method
- if there is only one statement then no need to bracket also
1. Example for single statement :
```
public interface Calculator {
	void switchOn();
}

public class LambdaMain{
	public static void main(String[] args) {
		Calculator c = () -> System.out.println("switch on method...");
		c.switchOn();
	}
}

```

2. Example for taking one argument :
```
public interface Calculator {
	void sum(int a);
}

public class LambdaMain{
	public static void main(String[] args) {
		Calculator c = (a) -> System.out.println("Sum = "+a);
		c.sum(5);
	}
}
```

3. Example for taking multiple arguments :
```
public interface Calculator {
	void multiply(int a, int b);
}

public class LambdaMain{
	public static void main(String[] args) {
		Calculator c = (a, b) -> {
			int res = a*b;
			System.out.println("Result is : "+res);
		};
		c.multiply(5, 4);
	}
}
```

4. Example for return statement :
```
public interface Calculator {
	intsubstraction(int a, int b);
}

public class LambdaMain{
	public static void main(String[] args) {
		Calculator c = (a, b) -> a-b;
		System.out.println(c.substraction(10, 5));
	}
}
```
