# Object Oriented Programming

## Featrues
 1. Class
 2. Object
 3. Encapsulation
 4. Inheritance
 5. Polymorphism 
 6. Abstraction


## Class
Classes are used to represent real world entities. It is a blueprint of objects.
With one class, many objects can be created

### Class consists of :
- Member variables
- Memeber functions / Methods

## static keyword
- Used to create class variables and methods
- Static components are loaded when we run java className.class is called or first occurence

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
- Responsible for object instanciation

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