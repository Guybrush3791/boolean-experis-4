## Schema ER
![[DB Aiport.png]]

## Dump
![[__assets/dump/mysql-db_aeroporto.sql]]

## Todo
### Query su singola tabella
- Selezionare tutti i passeggeri (1000) 
```sql
SELECT *
FROM passengers
```

- Selezionare tutti i nomi degli aeroporti, ordinati per nome (100)
```sql
SELECT *
FROM airports
ORDER BY airports.name;
```

- Selezionare tutti i passeggeri che hanno come cognome 'Bartell' (2)
```sql
SELECT *
FROM passengers
WHERE lastname LIKE 'bartell';
```

- Selezionare tutti i passeggeri minorenni (considerando solo l'anno di nascita) (96 - nel 2023)
```sql
SELECT *
FROM passengers
WHERE YEAR(NOW()) - YEAR(date_of_birth) < 18
```

- Selezionare tutti gli aerei che hanno piu' di 200 posti (84)
```sql
SELECT *
FROM airplanes
WHERE seating_capacity > 200;
```

- Selezionare tutti gli aerei che hanno un numero di posti compreso tra 350 e 700 (30)
```sql
SELECT *
FROM airplanes
WHERE seating_capacity > 350 AND seating_capacity  < 700;
```
```sql
SELECT *
FROM airplanes
WHERE seating_capacity BETWEEN 350 AND 700;
```

- Selezionare tutti gli ID dei dipendenti che hanno lasciato almeno una compagnia aerea (31077)
```sql
SELECT employee_id 
FROM airline_employee
WHERE layoff_date IS NOT NULL;
```

- Selezionare tutti gli ID dei dipendenti che hanno lasciato almeno una compagnia aerea prima del 2006 (493)
```sql
SELECT *
FROM airline_employee
WHERE layoff_date IS NOT NULL
	AND YEAR(layoff_date) < 2006;
```

- Selezionare tutti i passeggeri il cui nome inizia con 'Al' (26)
```sql
SELECT *
FROM passengers
WHERE name LIKE 'al%';
```

- Selezionare tutti i passeggeri nati nel 1960 (11)
```sql
SELECT *
FROM passengers
WHERE YEAR(date_of_birth) = 1960;
```

### Bonus
- contare tutti gli aeroporti la cui città inizia per 'East' (7)
```sql
SELECT COUNT(*) 
FROM airports
WHERE city LIKE 'east%';
```

- Contare quanti voli sono partiti il 4 luglio 2019 (3)
```sql
SELECT COUNT(*) 
FROM flights
WHERE DATE(departure_datetime) = '2019-07-04';
```



### Query con group by
- Contare quanti lavori di manutenzione ha eseguito ogni impiegato(dell'impiegato vogliamo solo l'ID) (1136)
```sql
SELECT employee_id, COUNT(*)
FROM employee_maintenance_work
GROUP BY employee_id 
```

- Contare quante volte ogni impiegato ha lasciato una compagnia aerea (non mostrare quelli che non hanno mai lasciato; dell'impiegato vogliamo solo l'ID) (8939)
```sql
SELECT employee_id, COUNT(*) 
FROM airline_employee
WHERE layoff_date IS NOT NULL
GROUP BY employee_id 
```

- Contare per ogni volo il numero di passeggeri (del volo vogliamo solo l'ID) (1000)
```sql
SELECT flight_id, COUNT(*)
FROM flight_passenger
GROUP BY flight_id 
```

- Ordinare gli aerei per numero di manutenzioni ricevute (da quello che ne ha di piu'; dell'aereo vogliamo solo l'ID) (100)
```sql
SELECT airplane_id, COUNT(*) AS 'mantCount' 
FROM maintenance_works
GROUP BY airplane_id 
ORDER BY mantCount DESC
```

- Contare quanti passeggeri sono nati nello stesso anno (61)
```sql
SELECT YEAR(date_of_birth), COUNT(*)
FROM passengers
GROUP BY YEAR(date_of_birth)
```

- Contare quanti voli ci sono stati ogni anno (tenendo conto della data di partenza) (11)
```sql
SELECT YEAR(departure_datetime), COUNT(*)
FROM flights
GROUP BY YEAR(departure_datetime)
```

### Bonus
- Per ogni manufacturer, trovare l'aereo con maggior numero di posti a sedere (8)
```sql
SELECT manufacturer, MAX(seating_capacity)
FROM airplanes
GROUP BY manufacturer
```

- Contare quante manutenzioni ha ricevuto ciascun aereo nel 2021 (dell'aereo vogliamo solo l'ID) (36)
```sql
SELECT airplane_id, COUNT(*) 
FROM maintenance_works
WHERE YEAR(`datetime`) = 2021
GROUP BY airplane_id 
```

- Selezionare gli impiegati che non hanno mai cambiato compagnia aerea per cui lavorano (1061)
```sql
SELECT employee_id, COUNT(*) AS 'compCount'
FROM airline_employee 
GROUP BY employee_id 
HAVING compCount = 1;
```



### Query con join
- Selezionare tutti i passeggeri del volo 70021493-2 (85)
```sql
SELECT p.*
FROM flights f 
	JOIN flight_passenger fp
		ON f.id = fp.flight_id
	JOIN passengers p 
		ON fp.passenger_id = p.id 
WHERE f.`number` LIKE '70021493-2';
```

- Selezionare i voli presi da 'Shirley Stokes' (61)
```sql
SELECT f.*
FROM passengers p
	JOIN flight_passenger fp 
		ON p.id = fp.passenger_id 
	JOIN flights f 
		ON fp.flight_id = f.id 
WHERE p.name LIKE 'Shirley'
	AND p.lastname LIKE 'Stokes';
```

- Selezionare tutti i passeggeri che hanno usato come documento 'Passport'(775)
```sql
SELECT UNIQUE p.*
FROM document d
	JOIN document_types dt 
		ON d.document_type_id = dt.id 
	JOIN passengers p 
		ON d.passenger_id = p.id 
WHERE dt.name LIKE 'passport';
```

- Selezionare tutti i voli con i relativi passeggeri (65296)
```sql
SELECT f.*, p.*
FROM passengers p
	JOIN flight_passenger fp 
		ON p.id = fp.passenger_id 
	JOIN flights f 
		ON fp.flight_id = f.id;
```

- Selezionare tutti i voli che partono da 'Charleneland' e arrivano a 'Mauricestad' (3)
```sql
SELECT f.*
FROM flights f 
	JOIN airports a 
		ON f.departure_airport_id = a.id 
	JOIN airports a2 
		ON f.arrival_airport_id = a2.id
WHERE a.city LIKE 'Charleneland' 
	AND a2.city LIKE 'Mauricestad';
```

- Selezionare tutti gli id dei voli che hanno almeno un passeggero il cui cognome inizia con 'L' (935)
```sql
SELECT fp.flight_id 
FROM flight_passenger fp 
	JOIN passengers p 
		ON fp.passenger_id = p.id
WHERE p.lastname LIKE 'l%'
GROUP BY fp.flight_id;
```

- Selezionare i dati delle compagnie dove c'e' almeno un impiegato che e' stato licenziato (286)
```sql
SELECT UNIQUE a.*
FROM airlines a 
	JOIN airline_employee ae 
		ON a.id = ae.airline_id
WHERE ae.layoff_date IS NOT NULL;
```

- Selezionare tutti gli aerei che sono partiti almeno una volta dalla città di 'Domingochester' (12)
```sql
SELECT UNIQUE a.*
FROM airplanes a 
	JOIN flights f 
		ON a.id = f.airplane_id 
	JOIN airports a2 
		ON f.departure_airport_id = a2.id
WHERE a2.city LIKE 'Domingochester';
```

- Selezionare i dati dei tecnici e gli aerei ai quali questi hanno fatto almeno un intervento di manutenzione (1506)
```sql
SELECT e.*, a.*
FROM airplanes a 
	JOIN maintenance_works mw 
		ON a.id = mw.airplane_id 
	JOIN employee_maintenance_work emw 
		ON mw.id = emw.maintenance_work_id 
	JOIN employees e
		ON emw.employee_id = e.id;
```

- Selezionare tutti i piloti che hanno viaggiato nel 2021 partendo dall'aeroporto di 'Abshireland' (4)
```sql
SELECT UNIQUE e.*
FROM employees e 
	JOIN roles r 
		ON e.role_id = r.id 
	JOIN employee_flight ef 
		ON e.id = ef.employee_id 
	JOIN flights f 
		ON ef.flight_id = f.id 
	JOIN airports a 
		ON f.departure_airport_id = a.id
WHERE a.city LIKE 'Abshireland'
	AND YEAR(f.departure_datetime) = 2021
	AND r.name = 'pilot';
```

### Bonus
- Selezionare i dati di tutti i passeggeri che hanno volato su un qualche aereo riparato da 'Aaliyah Leannon' (590)
```sql
SELECT UNIQUE p.*
FROM employees e 
	JOIN employee_maintenance_work emw 
		ON e.id = emw.employee_id 
	JOIN maintenance_works mw 
		ON emw.maintenance_work_id = mw.id 
	JOIN airplanes a 
		ON mw.airplane_id = a.id
	JOIN flights f 
		ON a.id = f.airplane_id 
	JOIN flight_passenger fp 
		ON f.id = fp.flight_id 
	JOIN passengers p 
		ON fp.passenger_id = p.id
WHERE e.name LIKE 'Aaliyah'
	AND e.lastname LIKE 'Leannon';
```

- Contare quanti piloti ha la compagnia 'Maldivian (Q2)' (10)
```sql
SELECT e.*
FROM airlines a 
	JOIN airline_employee ae 
		ON a.id = ae.airline_id 
	JOIN employees e 
		ON ae.employee_id = e.id 
	JOIN roles r 
		ON e.role_id = r.id
WHERE a.name LIKE 'Maldivian (Q2)'
	AND r.name LIKE 'pilot'
	AND ae.layoff_date IS NULL;
```

- Contare quanti dipendenti ha ogni compagnia aerea (286)
```sql
SELECT a.*, COUNT(*)
FROM airlines a 
	JOIN airline_employee ae 
		ON a.id = ae.airline_id 
	JOIN employees e 
		ON ae.employee_id = e.id 
WHERE ae.layoff_date IS NULL
GROUP BY a.id;
```
