## HTML_textContent
```html
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8" />
<title>Convert Japanese Bytes to Output</title>
</head>
<body>
<h1>Convert Japanese Byte Sequences to Output</h1>
<button id="generateBtn">Generate Output</button>
<div id="output"></div>

<script>
document.getElementById('generateBtn').addEventListener('click', () => {
    // Array of byte arrays (representing Japanese characters)
    const bytesArrays = [
        [0xe3, 0x81, 0x94], // ご (go)
        [0xe3, 0x81, 0xaf], // は (ha)
        [0xe3, 0x81, 0xbf], // み (mi)
        [0xe3, 0x81, 0x9a], // ず (zu)
        [0xe3, 0x81, 0xb2], // ひ (hi)
        [0xe3, 0x81, 0xa8], // と (to)
        [0xe3, 0x81, 0x95], // さ (sa)
        [0xe3, 0x81, 0x9b], // せ (se)
        [0xe3, 0x81, 0xa7], // で (de)
        [0xe3, 0x81, 0x8c], // が (ga)
        [0xe3, 0x81, 0x91], // け (ke)
        [0xe3, 0x81, 0x93], // こ (ko)
        [0xe3, 0x81, 0xa9], // ど (do)
        [0xe3, 0x81, 0x98], // じ (ji)
        [0xe3, 0x81, 0xa3], // っ (small tsu)
        [0xe3, 0x81, 0x9d], // そ (so)
    ];

    // Membuat string dari array byte menggunakan TextDecoder
    const decoder = new TextDecoder('utf-8');
    let resultText = '';

    bytesArrays.forEach(byteArray => {
        const uint8Array = new Uint8Array(byteArray);
        resultText += decoder.decode(uint8Array);
    });

    // Tampilkan hasilnya
    document.getElementById('output').textContent = resultText;
});
</script>
</body>
</html>
```
