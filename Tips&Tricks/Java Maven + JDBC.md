## Maven
Creare nuovo `progetto Maven`
![[Pasted image 20230522123937.png]]
Selezionare la **checkbox** `Create a simple project( skip archetype seletion)`
![[Pasted image 20230522124045.png]]

Definire `Group Id` e `Artifact Id` avendo cura che l'`Artifact Id` sia un **sott-pacchetto** del `Group Id`
![[Pasted image 20230522124721.png]]

### Dependencies
Per gestire le dipendenze tramite `Maven` basta aggiungerle all'interno del file `pom.xml`
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>org.java.query</groupId>
  <artifactId>org.java.query.sql</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  
  <dependencies>
	  <dependency>
		// ...
	  </dependency>
  </dependencies>
</project>
```

## JDBC
### Importare dipendenze
Definire la dipendenza nel `pom.xml`
```xml
<dependencies>
  <dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
	<version>8.0.33</version>
  </dependency>
</dependencies>
```
> [!note] Riferirsi al sito [MVN](https://mvnrepository.com/)

### Utilizzo della libreria
Attraverso la dipendenza e' possibile connettersi al *database* attraverso l'`url`, `user` e `password`
```java
public static void main(String[] args) {
		
		String url = "jdbc:mysql://localhost:3306/db-aereoporto";
		String user = "root";
		String password = "code";
		
		try (Scanner sc = new Scanner(System.in);
				Connection con = DriverManager.getConnection(url, user, password)){
		    
			String sql = " SELECT * FROM passengers "
					+ " WHERE lastname LIKE ? ";
			
			System.out.print("Ricerca passeggeri per cognome: ");
			String searchLastname = sc.nextLine();
			
			try (PreparedStatement ps = con.prepareStatement(sql)) {
				
				ps.setString(1, searchLastname);
				
				try (ResultSet rs = ps.executeQuery()) {
					
					while(rs.next()) {
						
						final int id = rs.getInt(1);
						final String name = rs.getString(2);
						final String lastname = rs.getString(3);
						final Date dateOfBirth = rs.getDate(4);
						
						System.out.println(id + " - " + name + " - " 
								+ lastname + " - " + dateOfBirth);
					}
				}				
			} catch (SQLException ex) {
				System.err.println("Query not well formed");
			}
		} catch (SQLException ex) {
			System.err.println("Error during connection to db");
		}
	}
	
	public static LocalDateTime getLocalDateTime(Timestamp time) {
		
		return LocalDateTime
				.ofInstant(Instant.ofEpochMilli(time.getTime()), 
						TimeZone.getDefault().toZoneId());  
	}
```