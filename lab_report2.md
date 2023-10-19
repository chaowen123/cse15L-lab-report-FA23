## Lab Report2 
---
## Part 1
* Show the code for my StringServer.java 
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
