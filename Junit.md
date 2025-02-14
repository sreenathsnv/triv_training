# Junit in java

## @Test and @BeforeEach

```
package com.trivium.junit;

public class Calculator {

	public float add(float num1, float num2) {
		return num1 + num2;
	}
	
	public float difference(float num1, float num2) {
		return num1 - num2;
	}
	public float product(float num1, float num2) {
		return num1 * num2;
	}
	public float division(float num1, float num2) {
		
		try {
			return num1/num2;
		}catch(ArithmeticException e) {
			e.printStackTrace();
		}
		return -1;
	}

}


```


```

package com.trivium.junit;

import static org.junit.jupiter.api.Assertions.assertEquals;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

public class CalculatorTest {
	
	Calculator c = null;
	
	@BeforeEach
	void init() {
		c = new Calculator();
	}

	@Test
	void testAdd() {

		c = new Calculator();

		float actual = c.add(2, 3);

		assertEquals(5f, actual);
	}

	@Test
	void testDifference() {

		c = new Calculator();
		float actual = c.difference(3, 4);

		assertEquals(-1f, actual);
	}

	@Test
	void testProduct() {

		c = new Calculator();
		float actual = c.product(3, 4);

		assertEquals(12f, actual);
	}

	@Test
	void testDivision() {

		c = new Calculator();
		float actual = c.division(6, 2);

		assertEquals(2f, actual);
	}
}



```