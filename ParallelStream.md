### Parallel Stream : 
  - it meant for utilizing multiple cores of the processor
  - normally any java code has one stream of processing, where it is executed sequentially. whereas by using paralled streams, we can divide the code into multiple streams that are executed in paralled on seprate cores and the final result is the combination of the individucal outcomes.
  - the order of execution, however is not under or control.
    - Example :
```
public class ParallelStreamDemo {
	public static void main(String[] args) {
		long startTime = 0;
		long endTime = 0;
		/*
		startTime = System.currentTimeMillis();
		IntStream.range(1, 1000).forEach(System.out::println);
		endTime = System.currentTimeMillis();
		System.out.println("Plain stream took time "+(endTime-startTime));	//Plain stream took time 101
		
		startTime = System.currentTimeMillis();
		IntStream.range(1, 1000).parallel().forEach(System.out::println);
		endTime = System.currentTimeMillis();
		System.out.println("Parallel stream took time "+(endTime-startTime));	//Parallel stream took time 32
		*/
		
		/*
		IntStream.range(1, 10).forEach(x-> System.out.println("Thread : "+Thread.currentThread().getName()+" "+x));
		//it will use only main thread and in sequential order
		
		IntStream.range(1, 10).parallel().forEach(x-> System.out.println("Thread : "+Thread.currentThread().getName()+" "+x));
		//here we will not get data in sequence order and it will run through the different threads, like "Thread : ForkJoinPool.commonPool-worker-3"
		*/
		
		List<Employee> list = EmployeeDao.getEmployees();
		startTime = System.currentTimeMillis();
		double salaryWithPlain = list.stream().map(Employee::getSalary).mapToDouble(i->i).average().getAsDouble();
		endTime = System.currentTimeMillis();
		System.out.println("Plain stream took time : "+(endTime-startTime)+" Average salary : "+salaryWithPlain);
		//Plain stream took time : 36 Average salary : 4971.664
		
		startTime = System.currentTimeMillis();
		double salaryWithParallel = list.stream().map(Employee::getSalary).mapToDouble(i->i).average().getAsDouble();
		endTime = System.currentTimeMillis();
		System.out.println("Parallel stream took time : "+(endTime-startTime)+" Average salray : "+salaryWithParallel);
		//Parallel stream took time : 1 Average salray : 4971.664
	}
}
```
