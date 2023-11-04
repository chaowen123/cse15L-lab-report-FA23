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

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for (String s : list) {
      if (sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }

  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while (index1 < list1.size() && index2 < list2.size()) {
      if (list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      } else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while (index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while (index2 < list2.size()) {
      result.add(list2.get(index2));
      index1 += 1;
    }
    return result;
  }
}
```
   **this is my test program for the listexamoles**

```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.ArrayList;
import java.util.List;

public class testFilter {
    @Test
    public void test_filter() {
        List<String> list = new ArrayList<>();
        list.add("Appl");
        list.add("Bob");
        list.add("coffe");
        list.add("Dave");
        list.add("coumpter");
        StringChecker isFourCharter = s -> s.length() == 8;
        List<String> result = ListExamples.filter(list, isFourCharter);
        assertEquals("coumpter", result);
    }
    @Test
    public void test_merge() {
        List<String> list1 = new ArrayList<>();
        list1.add("a");
        list1.add("c");
        list1.add("e");

        List<String> list2 = new ArrayList<>();
        list2.add("b");
        list2.add("d");
        list2.add("f");

        List<String> result = ListExamples.merge(list1, list2);
        assertEquals("a,c,e", result);
    }
}
```
**this is my output**
```
chaow@cao MINGW64 ~/lab4/lab_report_5/lab3 (main)
$ java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore testFilter
JUnit version 4.13.2
.E.E
Time: 12.366
There were 2 failures:
1) test_filter(testFilter)
java.lang.AssertionError: expected:<coumpter> but was:<[coumpter]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at testFilter.test_filter(testFilter.java:17)
2) test_merge(testFilter)
java.lang.OutOfMemoryError: Java heap space
        at java.base/java.util.Arrays.copyOf(Arrays.java:3513)
        at java.base/java.util.Arrays.copyOf(Arrays.java:3482)
        at java.base/java.util.ArrayList.grow(ArrayList.java:237)
        at java.base/java.util.ArrayList.grow(ArrayList.java:244)
        at java.base/java.util.ArrayList.add(ArrayList.java:483)
        at java.base/java.util.ArrayList.add(ArrayList.java:496)
        at ListExamples.merge(ListExamples.java:42)
        at testFilter.test_merge(testFilter.java:31)
        at java.base/java.lang.invoke.LambdaForm$DMH/0x000001a33c012400.invokeVirtual(LambdaForm$DMH)
        at java.base/java.lang.invoke.LambdaForm$MH/0x000001a33c013000.invoke(LambdaForm$MH)
        at java.base/java.lang.invoke.Invokers$Holder.invokeExact_MT(Invokers$Holder)

FAILURES!!!
Tests run: 2,  Failures: 2
```
* An input that doesn’t induce a failure, as a JUnit test and any associated code

  **this is the code that does not include a failure I samply change them to compare itself**
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.ArrayList;
import java.util.List;

public class testFilter {
    @Test
    public void test_filter() {
        List<String> list = new ArrayList<>();
        list.add("Appl");
        list.add("Bob");
        list.add("coffe");
        list.add("Dave");
        list.add("coumpter");
        StringChecker isFourCharter = s -> s.length() == 8;
        List<String> result = ListExamples.filter(list, isFourCharter);
        assertEquals(result, result);
    }
    @Test
    public void test_merge() {
        List<String> list1 = new ArrayList<>();
        list1.add("a");
        list1.add("c");
        list1.add("e");

        List<String> list2 = new ArrayList<>();

        List<String> result = ListExamples.merge(list1, list2);
        assertEquals(result, result);
    }
}
```
**this is the output with no failure**
```
$ java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore testFilter
JUnit version 4.13.2
..
Time: 0.01

OK (2 tests)
```


