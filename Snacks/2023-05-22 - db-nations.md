## Repo
`db-nations`

## Dump
![[dump_nations.sql]]

## E-R
![[Pasted image 20230522124951.png]]![[dump_nations.sql]]
## Soluzione
```java
String url = "jdbc:mysql://localhost:3306/db_nations";
String user = "root";
String password = "code";

try (Scanner sc = new Scanner(System.in);
		Connection con = DriverManager.getConnection(url, user, password)) {
	
	String sql = " SELECT c.name, c.country_id, r.name, c2.name "
			+ " FROM countries c "
			+ " 	JOIN regions r "
			+ " 		ON c.region_id = r.region_id "
			+ " 	JOIN continents c2 "
			+ " 		ON r.continent_id = c2.continent_id "
			+ " WHERE c.name LIKE ? "
			+ " ORDER BY c.name; ";
	
	try (PreparedStatement ps = con.prepareStatement(sql)) {
			
		System.out.print("Parametro di ricerca: ");
		String search = sc.nextLine();
		
		ps.setString(1, "%" + search + "%");
		
		try (ResultSet rs = ps.executeQuery()) {
		
			while(rs.next()) {
				
				final String countryName = rs.getString(1);
				final int countryId = rs.getInt(2);
				final String regionName = rs.getString(3);
				final String continentName = rs.getString(4);
				
				System.out.println(countryName + " - " + countryId 
						+ " - " + regionName + " - " + continentName);
				System.out.println("-------------------------------");
			}
		} catch(Exception e) {	}
	} catch(Exception e) { }
	
	System.out.print("Id nazione: ");
	final String strIdNation = sc.nextLine();
	final int idNation = Integer.valueOf(strIdNation);
	
	System.out.println("");
	
	String subSql1 = " SELECT l.`language` "
					+ " FROM country_languages cl "
					+ "	JOIN languages l "
					+ "		ON cl.language_id = l.language_id "
					+ " WHERE cl.country_id = ?; ";
	String subSql2 = " SELECT c.name, cs.* "
					+ " FROM countries c "
					+ "	JOIN country_stats cs "
					+ "		ON c.country_id = cs.country_id "
					+ " WHERE cs.country_id = ? "
					+ " ORDER BY cs.`year` DESC "
					+ " LIMIT 1; ";
	
	try (PreparedStatement ps1 = con.prepareStatement(subSql1);
			PreparedStatement ps2 = con.prepareStatement(subSql2);) {
		
		ps1.setInt(1, idNation);
		ps2.setInt(1, idNation);
		
		try (ResultSet rs1 = ps1.executeQuery();
				ResultSet rs2 = ps2.executeQuery()) {

			if (!rs2.next()) return;
			
			String nationName = rs2.getString(1);
			
			System.out.println("Details for country: " + nationName);
			System.out.print("Languages: ");
			
			while(rs1.next()) {
				
				System.out.print(rs1.getString(1) 
						+ (rs1.isLast() ? "" : ", "));
			}
			
			System.out.println("\nMost recent stats");
			System.out.println("Year: " + rs2.getInt(3));
			System.out.println("Population: " + rs2.getInt(4));
			System.out.println("GDP: " + rs2.getLong(5));
		} catch(Exception e) { }
	} catch(Exception e) { }
} catch (Exception e) { }
```
## Todo
### MILESTONE 1
Creare un nuovo database in `DBeaver` e importare lo schema in
allegato.
Scrivere una** query SQL** che restituisca la lista di tutte le nazioni
mostrando `nome`, `id`, `nome della regione` e `nome del continente`, ordinata per `nome della nazione`.

### MILESTONE 2
Creare un progetto `Maven`, configurato in modo da **potersi connettere ad un database MySQL**.
Nel progetto creare un programma che esegua la query della **Milestone
1** e stampi a video il risultato.

### MILESTONE 3
Modificare il **programma precedente** per fare in modo che un utente
possa effettuare ricerche tra i risultati:
- chiedere all’utente di inserire **una stringa** di ricerca da `terminale`
- usare quella stringa come **parametro aggiuntivo** della `query` in
modo che i risultati vengano filtrati con un `contains` (ad esempio se
l’utente cerca per “**ita**”, il risultato della query conterrà sia **Italy** che
**Mauritania**.

### BONUS
Dopo aver **stampato a video** l’elenco delle `country`, chiedere all’utente di inserire l’`id` di una delle `country`.
Sulla base di quell’id eseguire ulteriori ricerche su database, che restituiscano:
- tutte le **lingue parlate** in quella `country`
- le **statistiche** più recenti per quella `country`

Stampare a video i risultati.
Di seguito un esempio di programma completo:
![[Pasted image 20230522125504.png]]