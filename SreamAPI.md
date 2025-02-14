# Stream API
A sequence of objects from a source refers to an ordered collection of elements that can be accessed one at a time. This sequence can come from various sources such as collections, files, databases, or I/O streams. It allows processing elements sequentially without needing to load everything into memory at once.

Eg:

```
Predicate<Integer> validEven = num -> num%2 ==0;
		
		List<Integer> numList = Arrays.asList(1,2,3,4,5,6,7,8,9,10,11,12);
		
		List<Integer> evenList = numList.stream().filter(validEven).collect(Collectors.toList());
		evenList.stream().forEach(System.out::println);
		System.out.println("\n Even Sum = "+ evenList.stream().mapToInt(num->num).sum());
		
		List<Integer> oddList = numList.stream().filter(num-> !validEven.test(num)).collect(Collectors.toList());
		oddList.stream().forEach(num->System.out.print(num + " ,"));
		System.out.println("\n Even Sum = "+ oddList.stream().mapToInt(num->num).sum());
		
		System.out.println("Even Count = "+ evenList.stream().count());
		System.out.println("Odd Count = "+ oddList.stream().count());
```

## Distinct 

```
	List<String> names = Arrays.asList("Hareesh","","Rohan","","","Mathew","", "George","Venkat","","Balu","");
		
		names.stream().filter(x-> !x.isEmpty()).collect(Collectors.toList()).forEach(System.out::println);
		
		List<Integer> nums = Arrays.asList(1,22,3,4,55,6,7,1,2,44,2,0,1,4,65);
		List<Integer> uniqueList = nums.stream().distinct().collect(Collectors.toList());
		System.out.println(uniqueList);

```

## map 

```
List<Integer> squareofNums = uniqueList.stream().map(num->num*num).collect(Collectors.toList());

		System.out.println(squareofNums);
```

## sum and averages

```

int totalAge = people.stream().collect(Collectors.summingInt(Person::getAge));
		System.out.println("Total age ="+totalAge);
		
		Double avgAge = people.stream().collect(Collectors.averagingInt(Person::getAge));
		System.out.println("Total age ="+avgAge);

```

## groupingby

```

Map<String, List<Employee>> map = empList.stream().collect(Collectors.groupingBy(Employee::getDept));
		
		map.forEach((ele,emps)->{
			
			System.out.println("\t\t\n==============================");
			System.out.println("|       "+ele+"                     |");
			System.out.println("\t\t\n==============================");
			emps.forEach(emp->{
				System.out.println(emp.getName());
				
			});
		});
		
		Map<String, Double> salaryByDept = empList.parallelStream().collect(Collectors.groupingBy(Employee::getDept,Collectors.summingDouble(Employee::getSalary)));
		
		salaryByDept.forEach((ele,salary)->{
			
			System.out.println("\t\t\n==============================");
			System.out.println("|       "+ele+"                     |");
			System.out.println("\t\t\n==============================");
			System.out.println(salary);
		});


```

## Partitioning - true / false


```
Map<Boolean, List<Student>> PassFailing = students.stream()
				.collect(Collectors.partitioningBy(s->s.getTotalMarks()>60));
		
		PassFailing.get(true).forEach(student -> System.out.println(student));
		System.out.println("=========================================");
		PassFailing.get(false).forEach(student -> System.out.println(student));
		
		
		List<Integer> numList = Arrays.asList(1,2,3,4,5,6,7,8,9,10,11,12);
		
		Map<Boolean, List<Integer>> OddEven = numList.stream()
				.collect(Collectors.partitioningBy(num-> num%2!=0));
		
		System.out.println("Odd");
		OddEven.get(true).forEach(System.out::println);

		System.out.println("Even");
		OddEven.get(false).forEach(System.out::println);

```

## min and max

```


		List<Integer> numList = Arrays.asList(1,2,3,4,5,6,7,8,9,10,11,12);
		
		int max = numList.stream()
				.max(Comparator.comparingInt(num->num)).get();
		
		int min = numList.stream()
				.min(Comparator.comparingInt(num->num)).get();

```

### with comparing 


```
// returns the  object object with totalMarks
		Student maxMarkKeyObjet = students.stream()
				.max(Comparator.comparing(Student::getTotalMarks)).get();

```

```
// returns the  object object with totalMarks
		Optional<Student> maxMarkKeyObjet = students.stream()
				.max(Comparator.comparing(Student::getTotalMarks));
		
		System.out.println(maxMarkKeyObjet);
		
		float maxMark = students.stream()
				.max(Comparator.comparing(Student::getTotalMarks))
						.get().getTotalMarks();
		
		System.out.println(maxMark);

```

## converting into stream and doing the ops

```
	
	int maxLength = Stream.of("apple","orange",			"jack Fruit").max(Comparator.comparing(String::length)).get().length();
		System.out.println("val "+maxLength);

```