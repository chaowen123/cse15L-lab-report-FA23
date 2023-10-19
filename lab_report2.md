## Lab Report2 
---

## Part 1
* Show the code for my StringServer.java
---
---
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;
class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int num = 0;
    List<String> strings = new ArrayList<>();
    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return " ";
        } else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    String addString = parameters[1]; 
                    if(!strings.contains(addString))
                    {
                        strings.add(parameters[1].replace("+"," "));
                    }
                    StringBuilder output = new StringBuilder();
                   for (int i = 0; i < strings.size(); i++) {
                        output.append((i + 1) + ". " + strings.get(i) + "\n");
                    }
                    return output.toString();
                    
                }
            }
            return "404 Not Found!";
        }
    }
}
class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }
        int port = Integer.parseInt(args[0]);
        Server.start(port, new Handler());
    }
}
```
---
---
* /add-messages?=hello
![image](cse15l_week1_report/hello.png)
```
1.Which methods in your code are called?
    -handleMessage(URI url) method:The handleRequest method in the Handler class is called
        when a request is made to any path other than "/".
    -getPath().contains("/add-message"). it does the code proceeds to the next part.
    -getQuery().split("=") splitting the query string using "=" as a delimiter
2.What are the relevant arguments to those methods, and the values of any relevant fields of the class?
    -url is the URI  representing the incoming HTTP request.
    -url.getPath() this will getting the path
    -url.getQuery() this will getting thr query after ? for example/add-messages?s=hello.
    -List<String> strings this will sotre the element of the part of the query that split by the"="
3.How do the values of any relevant fields of the class change from this specific request? If no value
got changed, explain why.
    -if I opne the page, the page is empty,untill I using/add-messages?s=hello, then the string list will
    sotre this query as string and disply to the page,and the num will store the number of how many query that we add
```


---
* /add-messages?=how are you
![image](cse15l_week1_report/how_are_you.png)
```
1.Which methods in your code are called?
    -I think is same as the first one /add-messages?s=hello
2.What are the relevant arguments to those methods, and the values of any relevant fields of the class?
    -It is the same as the first one, but the only difference is when we type "how are you "the space separates,
    and the argument of getQuery() will take as three argument1. how2.are3.you and only store the how in the string
    list; therefore, we need to separate by %20 for each spec when doing the curl in the git bash.
3.How do the values of any relevant fields of the class change from this specific request? If no values got changed,
  explain why.
    -the space change the values of getQuery() method, and this method will accept three arguments instead of one
    because the space between how are you will let the method getQuery（）think they are separated by the delimiter
    such the space in between.
```





## Part 2
1.The path to the private key for your SSH key for logging into ieng6 (on your computer or on the home directory of the 
lab computer)
![image](cse15l_week1_report/privte.png)
![image](cse15l_week1_report/pricate1.png)

2.The path to the public key for your SSH key for logging into ieng6 (within your account on ieng6)
![image](cse15l_week1_report/pub.png)

3.A terminal interaction where you log into ieng6 with your course-specific account without being asked for a password.
![image](cse15l_week1_report/3_1.png)
![image](cse15l_week1_report/3_2.png)






## Part 3
```
*In a couple of sentences, describe something you learned from lab in week 2 or 3 that you didn’t know before.
    -I have learned what are the differences between the private key and the public key. Wich, we could send our
    public key to the remote server because this key is encrypted. also, I have learned how to build my own server 
    by using the sample httpserver.HttpHandler. The code sets up a simple HTTP server that can accept with paths like 
    "/add-messages?s=message" to add messages to a list and return a numbered list of all messages. It keeps track of
    these messages in stringlist. If the path is "/", it returns an empty space.
```
