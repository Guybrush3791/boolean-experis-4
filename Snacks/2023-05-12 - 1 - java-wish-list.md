## Repo
`java-wish-list`

## Package
`org.lessons.java.christmas`

## Todo
Creare una classe `Main` con metodo `main`, in cui implementare il seguente programma:
creare un `ArrayList` dove salvare *la lista dei desideri*
continuare a chiedere all’utente di inserire *un nuovo desiderio* nella lista, fino a che l’utente sceglie di fermarsi.

Ad ogni iterazione mostrare la lunghezza della lista e chiedere all’utente se vuole continuare.

Ad ogni iterazione aggiungere il desiderio alla lista.

Al termine dell’inserimento stampare a video la lista di desideri.

## Soluzione
```java
Scanner sc = new Scanner(System.in);
List<String> whishList = new ArrayList<>();

while (true) {
	
	System.out.println("1 - Inserire desiderio");
	System.out.println("2 - Uscire e stampare lista");
	
	int userValue = sc.nextInt();
	
	if (userValue < 1 || userValue > 2) {
		
		System.out.println("Scelta non valida, riprovare");
		continue;
	}
	if (userValue == 2) break;
	
	sc.nextLine();			
	System.out.print("Testo desiderio: ");
	String whish = sc.nextLine();
	
	whishList.add(whish);
	
	System.out.println("Numero desideri inseriti: " + whishList.size());
}

System.out.println("Questi sono i tuoi desideri:");
System.out.println(whishList);
System.out.println("------------------------------");
System.out.println("Arrivederci");
```