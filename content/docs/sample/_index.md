This document outlines the usage rules and behavior of the `findNeedles()` method.  


#### Description

The `findNeedles()` method enables you to search for words in a text and count them. Up to five words per text can be checked with one method call.  


#### Parameters

The following parameters are passed to the method: 

* `haystack`. A string—plain text without punctuation marks—against which the words are compared.   
	Example: `"every door leads to this room where is this room's door"`.
* `needles`. An array of strings—the list of words to be searched for in the `haystack` string.   
	Example: `{"door","room","floor"}`.  



#### Behavior

As you invoke the method, it first counts the number of items in the `needles` array. If `needles` contains more than five items, it outputs `"Too many words!"` and terminates the method execution.

If `needles` contains five or less items, it proceeds to creating a variable that is later used for counting the total of each item's occurence in the text. Then it splits the `haystack` object into an array of distinct words and iterates through each word, comparing it to each item in the `needles` array. With each occurrence of the `needles` item in `haystack`, it increments the value for this item's index position by one, starting from 0.

Outputs each item from `needles` with their total count in `haystack`, separated by the `": "` string.

```java
public static void findNeedles(String haystack, String[] needles) {
	// If the needles list contains more than five items, outputs "Too many words!". 
	if (needles.length > 5) {
		System.err.println("Too many words!");
	} else {
		// Creates an array of integers and assigns index positions of `needles` items to it.
		int[] countArray = new int[needles.length];
		// Iterates through the array of `needles`. 
		for (int i = 0; i < needles.length; i++) {
			// Parses the `haystack` string through regex delimiters and splits it into words on word boundaries, quotation marks, apostrophes, tabs, newlines, form-feeds, and return characters. 
			String[] words = haystack.split("[ \"\'\t\n\b\f\r]", 0);
			// Loops through each item in the previously split haystack string.
			for (int j = 0; j < words.length; j++) {
				// Compares `words` to each item in the `needles` array and assigns the value of 0 to them.
				if (words[j].compareTo(needles[i]) == 0) {
			// With each occurrence of the `needles` item in `haystack`, increments the value of its index position by 1.
					countArray[i]++; 
				}
			}
		}
	// Outputs each item from the `needles` array with their total count.
		for (int j = 0; j < needles.length; j++) {
			System.out.println(needles[j] + ": " + countArray[j]);
		}
	}
}
```

<!-- ##### Example method call

```java
static String[] needles = {"door","room","floor"};

static String haystack = "every door leads to this room where is this room's door";

public static void main(String[] args) {
    findNeedles(haystack, needles );
}
``` -->  


#### Example response

A successful response contains the total count for each needle in the array:

```bash
door: 2
room: 2
floor: 0
```


__*Comments or questions to the person who wrote the code:*__

1. I would suggest adding punctuation delimiters to the regex (or refactoring the haystack splitting code in some other way), so that the method could also work for the `haystack` values that contain punctuation marks. 

1. I would also suggest extracting the `haystack` splitting code into a separate method:

	```java
	class Main {
	    public static void findNeedles(String haystack, String[]
	            needles) {
	        if (needles.length > 5) {
	            System.err.println("Too many words!");
	        } else {
	            int[] countArray = new int[needles.length];
	            for (int i = 0; i < needles.length; i++) {
	                String[] words = getStrings(haystack);
	                for (String word : words) {
	                    if (word.compareTo(needles[i]) == 0) {
	                        countArray[i]++;
	                    }
	                }
	            }
	            for (int j = 0; j < needles.length; j++) {
	                System.out.println(needles[j] + ": " + countArray[j]);
	            }
	        }
	    }
	    private static String[] getStrings(String haystack) {
	        return haystack.split("[ \"'\t\n\b\f\r]", 0);
	    }
	}
	```
	
	Please note that I've replaced the nested iterative loop with an enhanced for-loop in this snippet: it was Intellij IDEA's hint which I found reasonable for this case.


