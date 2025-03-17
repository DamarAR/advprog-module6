# module 6
 
 ## Commit 1 Reflection notes
 To handle incoming HTTP requests from a web browser, I wrapped the TCP stream with a BufReader, allowing me to read the stream line by line using .lines(). Each line represents a different component of the HTTP request, such as the method, path, or headers.

To simplify processing, I transformed the iterator from Result<String> into String using .map(|line| line.unwrap()). Then, I applied .take_while(|line| !line.is_empty()) to stop reading at the first empty line, which signifies the boundary between the headers and the request body in an HTTP request.

By collecting these lines into a Vec<String>, I was able to obtain a structured, line-by-line view of how a browser communicates with the server. This approach gave me a deeper understanding of the low-level structure of HTTP requests.


## Commit 2 Reflection Notes
 
![alt text](assets/images/img_commit2.png)
 
I learned how to serve an actual HTML file instead of just plain text by modifying the handle_connection method. Using fs::read_to_string(), I could easily load the contents of hello.html into memory. By including the appropriate headers along with the file’s content in the HTTP response, I ensured that browsers rendered the page correctly.

Additionally, I discovered the significance of the Content-Length header—omitting it can lead to rendering issues in some browsers. I also gained a deeper understanding of the required structure of an HTTP response, which must follow a specific format: starting with a status line (e.g., HTTP/1.1 200 OK), followed by headers, a blank line, and then the response body.


## Commit 3 Reflection Notes

![alt text](assets/images/img_commit3.png)

I modified the handle_connection method to return different responses based on the requested path. By analyzing the request line from the browser, the server determines which page to serve: if the request is for /, it responds with a 200 OK status and serves hello.html; for any other path (such as /bad), it returns a 404 NOT FOUND status along with a custom 404.html file.

This implementation treats / as the only valid request path. If the request line matches GET / HTTP/1.1, the server delivers hello.html with a success status; otherwise, it responds with an error status and displays an error page.

Moreover, the tutorial recommends refactoring the code to enhance clarity and maintainability. By organizing the logic into smaller, reusable components instead of a single function, the code becomes more readable and scalable for future improvements.