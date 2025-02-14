# Date and Calendar


```

Date d1 = new Date();
		System.out.println(d1);
		
		
		SimpleDateFormat df = new SimpleDateFormat("dd-MM-yyyy");
```		
		dd - date
		MM - Month
		yyyy - year
		mm - minutes

```		
		String s = df.format(d1);
		System.out.println(s);



```


## Calendar

```
Calendar cal1 = new GregorianCalendar(2008,01,01);
		System.out.println("Year "+ cal1.get(Calendar.YEAR));
		System.out.println("Month "+ cal1.get(Calendar.MONTH));
		System.out.println("Day "+ cal1.get(Calendar.DAY_OF_MONTH));

```

```

public static void main(String[] args) {
		
		Calendar cal1 = new GregorianCalendar(2008,01,01);
		System.out.println("Year "+ cal1.get(Calendar.YEAR));
		System.out.println("Month "+ cal1.get(Calendar.MONTH));
		System.out.println("Day "+ cal1.get(Calendar.DAY_OF_MONTH));
		
		SimpleDateFormat df = new SimpleDateFormat("dd/MM/yyyy");
		
		System.out.println(df.format(cal1.getTime()));

```

### Output

```

Year 2008
Month 1
Day 1
01/02/2008
```
## Date Time Package


```

public static void main(String[] args) {
	
		DayOfWeek dow = DayOfWeek.MONDAY;
		Locale locale = Locale.getDefault();
		
		System.out.println(dow.getDisplayName(TextStyle.FULL, locale));
		System.out.println(dow.getDisplayName(TextStyle.NARROW, locale));
		System.out.println(dow.getDisplayName(TextStyle.SHORT, locale));
		

	}


```
#### Output
```

Monday
M
Mon

```


#### Adding two days

``` 		System.out.println(DayOfWeek.MONDAY.plus(3));``` 

```THURSDAY ```



#### Finding next wednesday

```
LocalDate local = LocalDate.of(2000, Month.FEBRUARY, 13);
		LocalDate nextWed = local.with(TemporalAdjusters.next(DayOfWeek.WEDNESDAY));
		System.out.println(nextWed);

```

#### Getting all the zones

````
Set<String> zones = ZoneId.getAvailableZoneIds();
		
		for(String s: zones) {
			System.out.println(s);
		}
````