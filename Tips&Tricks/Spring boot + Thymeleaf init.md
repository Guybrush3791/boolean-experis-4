Inizializzare progetto vuoto di tipo `Spring`
![[Pasted image 20230524143144.png]]

Definire poi il `name` del progetto, impostare il `Type` a `Maven`, definire il `Group` come *package principale*, il `Package` come *sotto-package del `Group`*
![[Pasted image 20230524143304.png]]

Non importare alcuna dipendenza e terminare con il tasto `Finish`.

All'interno del `pom.xml` assicurarsi di avere le seguenti dipendenze:
```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency> 
	<groupId>org.springframework.boot</groupId> 
	<artifactId>spring-boot-starter-thymeleaf</artifactId> 
</dependency>
```

All'interno del `Package` definire un sotto-package chiamato `controller` e creare almeno una classe di tipo `@Controller` all'interno:
```java
@Controller
@RequestMapping("/prova")
public class MyController {

	@GetMapping("/")
	@ResponseBody
	public String sayHello() {
		
		return "<h1>Prova!</h1>";
	}
	
	@GetMapping("/ciao")
	@ResponseBody
	public String sayHelloIta() {
		
		return "<h1>Ciao, Mondo!</h1>";
	}
	
	@GetMapping("/hola")
	public String sayHelloSp(Model model,
			@RequestParam(name = "name") String name) {
		
		model.addAttribute("name", name);
		
		return "index";
	}
	
	@GetMapping("/user/{id}")
	public String sayHelloToId(Model model,
			@PathVariable("id") int id) {
		
		model.addAttribute("name", "Guybrush " + id);
		
		return "index";
	}
}
```

All'interno della cartella `src/main/resources` creare una cartella chiamata *esattamente* `templates` e definire all'interno tutti i file `HTML` che sono necessari al `controller`
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1 th:text="'Hola ' + ${name} + '!'"></h1>
</body>
</html>
```