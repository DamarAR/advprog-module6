# module 6
 
 ## Commit 1 Reflection notes
 To handle incoming HTTP requests from a web browser, I wrapped the TCP stream with a BufReader, allowing me to read the stream line by line using .lines(). Each line represents a different component of the HTTP request, such as the method, path, or headers.

To simplify processing, I transformed the iterator from Result<String> into String using .map(|line| line.unwrap()). Then, I applied .take_while(|line| !line.is_empty()) to stop reading at the first empty line, which signifies the boundary between the headers and the request body in an HTTP request.

By collecting these lines into a Vec<String>, I was able to obtain a structured, line-by-line view of how a browser communicates with the server. This approach gave me a deeper understanding of the low-level structure of HTTP requests.