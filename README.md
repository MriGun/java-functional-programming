# java-functional-programming

## Stream Api
#### Stream api is used to process collection of objects.
_A stream is a sequence of objects that supports various method which can be pipelined to produce desired reult_.
- A stream is not a data structure instead it takes input from the Collections, Arrays or I/O channels.
- Streams dont change original data structure. They only provide result as per the provided method.

## Why need stream api
- For functional programming
- Code reduce
- Bulk operation

### forEach()
```java

List<String> list = new ArrayList<>();
		list.add("Sherlock");
		list.add("jhon");
		list.add("Andy");
		list.add("Maddy");
		
		//older system
		
		for(String s : list) {
			System.out.println("Older system : " + s);
		}
		
		//lambda
		list.stream().forEach(s -> System.out.println("Lambda way : " + s));
		
		
		Map<Integer, String> map = new HashMap<>();
		map.put(1, "hello");
		map.put(2, "darkness");
		map.put(3, "my");
		map.put(4, "world");
		map.put(4, "friend");
		
		//java 7 way
		for (Map.Entry<Integer, String> entry : map.entrySet()) {
			 System.out.println("java 7 way " + entry.getKey() + " : " + entry.getValue());
		}
		
		//java 10 way
		for(var entry : map.entrySet()) {
			 System.out.println("java 10 way " + entry.getKey() + " : " + entry.getValue());
		}
		
		//Direct iteration
		map.forEach((key, value) -> System.out.println(key +" : " + value));
		
		//to use the pipeline method presents in the stream
		map.entrySet().stream().forEach(obj -> System.out.println(obj));

```

### filter()
- this method is used for conditional check
- If we have to filter some data based on condition, we can go for filter method.

```java

list.stream()
		.filter(s -> s.startsWith("j"))
		.forEach((s -> System.out.println(s)));
		
		
		map.entrySet().stream()
		.filter(k -> k.getKey() % 2 == 0).forEach(obj -> System.out.println(obj));

```

### We can also collect it to a list or other collection
```java

List<Employee> empList = Database.getEmployees().stream()
				.filter(emp -> emp.getSalary() > 500000)
				.collect(Collectors.toList());
		
		
		System.out.println(empList);

```





#### Differences between Java 8 Map() Vs flatMap() :

|Map|FlatMap|
|---|---|
|It processes stream of values.|It processes stream of stream of values.|
|It does only mapping.|	It performs mapping as well as flattening.|
|It’s mapper function produces single value for each input value.|It’s mapper function produces multiple values for each input value.||
|It is a One-To-One mapping.|It is a One-To-Many mapping.|
|Data Transformation : From Stream to Stream|ata Transformation : From Stream<Stream> to Stream|
|Use this method when the mapper function is producing a single value for each input value.|Use this method when the mapper function is producing multiple values for each input value.|
