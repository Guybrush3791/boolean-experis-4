# Back-end
## Dependencies
`pom.xml`
```xml
<!-- SECURITY -->
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

## Configuration
Il file di configurazione della *security* in `SpringBoot` e' quello contenente l'`encoder` della *password*  e il `SecurityFilterChain`
```java
@Configuration
@EnableMethodSecurity
public class AuthConfProd implements WebMvcConfigurer {

	@Autowired
	private String baseApi;
	
	@Bean
	public static PasswordEncoder passwordEncoder() {
		
		return new BCryptPasswordEncoder();
	}
	
	@Bean
	public SecurityFilterChain getSecurityFilterChain(
			HttpSecurity http) throws Exception {
		
		return 
			http.cors().and() // vedi getCorsSettings()
				.csrf(c -> c // va gestito attraverso il token
					.csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse())
					.csrfTokenRequestHandler(new CsrfTokenRequestAttributeHandler())
				).authorizeHttpRequests(
					// ROTTE
				)
			    .formLogin(f -> f.disable()) // abilitare per monolitico
			    .logout(l -> l.disable()) // abilitare per monolitico
		.build();
	}
	
	@Bean
    public CorsFilter getCorsSettings() {
		
        final UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        final CorsConfiguration config = new CorsConfiguration();
        
        // OPTIONS
        config.setAllowCredentials(true);
        // necessario per login
        
        // ORIGINS
        config.addAllowedOrigin("http://localhost:9000"); 
        // settare porta corretta del proprio front-end (vuejs)
        
        // HEADERS
        config.addAllowedHeader("Content-Type");
        config.addAllowedHeader("Authorization");
        config.addAllowedHeader("Accept");
        config.addAllowedHeader("X-XSRF-TOKEN");
        // eventuali altri headers
        
        // METHODS
        config.addAllowedMethod("GET");
        config.addAllowedMethod("POST");
        // eventuali altri metodi
        
        // SET CONFIG ON PATHS
        source.registerCorsConfiguration("/**", config);
        
        return new CorsFilter(source);
    }
}
```
## Controller
Controller dedicata alla login via `webAPI`
```java
@RestController
@RequestMapping("/api/v1/open/auth")
public class AuthApiController {

	@Autowired
	private UserServ userServ;
	
	@PostMapping("/login")
	public ResponseEntity<UserDto> login(
			@RequestBody LoginDto loginDto, 
			HttpServletRequest request
		) throws Exception {
		
		try {
			
		    request.login(loginDto.getUsername(), loginDto.getPassword());
		} catch (ServletException e) {
			
			return new ResponseEntity<>(null, HttpStatus.BAD_GATEWAY);
		}

		// opzionalmente e' possibile ritornare come risposta positiva lo user che e' riuscito correttamente a collegarsi (utile ad evitare un'ulteriore chiamata per ottenere queste informazioni)
		final Optional<User> user = userServ.findByUsername(loginDto.getUsername());
		if (user.isEmpty()) return new ResponseEntity<>(null, HttpStatus.NOT_FOUND); 
		
		return new ResponseEntity<>(
			new UserDto(user.get()), 
			HttpStatus.OK
		);
	}
	
	@PostMapping("/logout")
	public ResponseEntity<String> login(HttpServletRequest request) {
		
		try {
			
			request.logout();
		} catch (ServletException e) {
			
			return new ResponseEntity<>("Error: " + e.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
		}
		
		return new ResponseEntity<>("Signed out", HttpStatus.OK);
	}

	// per inizializzare correttamente la comunicazione e' necessario ottenere prima di tutto un TOKEN
	@GetMapping("/csrf")
	public String getCsrfToken(HttpServletRequest request) { 

		CsrfToken token = (CsrfToken) request.getAttribute(CsrfToken.class.getName());
	    return token.getToken();
	}
}
```

# Front-end
All'interno del progetto `VueJS` e' sufficiente gestire le chiamate `axios` creando un `API` dedicata al nostro `back-end` impostando `indirizzo`, `credenziali` e `headers`.
Chiamando l'indirizzo di `login` e passando `username` e `password` e' quindi possibile *loggarsi* e *ottenere le informazioni riguardanti lo user collegato* (vedi [[#Controller]]).
```js

const api = axios.create({
  baseURL: process.env.API + "api/v1/",
  withCredentials: true,
  headers: {
    "Content-Type": "application/json",
  },
});

const LoginManager = {
  isLoggedIn: () => LocalStorage.has("user"),
  login: async (loginData) => {
    let user;

    try {
      await api.get("open/auth/csrf");
      user = (await api.post("open/auth/login", loginData)).data.user;
    } catch (e) {
      return false;
    }

    LocalStorage.set("user", user);

    return user;
  },
  logout: async () => {
    if (!LoginManager.isLoggedIn()) return true;

    try {
      const res = await api.post("open/auth/logout");
    } catch (e) {
      return false;
    }

    LocalStorage.remove("user");

    return true;
  },
  getMe: () =>
    LoginManager.isLoggedIn() ? LocalStorage.getItem("user") : null,
};
```