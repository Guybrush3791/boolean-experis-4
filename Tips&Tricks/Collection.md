## Snippets
```java
List<String> myList = new ArrayList<>();
		
myList.add("val1");
myList.add("val2");
myList.add("val3");
myList.add("val4");
myList.add("val5");

System.out.println(myList);
System.out.println(myList.get(0)); // [0]

List<String> myList2 = new ArrayList<>();

myList2.add("prod1");
myList2.add("prod2");
myList2.add("prod3");
myList2.addAll(myList);

System.out.println(myList2);

myList.remove(0);
myList.remove("val5");

System.out.println(myList);

for (int x=0;x<myList.size();x++) {
	
	String val = myList.get(x);
	System.out.println(val);
}
for (String val : myList) {
	
	System.out.println(val);
}

Iterator<String> it = myList.iterator();
while(it.hasNext()) {
	
	String val = it.next();
	System.out.println(val);
}

Set<Integer> mySet = new HashSet<>();

mySet.add(10);
mySet.add(20);
mySet.add(1);
mySet.add(10);
mySet.add(10);
mySet.add(10);
mySet.add(10);

System.out.println(mySet);

Map<Character, Integer> myMap = new HashMap<>();

myMap.put('a', 1);
myMap.put('b', 5);
myMap.put('c', 10);
myMap.put('a', 7);

System.out.println(myMap);
System.out.println(myMap.get('c'));

myMap.replace('a', 70);
System.out.println(myMap);
myMap.replace('d', 70);
System.out.println(myMap);

for (Character c : myMap.keySet()) {
	
	int value = myMap.get(c);
	System.out.println(c + " --> " + value);
}

Map<Character, Integer> occCounter = new HashMap<>();
String str = "abc bcd aaa bcbcbc";
for (Character c : str.toLowerCase().toCharArray()) {

	if (c.equals(' ')) continue;
	
	if (occCounter.containsKey(c)) {
		
		occCounter.put(c, occCounter.get(c) + 1);
	} else {
		
		occCounter.put(c, 1);
	}
}

System.out.println(occCounter);

Iterator<Character> itC = occCounter.keySet().iterator();
while(itC.hasNext()) {
	
	Character c = itC.next();
	Integer v = occCounter.get(c);
	
	System.out.println(c + " --> " + v);
}
```

## Ordinamento Set (e chiavi di Map)
```java
Set<String> keys = wordCounter.keySet();
List<String> keyList = new ArrayList<>(keys);
Collections.sort(keyList);
for (String k : keyList) {
	
	Integer value = wordCounter.get(k);
	System.out.println(k + " --> " + value);
}
```