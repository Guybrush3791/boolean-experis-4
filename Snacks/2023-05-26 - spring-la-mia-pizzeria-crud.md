## Repo
`spring-la-mia-pizzeria-crud`

## Live
Vedi [[2023-05-29 - crud books]]

## Todo
### Day 1
Abbiamo bisogno di creare la prima pagina (`index`) dove mostriamo *tutte le pizze* che prepariamo.

Una pizza avrà le seguenti informazioni :
- un `nome`
- una `descrizione`
- una `foto` (*url*)
- un `prezzo`

Creaimo l'`entity`, `repository` e `service` per gestire le CRUD delle pizze.

Implementiamo  quindi il controller con il metodo `index` che restituisce una `view` per mostrare l’*elenco delle pizze caricate dal database* (possiamo creare una tabella con `bootstrap` o una qualche grafica a nostro piacimento).

L’elenco **potrebbe essere vuoto**: in quel caso dobbiamo *mostrare un messaggio* che indichi all’utente che *non ci sono pizze* presenti nella nostra applicazione.

#### Correzione
[Repo](https://github.com/Guybrush3791/exp-java-4-spring-la-mia-pizzeria-crud)

### Day 2
Lo scopo di oggi è quello di mostrare i dettagli di una singola pizza.

Ogni pizza dell’elenco avrà quindi *un link* che se cliccato ci porterà a una pagina che mostrerà i *dettagli della pizza* scelta.
Dobbiamo quindi inviare l’`id` come parametro dell’`URL`, recuperarlo nel metodo del `controller`, caricare i dati della pizza ricercata e passarli come `model`.
La `view` a quel punto li mostrerà all’utente con la grafica che preferiamo.

Nella pagina con l’elenco delle pizze aggiungiamo un *campo di testo* che se compilato filtrerà le pizze (lato server) aventi come *titolo* quello inserito dall’utente.

#### Correzione
[Repo](https://github.com/Guybrush3791/exp-java-4-spring-la-mia-pizzeria-crud)

### Day 3
Abbiamo la lista delle pizze, abbiamo i dettagli delle pizze...perchè non realizzare la pagina per la *creazione di una nuova pizza*?

Aggiungiamo quindi tutto il codice necessario per *mostrare il form* per la *creazione di una nuova pizza* e per il salvataggio dei dati in tabella.

Nella `index` creiamo il bottone “*Crea nuova pizza*”.

Aggiungiamo inoltre una rotta che riceva il contenuto del `form` per poi mandarlo *a persistenza* nel *db* (NO VALIDAZIONI).

#### Correzione
[Repo](https://github.com/Guybrush3791/exp-java-4-spring-la-mia-pizzeria-crud)

### Day 4
Dobbiamo realizzare :
- pagina di *modifica di una pizza*
- *cancellazione di una pizza* cliccando un pulsante presente nella grafica di ogni singolo prodotto mostrato nella lista in `homepage`