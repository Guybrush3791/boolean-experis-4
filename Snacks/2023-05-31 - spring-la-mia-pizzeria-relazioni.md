## Repo
`spring-la-mia-pizzeria-relazioni`

## Live
Vedi [[2023-05-31 - crud books relazioni|Live]]

## Todo
### Day 1
> [!attention] IMPORTANTE
> Ricordatevi di sganciare la vostra vecchia repository e di crearne una nuova per questo esercizio, che prosegue il lavoro della pizzeria, dove lo avevate lasciato.

Nuova importante funzionalità : *le offerte speciali!*

In alcuni momenti potremmo voler vendere le nostre pizze *a un prezzo scontato*.

Dobbiamo quindi predisporre tutto il codice necessario per poter *collegare un’offerta speciale a una pizza* (in una *relazione 1 a molti*, cioè un’offerta speciale può essere collegata a una sola pizza, e una pizza può essere collegata a più offerte speciali).

L’*offerta speciale* e' caratterizzata da:
- `data di inizio`
- `data di fine`
- `titolo`
- `percentuale di sconto`

La *pagina di dettaglio della singola pizza* mostrerà *l’elenco delle offerte collegate* e avrà un bottone “*Crea nuova offerta speciale*” per aggiungerne una nuova.

Accanto ad ogni offerta speciale è previsto *un bottone* che mi porterà a una *pagina per modificarla*.

#### Bonus
- stampare per ogni offerta di ogni pizza, il *prezzo scontato*
- aggiungere le validazioni anche alla nuova entita' *offerta speciale*

#### Correzione
[Repo](https://github.com/Guybrush3791/exp-java-4-spring-la-mia-pizzeria-crud)

### Day 2
Nuovo pezzettino per la nostra pizzeria: *gli ingredienti*!

Ogni `pizza` può avere più `ingredienti`, e ogni ` ` può essere collegato a più `pizze`.

Prevediamo quindi una pagina per mostrare l*’elenco di tutti gli ingredienti* che utilizziamo nella nostra pizzeria che permetta anche di *crearne di nuovi* (e di *cancellarli*).

Nella pagina di *creazione* (e *modifica*) della singola pizza dobbiamo dare la *possibilità di collegare uno o più ingredienti*.