## Init progetto
Dopo aver creato un progetto di tipo **SpringBoot** aggiungiamo le dipendenze necessario per la comunicazione con il db nel `pom.xml`:
```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
	<version>8.0.33</version>
</dependency>
```

Definire inoltre le variabili essenziali all'`Hibernate` per collegarsi con il db:
```
spring.datasource.url=jdbc:mysql://localhost:3306/db-crud
spring.datasource.username=root
spring.datasource.password=code

spring.jpa.hibernate.ddl-auto=create
```

## Creazione entita'/tabella
Per creare una tabella all'interno del db utilizzando `Hibernate` e' sufficiente andare a creare l'`Entity` corrispondente con le notazioni necessarie per definirla come entita' di db:
```java
@Entity
public class Book {
	
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private int id;

	private String title;
	private String author;
	private String publisher;
	private int year;
	
	@Column(length = 13, unique = true)
	@NonNull
	private String isbn;
	private int copies;
	
	public Book() { }
	public Book(String title, String author, String publisher, int year, String isbn, int copies) {
		
		setTitle(title);
		setAuthor(author);
		setPublisher(publisher);
		setYear(year);
		setIsbn(isbn);
		setCopies(copies);
	}
	
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getTitle() {
		return title;
	}
	public void setTitle(String title) {
		this.title = title;
	}
	public String getAuthor() {
		return author;
	}
	public void setAuthor(String author) {
		this.author = author;
	}
	public String getPublisher() {
		return publisher;
	}
	public void setPublisher(String publisher) {
		this.publisher = publisher;
	}
	public int getYear() {
		return year;
	}
	public void setYear(int year) {
		this.year = year;
	}
	public String getIsbn() {
		return isbn;
	}
	public void setIsbn(String isbn) {
		this.isbn = isbn;
	}
	public int getCopies() {
		return copies;
	}
	public void setCopies(int copies) {
		this.copies = copies;
	}
	
	@Override
	public String toString() {
		
		return "[" + getId() + "] " + getTitle() + " - " + getAuthor() + " (" + getPublisher() + ")"
				+ "\nyear: " + getYear() 
				+ "\ncopies: " + getCopies()
				+ "\nisbn: " + getIsbn();
	}
}
```

Avviando il progetto verra' creata la tabella corrispondente (vuota) che e' possibile andare a vedere all'interno del gestore db (*DBEaver*)
![[Pasted image 20230526120844.png]]

## Interfacciarsi alla tabella
Per permettere ai controller di gestire la tabella appena salvata in db e' necessario creare un `Repository` (interfaccia) e un `Service` (classe):

### Repository
Il repository altro non e' che un'interfaccia che estende la `JpaRepository` di `Hibernate`:
```java
@Repository
public interface BookRepo extends JpaRepository<Book, Integer> {

}
```

### Service
Il service e' il canale di comunicazione tra il mondo esterno e la tabella appena creata. All'interno troviamo quindi tutti i metodi necessari per tutte le operazioni richieste dal sw (`CRUD` operation):
```java
@Service
public class BookService {

	@Autowired
	private BookRepo bookRepo;
	
	public List<Book> findAll() {
		
		return bookRepo.findAll();
	}
	public Book save(Book book) {
		
		return bookRepo.save(book);
	}
	public Optional<Book> findById(int id) {
		
		return bookRepo.findById(id);
	}
}
```

## Testing delle tabelle
E' ora possibile gestire i dati all'interno della tabella dal mondo esterno attraverso i metodi forniti dal `Service` appena creato. Per testare il corretto funzionamento di tutti il codice visto fino ad ora, e' possibile utilizzare l'implementazione dell'interfaccia `CommandLineRunner` nella classe principale (la classe che contiene il `main`) ed di conseguenza il metodo `run` che verra' eseguito ad ogni avvio del progetto:
```java
@SpringBootApplication
public class CrudTest1Application implements CommandLineRunner {

	@Autowired
	private BookService bookService;

	// ...

	@Override
	public void run(String... args) throws Exception {
		
		Book b = new Book("mio libro 1", "io", "sempre io", 2023, "1234567890123", 1943893);
		System.out.println(b);
		
		bookService.save(b);
		
		List<Book> books = bookService.findAll();
		System.out.println(books);
		
		Optional<Book> optBook = bookService.findById(1);
		
		if (optBook.isPresent()) {
			
			Book dbBook = optBook.get();
			
			System.out.println("Book con id 1");
			System.out.println("--------------");
			System.out.println(dbBook);
		} else 
			System.out.println("Book con id 1 non trovato :-(");
	}
}
```

## CRUD: index + show
Per creare delle pagine web che permettono di interagire con i dati presenti in tabella (operazioni di sola lettura), generare un `Controller` contenente le 2 rotte necessarie per la `index` e la `show`. Queste due rotte, leggono i dati dal db attraverso i metodi forniti dal `Service` che viene importato attraverso l'`autowired`, per poi passarli ai fogli `HTML` con `Thymeleaf` che si occuperanno della rappresentazione degli oggetti.

### Controller
```java
@Controller
public class BookController {

	@Autowired
	private BookService bookService;
	
	@GetMapping("/")
	public String getHome(Model model) {
		
		List<Book> books = bookService.findAll();
		
		model.addAttribute("books", books);
		
		return "books";
	}
	
	@GetMapping("/books/{id}")
	public String getBook(
			Model model,
			@PathVariable("id") int id
	) {
		
		Optional<Book> optBook = bookService.findById(id);
		Book book = optBook.get();
		
		model.addAttribute("book", book);
		
		return "book";
	}
}
```

### Pagine HTML/CSS/JS
#### `books.html`
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1>Books</h1>
	<ul>
		<li
			th:each="book : ${books}"
			th:object="${book}"
		>
			<a th:href="@{/books/{id} (id=*{id})}">
				[[ *{title} ]]
			</a>
		</li>
	</ul>
</body>
</html>
```

#### `book.html`
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body th:object="${book}">
	<h1>Book</h1>
	<h3>[[ *{title} ]] - [[ *{author} ]] ([[ *{publisher} ]])</h3>
	<h4>Year: [[ *{year} ]]</h4>
	<h4>ISBN: [[ *{isbn} ]]</h4>
	<h4>Copies: [[ *{copies} ]]</h4>
</body>
</html>
```