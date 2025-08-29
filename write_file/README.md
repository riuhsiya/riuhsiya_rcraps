## git --force
rm -rf .git && git init && git remote add origin git@github.com:riuhsiya/riuhsiya_rcraps.git && git config --global user.name "riuhsiya" && git config --global user.email "riuhsiya@gmail.com" && git checkout -b main && git add . && git commit -m "init" && git push origin main --force
```bash
rm -rf .git && git init && git remote add origin git@github.com:riuhsiya/riuhsiya_rcraps.git && git config --global user.name "riuhsiya" && git config --global user.email "riuhsiya@gmail.com" && git checkout -b main && git add . && git commit -m "init" && git push origin main --force
```

## git pull
rm -rf riuhsiya_rcraps && mkdir riuhsiya_rcraps && cd riuhsiya_rcraps && git init && git remote add origin git@github.com:riuhsiya/riuhsiya_rcraps.git && git config --global user.name "riuhsiya" && git config --global user.email "riuhsiya@gmail.com" && git pull origin main --allow-unrelated-histories && git branch -M main
```bash
rm -rf riuhsiya_rcraps && mkdir riuhsiya_rcraps && cd riuhsiya_rcraps && git init && git remote add origin git@github.com:riuhsiya/riuhsiya_rcraps.git && git config --global user.name "riuhsiya" && git config --global user.email "riuhsiya@gmail.com" && git pull origin main --allow-unrelated-histories && git branch -M main
```

## git --force-with-lease
git add . && git commit -m "up" --amend && git push -u origin main --force-with-lease
```bash
git add . && git commit -m "up" --amend && git push -u origin main --force-with-lease
```
```bash
git --no-pager diff README.md
git --no-pager diff --cached
git config --global core.pager ""
go mod init first_program
go test -v
```

## Golang
```golang
package main

import (
    "fmt"
    "os"
    "unicode/utf8"
)

func main() {
    // Define the byte sequences
    bytesArrays := [][]byte{
        {0xe3, 0x81, 0x94}, // ご (go)
        {0xe3, 0x81, 0xaf}, // は (ha)
        {0xe3, 0x81, 0xbf}, // み (mi)
        {0xe3, 0x81, 0x9a}, // ず (zu)
        {0xe3, 0x81, 0xb2}, // ひ (hi)
        {0xe3, 0x81, 0xa8}, // と (to)
        {0xe3, 0x81, 0x95}, // さ (sa)
        {0xe3, 0x81, 0x9b}, // せ (se)
        {0xe3, 0x81, 0xa7}, // で (de)
        {0xe3, 0x81, 0x8c}, // が (ga)
        {0xe3, 0x81, 0x91}, // け (ke)
        {0xe3, 0x81, 0x93}, // こ (ko)
        {0xe3, 0x81, 0xa9}, // ど (do)
        {0xe3, 0x81, 0x98}, // じ (ji)
        {0xe3, 0x81, 0xa3}, // っ (k)
        {0xe3, 0x81, 0x9d}, // そ (so)
    }

    labels := []string{
    " (go) 1", " (ha) 2", " (mi) 3", " (zu) 4", " (hi) 5",
    " (to) 6", " (sa) 7", " (se) 8", " (de) 9", " (ga) 10",
    " (ke) 11", " (ko) 12", " (do) 13", " (ji) 14", " (k) 15",
    " (so) 16",
    }

    var outputLines []string

    decoder := func(b []byte) string {
        if utf8.Valid(b) {
            return string(b)
        }
        return "Invalid UTF-8 sequence"
    }

    for i, byteArray := range bytesArrays {
        decodedStr := decoder(byteArray)
        line := fmt.Sprintf("%d%s: %s", i+1, labels[i], decodedStr)
        outputLines = append(outputLines, line)
    }

    outputText := ""
    for _, line := range outputLines {
        outputText += line + "\n"
    }

    // Print to console
    fmt.Println(outputText)

    // Save to output.txt
    err := os.WriteFile("output.txt", []byte(outputText), 0644)
    if err != nil {
        fmt.Println("Error writing to file:", err)
    } else {
        fmt.Println("Output saved to output.txt")
    }
}
```

## HTML
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
        [0xe3, 0x81, 0xa3], // っ (k)
        [0xe3, 0x81, 0x9d], // そ (so)
    ];

    const labels = [
        " (go) 1", " (ha) 2", " (mi) 3", " (zu) 4", " (hi) 5",
        " (to) 6", " (sa) 7", " (se) 8", " (de) 9", " (ga) 10",
        " (ke) 11", " (ko) 12", " (do) 13", " (ji) 14", " (k) 15",
        " (so) 16"
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
