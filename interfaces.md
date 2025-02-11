
# Interfaces in Java

## Declaration and definition

- Use interface keyword
- From jdk 1.8, If you know the implementation for a common functionality, You can write it as a static method.
- Cannot override the static method
- default methods in interfaces can be overriden by the implemented class
```
    public interface SizeComparable {

}

```

- All methods in interfaces are public and abstract by default
- Abstract classes are used for related classes. But Interfaces are used for unrelated classes
- All the fields or member variables are public ,static and final by default

```
public interface SizeComparable {
	
	public boolean isBig(Object obj);//  Java.lang.Object
	public abstract boolean isSmall(Object obj);
	
}

```

## final Keyword
- Should be initialised
- final w/ variables - the variables cannot be modified
- w/ class -  cannot be inherited
- w/ methods - cannot be overriden
  

## implements Keyword

To  implement the interface to a car or another interface

```
package com.trivium.interfaces;

public class Dog implements SizeComparable {
	
	float weight;
	String breed;
	public Dog(float weight, String breed) {
		super();
		this.weight = weight;
		this.breed = breed;
	}
	@Override
	public String toString() {
		return "Dog [weight=" + weight + ", breed=" + breed + "]";
	}
	@Override
	public boolean isBig(Object obj) {
		
		Dog dog = (Dog)obj;
				
		return this.weight > dog.weight;
	}
	@Override
	public boolean isSmall(Object obj) {
		Dog dog = (Dog)obj;
		
		return this.weight < dog.weight;
	
	}
	
}

```

## Implementing more than  one interface

```

    public class Sample implements MyInterface1,MyInterface2 {

	@Override
	public void test() {
		System.out.println("test() of MyInterface1");
		
	}

	@Override
	public void show() {
		System.out.println("show() of MyInterface2");
		
	}
	
	public void display() {
		
		//System.out.println(SIZE);// Ambiguity error
		System.out.println(MyInterface2.SIZE);
	}
	
	

}


```

## What if both interfaces have method of same name

If that is the case, only the last implemented interface method is overidden.

```
public class Sample implements MyInterface1,MyInterface2 {

	@Override
	public void test() {
		System.out.println("test() of MyInterface2");
		
	}

	@Override
	public void show() {
		System.out.println("show() of MyInterface2");
		
	}
	
	public void display() {
		
		//System.out.println(SIZE);// Ambiguity error
		System.out.println(MyInterface2.SIZE);
	}
```



## Default methods in an Interface
```
package com.trivium.interfaces;

public interface MyInterface3 {
	
	int SIZE= 100;
	void test();
	static void showSize() { // cannot override
		System.out.println("Size is "+ SIZE);
	}
	// Default method
	default void display() {
		System.out.println("display in MyInterface3");
	}

}

```
```
package com.trivium.interfaces;

public class TestDefault implements MyInterface3 {

	@Override
	public void test() {
		
		System.out.println("Implemented test");
		
	}
	@Override
	public void display() {
		// TODO Auto-generated method stub
		System.out.println("Display is overriden from TestDefault");
	}

}

```

```
package com.trivium.interfaces;

public class DefaultApp {

	public static void main(String[] args) {
		TestDefault testDefault = new TestDefault();
		testDefault.display();
		testDefault.test();
		
		MyInterface3.showSize();
		MyInterface3.display(); // cant call this from  interface directly

	}

}

```

## Marker Interface
- A Marker Interface in Java is an interface that does not contain any methods or fields; it serves as a tag to indicate that a class has a specific property or behavior. It allows the Java runtime or frameworks to handle objects differently based on whether they implement the marker interface.
- Eg : Serializable, Clonable


```
package com.trivium.interfaces;

// Marker Interface
public interface MyInterface4 {
	
	
}

```

```
package com.trivium.interfaces;

// Marker Interface
public interface Showable {
	
	
}



```

```
package com.trivium.interfaces;

public class MarkerClass implements Showable {
	
	void show() {
		System.out.println("In show()");
	}
}

```

```


package com.trivium.interfaces;


class ShowableException extends RuntimeException{
	
	String msg;

	public ShowableException(String msg) {
		super();
		this.msg = msg;
	}
	
}

public class MarkerApp {
	
	public static void main(String[] args) {
		MarkerClass markerClass = new MarkerClass();
		

		// Usage

		if(markerClass instanceof Showable) {
			markerClass.show();
		}
		else {
			throw new ShowableException("Not implemented Showable interface");
		}
	}
}


```

# Anonymous class
- A class without a name
- An anonymous class is a class without a name, declared and instantiated in a single expression. It is primarily used when you need a short-lived class instance, typically for event handling or interface implementation.

