## Repo
`java-oop-shop`

## Todo
Nel progetto `java-oop-shop`, package `org.lessons.java.shop`, creare la classe `Prodotto` che gestisce i prodotti dello shop. 

Un prodotto è caratterizzato da:
- codice (numero intero)
- nome
- descrizione
- prezzo
- iva

Usate opportunamente i livelli di accesso (`public`, `private`), i costruttori, i metodi getter e setter ed eventuali altri metodi di *utilità* per fare in modo che:
- alla creazione di un nuovo prodotto il codice sia valorizzato con un numero random
- il codice prodotto sia accessibile solo in lettura
- gli altri attributi siano accessibili sia in lettura che in scrittura
- il prodotto esponga sia un `metodo` per avere il *prezzo base* sia uno per avere il prezzo *comprensivo di iva*
- il prodotto esponga un metodo per avere il nome esteso, ottenuto concatenando `codice-nome`

Nello stesso package aggiungete una classe `Main` con metodo `main` nella quale testate tutte le funzionalità della classe `Prodotto`

### BONUS
Create un metodo che restituisca il codice con un pad left di 0 per arrivare a 8 caratteri (ad esempio codice 91 diventa 00000091, mentre codice 123445567 resta come è).