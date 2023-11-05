## Lab Report 3

**Part I**
* A failure-inducing input for the buggy program, as a JUnit test and any associated code

  **this the my buggy program " listexamples"**

```
import java.util.ArrayList;
import java.util.List;

interface StringChecker {
  boolean checkString(String s);
}

class ListExamples {


  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for (String s : list) {
      if (sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }
```

  **this is my test program for the listexamoles**

```
public class testFilter {
       @Test
    public void test_filter() {
        List<String> sampleList = Arrays.asList("apple", "pie", "banan", "kiwii", "grape");
        StringChecker isFourCharter = s -> s.length() == 5;
        List<String> filteredList = ListExamples.filter(sampleList, isFourCharter);
        List<String> expect = Arrays.asList("applee", "banana", "kiwiii","grapee");
        assertEquals(expect, filteredList);
    }
```
---
* An input that doesn’t induce a failure, as a JUnit test and any associated code

```
     @Test
    public void test_filter() {
        List<String> sampleList = Arrays.asList("apple", "pie", "banan", "kiwii", "grape");
        StringChecker isFourCharter = s -> s.length() == 5;
        List<String> filteredList = ListExamples.filter(sampleList, isFourCharter);
        List<String> expect = Arrays.asList("apple", "banan", "kiwii","grape");
        assertEquals(expect, filteredList);
    }
```

---
* The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)

  **this is my output that include a failure**

  ![image](cse15l_week1_report/output33.png)




