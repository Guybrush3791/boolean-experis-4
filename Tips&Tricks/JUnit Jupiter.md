Creare progetto vuoto con `Maven` e aggiungere al file `pom.xml` le seguenti direttive:
```xml
  <properties>
	<maven.compiler.source>1.8</maven.compiler.source>
	<maven.compiler.target>1.8</maven.compiler.target>
  </properties>
  
  <dependencies>
	<dependency>
	    <groupId>org.junit.jupiter</groupId>
	    <artifactId>junit-jupiter-engine</artifactId>
	    <version>5.10.0-M1</version>
	    <scope>test</scope> 
	</dependency>
  </dependencies>
  
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>2.22.0</version>
      </plugin>
    </plugins>
  </build>
```

All'interno del progetto, per ogni classe che si vuole testare, creare una classe controparte con lo stesso nome piu' l'aggiunta della parola `Test`
![[Pasted image 20230523122524.png]]

Per ogni metodo da testare creare uno o piu' metodi con lo stesso nome del metodo da testare piu' l'aggiunta di risultati attesi e test.

Es:
**metodo da testare**
```java
public int getSum() { /*...*/ }
```

**metodi di testing**
```java
public void getSumTest() { /*...*/ }
public void getSumPoisitiveTest() { /*...*/ }
```

All'interno dei metodi di testing usare oppurtunamente una combinazione di `assumeTrue`/`assumeFalse` e `assert[data-type]` (`assertEquals`, `assertString`, `assertTrue`, ecc).

Es:
```java
	@RepeatedTest(10)
	public void getDivTest() throws Exception {
		
		assumeTrue(c.getY() != 0);
		
		final int attRes = c.getX() / c.getY();
		
		final int res = c.getDiv();
		
		assertEquals(attRes, res, "Divisione tra interi");
	}
	
	@RepeatedTest(10)
	public void getDivExcTest() {
		
		assumeTrue(c.getY() == 0);
		
		assertThrows(Exception.class,
				() -> c.getDiv(),
				"Deve sollevare eccezione");
	}
```

Per lanciare la fase di test, tasto dx sul progetto -> Run as -> Maven test
Comparira a terminale una serie di scritte indicandi l'esito dei test e se il progetto e' stato correttamente buildato oppure no:
![[Pasted image 20230523123525.png]]