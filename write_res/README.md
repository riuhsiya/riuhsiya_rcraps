
npm init -y
```bash
npm init -y
```

## res
```json
{
  "name": "write_req",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}

```

npm start
```bash
npm start
```

## title: write_res file: index.js
```javascript
const http = require('http');

const hostname = 'localhost';
const port = 3000;

const server = http.createServer((req, res) => {
  // Set header response
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');

  // Tanggapan terhadap permintaan
  res.end('Halo, ini server Node.js tanpa Express!');
});

// Jalankan server
server.listen(port, hostname, () => {
  console.log(`Server berjalan di http://${hostname}:${port}/`);
});

```

## title: write_res_2
```javascript
const http = require('http');
const fs = require('fs');
const path = require('path');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  // Jika request ke root, tampilkan index.html
  if (req.url === '/' || req.url === '/index.html') {
    const filePath = path.join(__dirname, 'index.html');
    fs.readFile(filePath, (err, data) => {
      if (err) {
        console.error('Internal Server Error: ', err);
        res.statusCode = 500;
        res.setHeader('Content-Type', 'text/plain; charset=UTF-8');
        res.end('Error loading page');
        return;
      }
      res.statusCode = 200;
      res.setHeader('Content-Type', 'text/html; charset=UTF-8');
      res.end(data);
    });
  } else {
    // Untuk URL lain, berikan 404
    res.statusCode = 404;
    res.setHeader('Content-Type', 'text/plain; charset=UTF-8');
    res.end('404 Not Found');
  }
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});

```

## title: write_res_3
```javascript
const http = require('http');
const fs = require('fs');
const path = require('path');

const hostname = '127.0.0.1';
const port = 3000;

// Fungsi helper untuk mengirim response dengan otomatis atur header
function sendResponse(res, statusCode, content, contentType = 'text/plain; charset=UTF-8') {
  res.writeHead(statusCode, { 'Content-Type': contentType });
  res.end(content);
}

const server = http.createServer((req, res) => {
  // Jika request ke root, tampilkan index.html
  if (req.url === '/' || req.url === '/index.html') {
    const filePath = path.join(__dirname, 'index.html');
    fs.readFile(filePath, 'utf8', (err, data) => {
      if (err) {
        console.error('Internal Server Error: ', err);
        sendResponse(res, 500, 'Error loading page');
        return;
      }
      // Kirim file dengan Content-Type html
      sendResponse(res, 200, data, 'text/html; charset=UTF-8');
    });
  } else {
    // Untuk URL lain, berikan 404
    sendResponse(res, 404, '404 Not Found');
  }
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});

```

title: write_res_3_trycatch
```javascript
const http = require('http');
const fs = require('fs').promises; // Menggunakan promises
const path = require('path');

const hostname = '127.0.0.1';
const port = 3000;

// Fungsi helper untuk mengirim response dengan otomatis atur header
function sendResponse(res, statusCode, content, contentType = 'text/plain; charset=UTF-8') {
  res.writeHead(statusCode, { 'Content-Type': contentType });
  res.end(content);
}

const server = http.createServer(async (req, res) => {
  try {
    if (req.url === '/' || req.url === '/index.html') {
      const filePath = path.join(__dirname, 'index.html');
      const data = await fs.readFile(filePath, 'utf8');
      // Kirim file dengan Content-Type html
      sendResponse(res, 200, data, 'text/html; charset=UTF-8');
    } else {
      // Untuk URL lain, berikan 404
      sendResponse(res, 404, '404 Not Found');
    }
  } catch (err) {
    console.error('Error:', err);
    sendResponse(res, 500, 'Error loading page');
  }
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```


## title: write_res_3_rust
$ cargo new write_res_3_rust

```rust
use std::net::{TcpListener, TcpStream};
use std::io::{Read, Write};
use std::fs;

fn handle_client(mut stream: TcpStream) {
    let mut buffer = [0; 1024];
    match stream.read(&mut buffer) {
        Ok(_) => {
            let request = String::from_utf8_lossy(&buffer);
            // Parse request line
            let request_line = request.lines().next().unwrap_or("");
            let parts: Vec<&str> = request_line.split_whitespace().collect();

            if parts.len() >= 2 {
                let method = parts[0];
                let path = parts[1];

                if method == "GET" && (path == "/" || path == "/index.html") {
                    // Membaca file index.html
                    match fs::read_to_string("index.html") {
                        Ok(contents) => {
                            let response = format!(
                                "HTTP/1.1 200 OK\r\nContent-Type: text/html; charset=UTF-8\r\nContent-Length: {}\r\n\r\n{}",
                                contents.len(),
                                contents
                            );
                            stream.write_all(response.as_bytes()).unwrap();
                        }
                        Err(_) => {
                            let response = "HTTP/1.1 500 Internal Server Error\r\n\r\nError loading page";
                            stream.write_all(response.as_bytes()).unwrap();
                        }
                    }
                } else {
                    // 404 Not Found
                    let response = "HTTP/1.1 404 Not Found\r\n\r\n404 Not Found";
                    stream.write_all(response.as_bytes()).unwrap();
                }
            }
        }
        Err(e) => eprintln!("Failed to read from socket: {}", e),
    }
}

fn main() {
    let listener = TcpListener::bind("127.0.0.1:3000").unwrap();
    println!("Server running at http://127.0.0.1:3000/");

    for stream in listener.incoming() {
        match stream {
            Ok(stream) => {
                handle_client(stream);
            }
            Err(e) => eprintln!("Connection failed: {}", e),
        }
    }
}
```

## title: write_res_req.url_ifelse
```javascript
if (req.url === '/' || req.url === '/index.html') {
    // halaman utama
} else if (req.url === '/about') {
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain; charset=UTF-8');
    res.end('About Page');
} else if (req.url === '/contact') {
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain; charset=UTF-8');
    res.end('Contact Page');
} else {
    // 404
}

```

## title: write_res_req.url_switch
```javascript
switch (req.url) {
    case '/':
    case '/index.html':
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain; charset=UTF-8');
        res.end('ROOT PAGE');
        break;
    case '/about':
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain; charset=UTF-8');
        res.end('About Page');
        break;
    case '/contact':
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain; charset=UTF-8');
        res.end('Contact Page');
        break;
    default:
        res.statusCode = 404;
        res.setHeader('Content-Type', 'text/plain; charset=UTF-8');
        res.end('404 Not Found');
}

```
## title: write_res
```javascript
const routes = {
    '/': () => {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain; charset=UTF-8');
        res.end('ROOT PAGE');
    },
    '/about': () => {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain; charset=UTF-8');
        res.end('About Page');
    },
    '/contact': () => {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain; charset=UTF-8');
        res.end('Contact Page');
    }
};

if (routes[req.url]) {
    routes[req.url]();
} else {
    res.statusCode = 404;
    res.setHeader('Content-Type', 'text/plain; charset=UTF-8');
    res.end('404 Not Found');
}

```

