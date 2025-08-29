
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
<pre id="output"></pre>

<script>
document.getElementById('generateBtn').addEventListener('click', () => {
    // Array of byte arrays (representing Japanese characters)
    const bytesArrays = [
        [0xe3, 0x81, 0x94], // ご
        [0xe3, 0x81, 0xaf], // は
        [0xe3, 0x81, 0xbf], // み
        [0xe3, 0x81, 0x9a], // ず
        [0xe3, 0x81, 0xb2], // ひ
        [0xe3, 0x81, 0xa8], // と
        [0xe3, 0x81, 0x95], // さ
        [0xe3, 0x81, 0x9b], // せ
        [0xe3, 0x81, 0xa7], // で
        [0xe3, 0x81, 0x8c], // が
        [0xe3, 0x81, 0x91], // け
        [0xe3, 0x81, 0x93], // こ
        [0xe3, 0x81, 0xa9], // ど
        [0xe3, 0x81, 0x98], // じ
    ];

    const labels = [
        " (go) 1", " (ha) 2", " (mi) 3", " (zu) 4", " (hi) 5",
        " (to) 6", " (sa) 7", " (se) 8", " (de) 9", " (ga) 10",
        " (ke) 11", " (ko) 12", " (do) 13", " (ji) 14"
    ];

    let outputLines = [];

    for (let i = 0; i < bytesArrays.length; i++) {
        const byteArray = bytesArrays[i];
        // Convert byte array to Uint8Array
        const uint8Arr = new Uint8Array(byteArray);

        // Decode UTF-8 bytes to string
        const decoder = new TextDecoder('utf-8');
        let decodedStr;
        try {
            decodedStr = decoder.decode(uint8Arr);
        } catch (e) {
            decodedStr = "Invalid UTF-8 sequence";
        }

        // Prepare line
        const line = `${i + 1} ${labels[i]}: ${decodedStr}`;
        outputLines.push(line);
    }

    const outputText = outputLines.join('\n');

    // Display output in <pre> element
    document.getElementById('output').textContent = outputText;

    // Create a downloadable file
    const blob = new Blob([outputText], { type: 'text/plain' });
    const url = URL.createObjectURL(blob);

    const downloadLink = document.createElement('a');
    downloadLink.href = url;
    downloadLink.download = 'output.txt';
    document.body.appendChild(downloadLink);
    downloadLink.click();
    document.body.removeChild(downloadLink);
    URL.revokeObjectURL(url);
});
</script>
</body>
</html>
```
