# AdvProg-Module6
Name : Siti Shofi Nadhifa <br>
NPM : 2306152172 <br>
Class : AdPro B

## Commit 1 Reflection notes
The method handle_connection is used to handle incoming TCP connections and parse HTTP requests in Rust. Based on my searching, in this function the `TcpStream` is first wrapped with a `BufReader` to enable efficient, buffered reading from the stream. Then, `buf_reader.lines()` creates an iterator over each line of the incoming request, where each line is a `Result<String, Error>.` Using `.map(|result| result.unwrap())`, the lines are unwrapped to extract the strings, assuming the request is well-formed. The call to `.take_while(|line| !line.is_empty())` ensures that only the request line and headers are collected, stopping at the first empty line, which in HTTP marks the end of the header section. These lines are gathered into a vector called `http_request`, which is printed in a nicely formatted way using `println!("Request: {:#?}", http_request);` to assist with debugging and inspection. This approach gave me a clearer understanding of how raw HTTP data is processed and improved my grasp of stream handling and I/O operations in Rust.

## Commit 2 Reflection notes
![Commit 2 screen capture](/assets/images/commit2.png)
In this part, I learned how to serve an actual HTML file in response to a browser’s HTTP request using Rust. The updated `handle_connection` function not only reads and parses the incoming request but also constructs a valid HTTP response. After reading the request lines with a buffered reader, a status line `"HTTP/1.1 200 OK"` is defined to indicate a successful response. Then, the contents of `hello.html` is loaded using `fs::read_to_string`, and calculated its length to correctly set the `Content-Length` header, which informs the browser how much data to expect. Finally, the status line, headers, and HTML content were combined into a single response string using `format!`, and sent back through the TCP stream with `stream.write_all`. This tutorial gave me a clearer understanding of how HTTP responses are constructed and how static content can be delivered through a network connection in Rust, which deepened my appreciation for the underlying mechanics of web server communication.

## Commit 3 Reflection notes
![Commit 3 screen capture](/assets/images/commit3.png)
In this milestone, I learned how to parse and validate HTTP requests to enable the server to respond differently based on the request path. The function `handle_connection` now checks the first line of the HTTP request (the request line) and compares it to `GET / HTTP/1.1`. If it matches, the server responds with `hello.html`. Otherwise, it returns a 404 status along with `404.html`. This process introduced the concept of conditional routing based on request paths. I realized the importance of splitting the logic between response types for maintainability and readability, leading me to refactor the code for clarity. Refactoring was needed because previously, the server responded with the same page regardless of the request, which is not realistic. The new version splits request handling into two outcomes (200 OK and 404 Not Found), improving the server's ability to communicate meaningful responses to the client.

## Commit 4 Reflection notes
![Commit 4 screen capture](/assets/images/commit4.png)
In this milestone, the server code is modified to simulate a slow response by introducing a 10-second delay when the `/sleep` route is accessed, using `thread::sleep`. When testing with two browser tabs—one accessing `/sleep` and the other accessing `/`, I observed that the second request had to wait until the first one completed. This happened because the server runs on a single thread, so it processes one request at a time. As a result, any slow request blocks all others, leading to poor performance when multiple users are accessing the server simultaneously. This experiment helped me understand the limitation of single-threaded servers and the importance of using concurrency or asynchronous approaches to handle multiple requests efficiently.
