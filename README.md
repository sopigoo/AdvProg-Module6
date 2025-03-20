# AdvProg-Module6
Name : Siti Shofi Nadhifa <br>
NPM : 2306152172 <br>
Class : AdPro B

## Commit 1 Reflection notes
The method handle_connection is used to handle incoming TCP connections and parse HTTP requests in Rust. Based on my searching, in this function the `TcpStream` is first wrapped with a `BufReader` to enable efficient, buffered reading from the stream. Then, `buf_reader.lines()` creates an iterator over each line of the incoming request, where each line is a `Result<String, Error>.` Using `.map(|result| result.unwrap())`, the lines are unwrapped to extract the strings, assuming the request is well-formed. The call to `.take_while(|line| !line.is_empty())` ensures that only the request line and headers are collected, stopping at the first empty line, which in HTTP marks the end of the header section. These lines are gathered into a vector called `http_request`, which is printed in a nicely formatted way using `println!("Request: {:#?}", http_request);` to assist with debugging and inspection. This approach gave me a clearer understanding of how raw HTTP data is processed and improved my grasp of stream handling and I/O operations in Rust.
