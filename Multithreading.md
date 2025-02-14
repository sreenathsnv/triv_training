# Multithreading in Java

## Process

 Program in execution

### A Process consists of

- Data
- text/code
- Heap
- Stack





## Thread Demo


```

class Thread1 extends Thread {
	@Override
	public void run() {

		System.out.println("run() of Thread");
	}
}

public class ThreadDemo1 {

	public static void main(String[] args) throws InterruptedException {
		
		
		Thread1 t1 = new Thread1();
		t1.start();
		System.out.println("End of main");

	}

}

```

### output

    End of main
    run() of Thread

### reason 

 First the main thread is being executed, then it created the 
 t1 thread and starts  the thread and print the value.
 After that actually the time slot given to main is ended and it executes the second thread t1


 ## Using sleep

 ```

package com.trivium.multithreading;

class Thread1 extends Thread {
	@Override
	public void run() {

		System.out.println("run() of Thread");

		for (int i = 0; i < 10; i++) {
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			System.out.println(i + "-> line");
		}
	}
}
 ```

 ```

 public class ThreadDemo1 {

	public static void main(String[] args)  {

		Thread1 t1 = new Thread1();

		t1.start();

		for (int i = 0; i < 10; i++) {
			try {
				Thread.sleep(2000);
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			System.out.println("main thread ->"+i);
		}

	}

}

 ```

 ## join method

 allows a thread to wait until another thread has finished executing

 ```
public class ThreadDemo1 {

	public static void main(String[] args) {

		Thread1 t1 = new Thread1();

		t1.start();

		try {
			t1.join();
			/*t1.join(1000);
			t1.join(1000, 101);*/
			
		} catch (InterruptedException e) {

			e.printStackTrace();
		}
		
		
		
		System.out.println("END OF MAIN");
	}

}

 ```

 # Runnable Intefrace


 ```
 package com.trivium.multithreading;

class Thread4 implements Runnable {

	Thread th;

	// dont have a start method, thats why we create like this
	public Thread4() {

		th = new Thread(this,"Thread4");
		th.start();
	}

	@Override
	public void run() {

		for (int i = 0; i < 10; i++) {

			System.out.printf("instance -> %d\n", i);
		}
		System.out.println("END OF THREAD");
	}
}

public class ThreadDemo4 {

	public static void main(String[] args) {
		
		Thread4 t1 = new Thread4();
		
		try {
			t1.th.join();
		} catch (InterruptedException e) {
			
			e.printStackTrace();
		}
		
		System.out.println("END OF MAIN");
		
	}

}

 
 ```

## Fail Fast Itertaor

A Fail-Fast Iterator in Java is an iterator that immediately throws a ConcurrentModificationException if it detects any structural modification to the underlying collection during iteration. It helps prevent unpredictable behavior when multiple threads or modifications occur during traversal.

 ```

		HashMap<Integer, String> hm = new HashMap<Integer, String>();
		hm.put(10, "Arun");
		hm.put(11, "Varun");
		hm.put(12, "Arjun");
		hm.put(13, "Tarun");
		hm.put(14, "Akhil");
		
		System.out.println(hm);
		
		
		Set<Integer> keys = hm.keySet();
		Iterator<Integer> itr = keys.iterator();
		
		// fail fast iterator
		while(itr.hasNext()) {
			System.out.println(itr.next());
			hm.put(15, "Raju"); // throws java.util.ConcurrentModificationException
		}
 ```

 ### using concurrent HashMap

 ```

ConcurrentHashMap<Integer, String> hm = new ConcurrentHashMap<Integer, String>();
		hm.put(10, "Arun");
		hm.put(11, "Varun");
		hm.put(12, "Arjun");
		hm.put(13, "Tarun");
		hm.put(14, "Akhil");
		
		System.out.println(hm);
		
		
		Set<Integer> keys = hm.keySet();
		Iterator<Integer> itr = keys.iterator();
		
		// fail fast iterator
		while(itr.hasNext()) {
			System.out.println(itr.next());
			hm.put(15, "Raju"); // throws java.util.ConcurrentModificationException
		}


 ```