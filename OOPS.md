# Object Oriented Programming

## Featrues
 1. Class
 2. Object
 3. Encapsulation
 4. Inheritance
 5. Polymorphism 
 6. Abstraction

!["members and blocks"](/images/oops1.png)


## Class
Classes are used to represent real world entities. It is a blueprint of objects.
With one class, many objects can be created

### Class consists of :
- Member variables
- Memeber functions / Methods

## static keyword
- Used to create class variables and methods
- Static components are loaded when we run java className.class is called or first occurence


## this keyword

- To refer the current object
- Used to call the constructor of the class

```
	

	public class Coordinate {
		
		private float x,y;

		public Coordinate(float x) {
			this.x = x;
			
		}
		
		// instead of the below one 
	//	public Coordinate(float x, float y) {
	//		this.x = x;
	//		this.y = y;
	//	}
		// we can write it like this
		
		public Coordinate(float x, float y) {
			this(x); // must be first statement
			this.y = y;
		}
		
		

	}


```
#### Instance variables

  - variables which are attributes of an object
  - created in the memory when the object is created 
  - Can't use inside a static method

#### Static variables

- Static variables are shared across all instances of a class.
- Static methods and variables are loaded into the memory during the first occurence of the class
- Can be used along with instance methods

```
    Employee e1 = new Employee();
	System.out.println(Employee.orgName); // null
    Employee.orgName = "Trivium"; 
		System.out.println(Employee.orgName);  // Trivium
```
### Constructors    

- Used to create objeccts
- Responsible for object instantiation

### Block 

- Enclosed within { }
- Executed in the order in which it is written
- static block, instance block and local block

```
    package oops;

public class BlocksDemo {
	
	// instance block
	
	{
		System.out.println("This is an instance class");
	}

	public static void main(String[] args) {
		
		BlocksDemo b = new BlocksDemo();
		{
			System.out.println("This local block 1");
		}
		System.out.println("inside menu");
		{
			System.out.println("This local block 2");
		}
		

	}
	// instance block 2
	{
		System.out.println("this an instance block 2");
	}
	
	// static block 1
	static {
		
		System.out.println("this a static block 1");
		
		}
	
	// static block 2
	static {
		
		System.out.println("this a static block 2");
		
	}
	
	
}


output 

    this a static block 1
    this a static block 2
    This is an instance class
    this an instance block 2
    This local block 1
    inside menu
    This local block 2

```
## Getters 
### To  access a private property of an object or class

### Syntax 

     
    public type getXXXX(){
        return this.privatePropertyName;
    }

    For static private vars

    public static String getXXX() {
		return XXXX;
	}
    

## Setters 
### To  set value to a private property of an object or class

### Syntax 

     
    public void setXXXX( type val){
        this.privatePropertyName = val;
    }

    For static private vars
    
    public static void setXXXX(String XXXX) {
		ClassName.XXXXX = XXXX;
	}

## Relations - Is A and Has A relations  

### - Has A : Association - Aggregation and Composition

#### Aggregation - can exist independently
#### Composition - The child (part) cannot exist without the parent (whole).



## Encapsulation

- Both data and methods that operates on the data is bind together inside a class
- Provides data hiding and modularity
- Data hiding can be performed using access specifier


### Access specifier

- public
- protected
- default
- private

## Inheritance
!["Inheritance in memory"](/images/inheritance.png)

- in the constructor of child class super(); must be called first to ensure parent class initialization before the child class.

- First the sub class constructer will be called first but the super class is instanciated first


### Simple inheritance 

``` 
	// Person class
	package com.trivium.inheritance;

	public class Person1 {
		private String name;
		private int age;

		public Person1(String name, int age) {
			super();
			this.name = name;
			this.age = age;
		}

		@Override
		public String toString() {
			return "Person1 [name=" + name + ", age=" + age + "]";
		}

		public String getName() {
			return name;
		}

		public int getAge() {
			return age;
		}

	}

```
```
	// Employee class

	public class Employee1 extends Person1 {

		private int eno;
		private float basicPay;

		public Employee1(String name, int age, int eno, float basicPay) {
			super(name, age);
			this.eno = eno;
			this.basicPay = basicPay;
		}

		@Override
		public String toString() {
			return "Employee1 [eno=" + eno + ", basicPay=" + basicPay + ", getName()=" + getName() + ", getAge()="
					+ getAge() + "]";
		}

	}
```
```
	// main

	public class InheritanceDemo2 {
		public static void main(String[] args) {
			
			Employee1 emp1 = new Employee1("Sreenath", 23, 101, 90000);
			System.out.println(emp1);
		}
	}
```

### Multilevel inheritance

class A -> class B -> class C


## Polymorphism

### Method overriding
- Runtime Polymorphism

- The class should be inherited from a parent class
- Signature should be same



```

public class A {
	
	void show() {
		System.out.println("Message from class A");
	}
}


```

```  


public class B extends A {
	
	void test() {
		System.out.println("Message from class B");
	}
	
	
	@Override
	void show() {
		System.out.println("This is from B");
	}
}


```

``` 

public class MethodOverridingDemo {

	public static void main(String[] args) {
		
		
		B b = new B();
		b.test();
		b.show();

	}
	
	

}


```

### Dynamic  binding / Polymorphism

Since the child object has some part of parent class in the memory,
during the runtime , parent class will be able to refer that area. The JVM can't identify this
during the compile time.

``` 
		
		A aObj = new A();
		aObj.show();
		
		A bObj = new B();
		bObj.show();
//		bObj.test(); wont work

```
With Multilevel inheritance A->B->C

```
	A cobj = new C();
	cobj.show(); // "Message from B"
```


### Method overloading

- Compile time binding 
- signature is different
- differ in arg datatype, number of args , order of args

``` 

package com.trivium.oops;

public class MethodOverLoadingDemo {

	void show() {
		System.out.println("Show without arguments");
	}

	void show(int x) {
		System.out.println("Show with 1 int argument : " + x);
	}

	void show(String y) {
		System.out.println("Show with 1 string argument : " + x);
	}

	void show(int x, String y) {
		System.out.println("Show with 1 int and 1 String arguments : " + x + " " + y);
	}

	void show(String y, int x) {
		System.out.println("Show with  1 String and 1 int arguments : " + y + " " + x);
	}

	public static void main(String[] args) {
		
		MethodOverLoadingDemo m = new MethodOverLoadingDemo();
		m.show();
		m.show(12);
		m.show("hello" );
		m.show(12, "hello");
		m.show("hello",12);
		

	}

}


```

### instanceof operator

```
	a instanceof A -> bool
``` 

## Abstraction 

- Child should implement all the abstract methods
- Otherwise make the child class abstract as well



```
	public abstract class Shape {
	
		abstract void computeArea() ;
		abstract void computePerimeter();

	}

```
```
	public static void main(String[] args) {
		Shape s = null; // allowed

		s = new Square(7);
		s.computeArea();
		s.computePerimeter();

	}

```