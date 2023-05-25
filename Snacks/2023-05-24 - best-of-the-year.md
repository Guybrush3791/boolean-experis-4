
## Repo
`best-of-the-year`

## Todo
### Day 1
#### Step 1
Creare un nuovo progetto **Spring Boot MVC + Thymeleaf**

Nel progetto aggiungere un `controller` che risponde alla *root dell’applicazione*, con un metodo che restituisce una `view` fatta con *Thymeleaf* in cui viene stampato un titolo: "Best of the year by …" (al posto dei puntini deve apparire il vostro `nome`, passato come attributo dal `controller` attraverso il `model`).

#### Step 2
Creare all’interno del controller due metodi privati:
- uno restituisce una `List<Movie>` - `getBestMovies()`
- l’altro restituisce una `List<Song>` - `getBestSongs()`

Creare le classi `Movie` e `Song` aventi almeno:
- `id`
- `titolo`

Aggiungere al `controller` altri *due metodi*, che rispondono agli `url`:
- `/movies`
- `/songs`

In ognuno di questi metodi aggiungere al `model` un attributo `stringa` con una *lista di titoli di migliori film o canzoni* (in base al metodo che stiamo implementando) separati da *virgole*.
Utilizzare i due metodi `getBest…` per recuperare i *film* e le *canzoni*.

Creare i rispettivi template `Thymeleaf`.

Creare due metodi:
- `/movies/{id}`
- `/songs/{id}`
che dato il parametro `id` passato tramite il `path`, mostri in pagina il titolo relativo al `film`/`canzone`.

Testare chiamando dal browser i diversi `url`.

### Day 2
#### Step 1
Includere `Bootstrap` e fare il refactoring del layout come da allegato, cercando di creare componenti riutilizzabili con i `fragments`.

Modificare i metodi che rispondono agli url:
- `/movies`
- `/songs`

Fare in modo che i `Model` restituiscano una *lista di oggetti* (`Movie` o `Song`) invece di una *stringa*.
Modificare anche le rispettive *view*.

Ogni elemento mostrato nella *lista* (`movie` o `song`) deve essere un `link` che punta alla rispettiva *pagina di dettaglio* (e anche in questo caso restituire il `Model` al posto della *stringa col titolo*).

Nella pagina `home` (quella che risponde alla *root dell’applicazione*) aggiungere *due link* che portano agli url `/movies` e `/songs`.

Nelle pagine con le liste *aggiungere un link* che riporta alla *home page*.

Testare navigando l’applicazione.

![[design-best-2021.drawio.png]]