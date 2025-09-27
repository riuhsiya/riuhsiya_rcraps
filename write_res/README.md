
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

