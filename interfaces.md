
# Interfaces in Java

## Declaration and definition

- Use interface keyword

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