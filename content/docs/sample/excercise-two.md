
```java
// take values for haystack and needles and return a result  
public static void findNeedles(String haystack, String[] needles) {
	// comment
	if (needles.length > 5) {
		System.err.println("Too many words!");
	} else {
		int[] countArray = new int[needles.length];
		for (int i = 0; i < needles.length; i++) {
			String[] words = haystack.split("[ \"\'\t\n\b\f\r]", 0);
			for (int j = 0; j < words.length; j++) {
				if (words[j].compareTo(needles[i]) == 0) {
					countArray[i]++;
				}
			}
		}
		for (int j = 0; j < needles.length; j++) {
			System.out.println(needles[j] + ": " + countArray[j]);
		}
	}
}
```

Example method call:
