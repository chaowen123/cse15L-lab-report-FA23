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
