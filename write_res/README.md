
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
