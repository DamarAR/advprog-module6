# module 6
 
 ## Commit 1 Reflection notes
 To handle incoming HTTP requests from a web browser, I wrapped the TCP stream with a BufReader, allowing me to read the stream line by line using .lines(). Each line represents a different component of the HTTP request, such as the method, path, or headers.

To simplify processing, I transformed the iterator from Result<String> into String using .map(|line| line.unwrap()). Then, I applied .take_while(|line| !line.is_empty()) to stop reading at the first empty line, which signifies the boundary between the headers and the request body in an HTTP request.

By collecting these lines into a Vec<String>, I was able to obtain a structured, line-by-line view of how a browser communicates with the server. This approach gave me a deeper understanding of the low-level structure of HTTP requests.


## Commit 2 Reflection Notes
 
 ![alt text](assets/images/img_commit2.png)
 
I learned how to serve an actual HTML file instead of just plain text by modifying the handle_connection method. Using fs::read_to_string(), I could easily load the contents of hello.html into memory. By including the appropriate headers along with the file’s content in the HTTP response, I ensured that browsers rendered the page correctly.

Additionally, I discovered the significance of the Content-Length header—omitting it can lead to rendering issues in some browsers. I also gained a deeper understanding of the required structure of an HTTP response, which must follow a specific format: starting with a status line (e.g., HTTP/1.1 200 OK), followed by headers, a blank line, and then the response body.