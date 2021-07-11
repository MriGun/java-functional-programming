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

//psudo code for employee
public static List<Employee> getEmployees() {
		List<Employee> list = new ArrayList<>();
		list.add(new Employee(176, "Roshan", "IT", 600000));
		list.add(new Employee(388, "Bikash", "CIVIL", 900000));
		list.add(new Employee(470, "Bimal", "DEFENCE", 500000));
		list.add(new Employee(624, "Sourav", "CORE", 400000));
		list.add(new Employee(176, "Prakash", "SOCIAL", 1200000));
		return list;
	}

List<Employee> empList = Database.getEmployees().stream()
				.filter(emp -> emp.getSalary() > 500000)
				.collect(Collectors.toList());
		
		
		System.out.println(empList);

```

### Sorting a list
```java

List<Integer> intList = new ArrayList<>();
		intList.add(8);
		intList.add(3);
		intList.add(12);
		intList.add(4);
		
		Collections.sort(intList);  //assending
		Collections.reverse(intList);
		
		System.out.println(intList);
		
		intList.stream().sorted(Comparator.reverseOrder()).forEach(t->System.out.println(t)); //descending

```

### Sorting for little bit complex object
```java

List<Employee> employee = Database.getEmployees();
		
		Collections.sort(employee, new MyComparator());
		
		System.out.println(employee);
		
class MyComparator implements Comparator<Employee>{

	@Override
	public int compare(Employee o1, Employee o2) {

		return (int) (o1.getSalary()-o2.getSalary());  //assending
	}
	
}		

```

### Doing the same thing using inline annonymous function

```java

Collections.sort(employee, new Comparator<Employee>() {

			@Override
			public int compare(Employee o1, Employee o2) {
				// TODO Auto-generated method stub
				return 0;
			}});
		
		System.out.println(employee);

```

### Using lambda
```java

Collections.sort(employee, (o1, o2) -> (int) (o1.getSalary()-o2.getSalary()));
		
		System.out.println(employee);

```

### Using stream
```java

employee.stream().sorted((o1, o2) -> (int) (o1.getSalary()-o2.getSalary())).forEach(System.out::println);

```

### Using method references
```java

employee.stream().sorted(Comparator.comparing(Employee::getName)).forEach(System.out::println);


```

### Sorting a map
```java

Map<String, Integer> map = new HashMap<>();
		map.put("eight", 8);
		map.put("four", 4);
		map.put("ten", 10);
		map.put("two", 2);
		
		//Getting the list from a map
		//Get the entry set from then add it to list
		
		List<Entry<String, Integer>> entries = new ArrayList<>(map.entrySet());	
		
		Collections.sort(entries, (o1, o2) -> o1.getValue().compareTo(o2.getValue()));
		
		System.out.println(entries);

```

### Same thing using stream
```java

map.entrySet().stream().sorted(Map.Entry.comparingByKey()).forEach(System.out::println);
		
map.entrySet().stream().sorted(Map.Entry.comparingByValue()).forEach(System.out::println);

```

### Sorting map with object
```java
Map<Employee, Integer> employeeMap = new TreeMap<>((o1, o2) -> (int) (o2.getSalary()-o1.getSalary()));
		
employeeMap.put(new Employee(176, "Roshan", "IT", 600000), 60);
employeeMap.put(new Employee(388, "Bikash", "CIVIL", 900000), 90);
employeeMap.put(new Employee(470, "Bimal", "DEFENCE", 500000), 50);
employeeMap.put(new Employee(624, "Sourav", "CORE", 400000), 40);
employeeMap.put(new Employee(284, "Prakash", "SOCIAL", 1200000), 120);

System.out.println("Hello");
System.out.println(employeeMap);

System.out.println("Hello12");
employeeMap.entrySet().stream().sorted(Map.Entry.comparingByKey(Comparator.comparing(Employee::getSalary).reversed())).forEach(System.out::println);

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