## Anonymous class for Interface
```
package com.trivium.anonymousclass;

public interface CalculatorInterface {
	
	int computeSum(int num1,int num2);
	int computeProduct(int num1,int num2);
}
	
```

```

public class AnonymousClassDemo2 {
	public static void main(String[] args) {
		
		CalculatorInterface calculator = new CalculatorInterface() {
			
			@Override
			public int computeSum(int num1, int num2) {
				// TODO Auto-generated method stub
				return num1+num2;
			}

			@Override
			public int computeProduct(int num1, int num2) {
				// TODO Auto-generated method stub
				return num1*num2;
			}
		};
	}

}
```
!["Anonymous .class path"](/images//anon.png)

## Nested Class

### Static Class
#### - Static class

### Non Static class
#### - Inner class
#### - Anonymous class



### Anonymous class for abstract class

- Cannot have parametrised constructer for anonymous inner class

# Functional Interface

An interface with only one abstract method

```


public interface Calculator {
	
	float computeSum(float num1,float num2);
	
	
}

```

## @FunctionalInterface annotation

- Forcefully make an interface to be functional interface. So that
  JVM can understand that it is a functional interface


## Functional Interfaces in Java 8

- ### Consumer < T >
	Having a mehtod void accept( T t)\
  To make a function which can accept only one arg and return nothing 

		public static void main(String[] args) {
		
			Consumer<String> greet = name -> System.out.println("Hello " + name+ "!");
				greet.accept("Arun");
		}
- ### Supplier < T >
	It represents a function which does not take in any argument but produces a value of type T.
	
	```
	Supplier<String> greet = () -> "Hello ";
		System.out.println(greet.get());

	```
- ### Function < T , R>
	 - R apply (T t); \
  
	Takes an input of type T and return a value of type R
	 
	

	```
	Function<String, String> greet = name -> "Hello "+name + "!";
		
		System.out.println(greet.apply("Sreenath"));
	```

	```
	Function<Long, Long> fact = num -> computeFact(num);
		System.out.println("Factorial is "+ fact.apply(3L));

	```

- ### Predicate < T >
	 - boolean test(T t); 
	- It represents a boolean-valued function that takes an input and returns either true or false. It is mainly used for filtering, validation, and conditional checks in streams, collections, and other functional programming scenarios.
 
		```
		Predicate<Integer> isMajor = age -> age>=18 ? true:false;
				
				if(isMajor.test(23)) {
					System.out.println("Yes");
				}
				else {
					System.out.println("NO");
				}

		```
	#### Passing Predicate inside a function
	

	```
	static HashMap<String, Integer> computeSum(int nums[], Predicate<Integer> isOdd) {
		
		HashMap<String, Integer> sums = new HashMap<String, Integer>() ;
		int sumEven =0,sumOdd = 0;
		
		for(int i : nums) {
			if(isOdd.test(i)) {
				sumOdd += i;
			}
			else {
				sumEven += i;
			}
		}
		sums.put("Odd", sumOdd);
		sums.put("Even", sumEven);
		return sums;
	}
	
	public static void main(String[] args) {
		
		Predicate<Integer> isOdd = num -> num%2 != 0? true : false;
		
		int nums[] = {2,4,3,1,6,7,5,8,9,0,1,3,9,12,13,27};
		
		System.out.println("sum of Odd numbers : "+computeSum(nums, isOdd).get("Odd")+
				"  sum of Even numbers : "+computeSum(nums, isOdd).get("Even"));
		
		
	}
	```
#  LAMBDA Expression

Lambda expression for an interface is only written if and only if the 
interface is a funtional interface

```

		Calculator calculator = (float num1,float num2) ->{return num1+ num2;};
		System.out.println(calculator.computeSum(12, 13));	
```

## Passing functional interface as parameter

```
public interface Number {
	
	long computeFactorial(int num);
}
```

```
static void test(Number num) {
		System.out.println(num.computeFactorial(5));
	}
	
	static void compute(Calculator calc) {
		
		System.out.println(calc.computeSum(3,5));
	}
	public static void main(String[] args) {

		test((num) -> {
			long f = 1;
			for (int i = 1; i <= num; i++) {
				f = f * i;
			}
			return f;

		});
		
	}
```

## Return functional interface


```
package com.trivium.lamda;

public interface Calculator {
	
	float computeSum(float num1,float num2);
	
	
}

```


```

package com.trivium.lamda;

public class ReturnLambdaApp {
	
	
	static Calculator test() {
		
		return (float num1,float num2)-> num1+num2;
	}
	
	public static void main(String[] args) {
		
		System.out.println(test().computeSum(21, 22));
	}
}

```