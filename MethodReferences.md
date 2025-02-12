# Method Reference


In Java, method references provide a way to refer to methods of a class or an object using the :: operator. They are a shorthand for lambda expressions when working with functional interfaces.

``` :: ``` is called method references operator

## 3 Types of Method references
### 1. Static method references
    ``` ClassName::staticMethodName ```
    Eg:
```
public class MethodReferenceDemo1 {

	public static void sayHello() {
		System.out.println("Hello");
	}

	public static void main(String[] args) {
		
		
		Greetings greet = MethodReferenceDemo1 ::sayHello;
		greet.showMessage();

	}

}

```
With parameter

```
public class Test {
	
	
	public static void sayHello() {
		System.out.println("Hello");
	}
	
	public static void sayHello(String name) {
		System.out.println("Hello "+ name +"!");
	}
}

```

```
		
		Greetings1 greetAgain = Test::sayHello;
		greetAgain.showMessage("Arun");
	

```

### 2. Reference to an Instance Method of a Particular Object

```

public class MethodReferencedemo2 {
	
	void sayHello() {
		System.out.println("Hello!");
	}
	public static void main(String[] args) {
		
		MethodReferencedemo2 obj = new MethodReferencedemo2();
		Greetings greet = obj::sayHello;
		greet.showMessage();
		

	}

}


```
### 3. Reference to a Constructor (Constructor Reference)

```

public class MethodReferenceDemo3 {
	
	

	public MethodReferenceDemo3() {
		super();
		System.out.println("Helloooo!!");
	}

	public static void main(String[] args) {
		
		Greetings greet = MethodReferenceDemo3::new;
		greet.showMessage();

	}

}

```