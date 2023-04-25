# Lab Report 2 - Servers and Bugs
In this Lab Report, you will learn about the specifics of servers such as creating and using a serving. You will also learn about bugs, how to identify them, the different parts of an error message, and how to fix them.
***

## Part One: Creating and Using a Server

Below is code for creating a server that concatanates a string using the `\n` notation to the previous string requests. For example, if the first string request had the string `Hello` then `Hello` would be printed on to the server. Now if another string request came in with the string `Hi` then both `Hello` and `Hi` would be printed on to the server.

```Java
  class Handler implements URLHandler {
      // The one bit of state on the server: a number that will be manipulated by
      // various requests

      String strs = "";

      public String handleRequest(URI url) {
          if (url.getPath().equals("/")) {
              return strs;
          } 
          else if (url.getPath().contains("/add-message")) {
              System.out.println("Path: " + url.getPath());
              String[] parameters = url.getQuery().split("=");
              if (parameters[0].equals("s")) {
                  strs += parameters[1] + "\n";
                  return strs;
              }
          } 
          return "404 Not Found!";
      }
  }
```
My code takes in a url of type `URI` that gets passed through an if-else-if statement and acts accordingly depending on the type of path and query given in the url. If given a valid path and query, the code should return the string requests; however, in the case of an invalid path and query then the server will return a `404 Not Found` error message. Here's how the server will look when compiling and running this code:

![Image](ServerCreated.png)

**Note:** The terminal shows that the server is created so now we can click on the given link and start sending string requests by modifying the url's path and query.

### Here is what the page should look like once you open the server:
![Image](NoRequest.png)

**Note:** You can see in the search bar that the link doesn't contain any path or query other than the `/` at the end, which is the reason why the page is currently blank without words.

Now let's try adding `add-message?s=Hello` to the end of the the url:

### Here is the server after one string request has been sent through:
![Image](FirstRequest.png)

1. The method called in the code when running all of this is the `public String handleRequest(URI url)`.
2. After running this method, the url of type `URI` gets passed as a parameter. This parameter is first used in the if-statement to check if the server has any path other than just `/`. If it doesn't, then an empty string gets printed out through the `strs` variable. If it does, then it checks if the path is equal to `/add-message` and from there it splits the given query from the `=` and returns the element of index 1 from that list. However, if the path doesn't match, then a `404 Not Found` error message gets printed out on to the server.
3. The only value that actually changes during this entire process would be the `strs` variable which stores the given strings from the requests and is then used to print them on to the server page. By using a variable like `strs`, we are able to properly store all the given strings and properly print them when necessary. In this case, because this is the first request, all the gets printed on to the server is `Hello`.


Now let's try typing `add-message?s=How are you?` instead to the end of the the url:

### Here is the server after a second string request has been sent through:
![Image](SecondRequest.png)

1. The method called in the code when running all of this is the `public String handleRequest(URI url)`.
2. After running this method, the url of type `URI` gets passed as a parameter. This parameter is first used in the if-statement to check if the server has any path other than just `/`. If it doesn't, then an empty string gets printed out through the `strs` variable. If it does, then it checks if the path is equal to `/add-message` and from there it splits the given query from the `=` and returns the element of index 1 from that list. However, if the path doesn't match, then a `404 Not Found` error message gets printed out on to the server.
3. The only value that actually changes during this entire process would be the `strs` variable which stores the given strings from the requests and is then used to print them on to the server page. By using a variable like `strs`, we are able to properly store all the given strings and properly print them when necessary. In this case, what gets printed on to the server is `Hello` and `How are you?`.
