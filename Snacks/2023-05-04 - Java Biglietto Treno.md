## Repo
`java-biglietto-treno`

## Todo
### Main Ex
Il programma dovrà chiedere all’utente il *numero di chilometri* che vuole percorrere e l’*età del passeggero*. Sulla base di queste informazioni dovrà calcolare il prezzo totale del viaggio, secondo queste regole:
- il prezzo del biglietto è definito in base ai km (0.21 € al km)
- va applicato uno sconto del 20% per i minorenni
- va applicato uno sconto del 40% per gli over 65

Come sempre create un progetto java con lo stesso nome del repo (`java-biglietto-treno`), aggiungete un package `org.lessons.java` e una classe `CalcolaBiglietto`. Il programma va implementato nel metodo `main` della classe `CalcolaBiglietto`.
Per acquisire l’input dell’utente usate la classe `Scanner`, come visto stamattina a lezione.

Buon lavoro!

[Correzione](https://github.com/Guybrush3791/exp-java-4-java-biglietto-treno/blob/main/src/org/lessons/java/CalcolaBiglietto.java)

### Update: 15:10
> [!note] PER CHI HA FINITO

Aggiungere al `package` dell'esercizio precedente una classe `CibiPreferiti` col suo metodo `main`.
Nel programma inizializzate un `array` (con i metodi visti a lezione) con la *classifica dei vostri cibi preferiti* (minimo 5, massimo 10 elementi).

Poi stampate a video:
- la *lunghezza della classifica*
- il vostro *cibo top* (prima posizione della classifica)
- il vostro *cibo preferito ma non troppo* (ultima posizione della classifica)

#### BONUS
Stampate a video anche il cibo di mezza classifica, cioè che si trova nella posizione mediana.

[Correzione](https://github.com/Guybrush3791/exp-java-4-java-biglietto-treno/blob/main/src/org/lessons/java/CibiPreferiti.java)

### Update: 17:00
Aggiungere al `package` dell'esercizio precedente una classe `FizzBuzz` col suo metodo `main`.
Scrivi un programma che stampi i numeri *da 1 a 100*,
ma per *i multipli di 3 stampi Fizz* al posto del numero e *per i multipli di 5 stampi Buzz*.
Per i numeri che sono *sia multipli di 3 che di 5 stampi FizzBuzz*.

#### Bonus
Chiede all'utente il numero di valori da valutare (al posto di fermarsi a 100, fermarsi al valore suggerito dall'utente).

[Correzione](https://github.com/Guybrush3791/exp-java-4-java-biglietto-treno/blob/main/src/org/lessons/java/FizzBuzz.java)

### EX: Bonus
State lavorando col servizio di sicurezza dei Ferragnez e il vostro compito è di *assicurarvi che accedano alla festa solo gli invitati presenti sulla lista* (in fondo al post).

Aggiungere al `package` dell'esercizio precedente una classe `CheckGuest` col suo metodo `main`.
Generare all'interno del `main` un array contenente la lista degli invitati (presente in calce).
Chiedere poi all'utente il suo nome e verificarne la presenza nella lista, dando risposta sensata all'utente.

#### Bonus
Nel caso in cui sia stato utilizzato il ciclo `for`, svolgere la stessa ricerca tramite ciclo `while` e viceversa

#### Data
```
Lista invitati: Dua Lipa, Paris Hilton, Manuel Agnelli, J-Ax, Francesco Totti, Ilary Blasi, Bebe Vio, Luis, Pardis Zarei, Martina Maccherone, Rachel Zeilic
```

[Correzione](https://github.com/Guybrush3791/exp-java-4-java-biglietto-treno/blob/main/src/org/lessons/java/CheckGuest.java)