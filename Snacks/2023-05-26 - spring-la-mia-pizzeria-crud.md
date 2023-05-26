## Repo
`spring-la-mia-pizzeria-crud`

## Todo
Abbiamo bisogno di creare la prima pagina (`index`) dove mostriamo *tutte le pizze* che prepariamo.

Una pizza avrà le seguenti informazioni :
- un `nome`
- una `descrizione`
- una `foto` (*url*)
- un `prezzo`

Creaimo l'`entity`, `repository` e `service` per gestire le CRUD delle pizze.

Implementiamo  quindi il controller con il metodo `index` che restituisce una `view` per mostrare l’*elenco delle pizze caricate dal database* (possiamo creare una tabella con `bootstrap` o una qualche grafica a nostro piacimento).

L’elenco **potrebbe essere vuoto**: in quel caso dobbiamo *mostrare un messaggio* che indichi all’utente che *non ci sono pizze* presenti nella nostra applicazione.