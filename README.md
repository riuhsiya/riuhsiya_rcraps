## clone-pull
rm -rf riuhsiya_rcraps && mkdir riuhsiya_rcraps && cd riuhsiya_rcraps && git init && git remote add origin git@github.com:riuhsiya/riuhsiya_rcraps.git && git config --global user.name "riuhsiya" && git config --global user.email "riuhsiya@gmail.com" && git pull origin main --allow-unrelated-histories && git checkout -b main
```bash
rm -rf riuhsiya_rcraps && mkdir riuhsiya_rcraps && cd riuhsiya_rcraps && git init && git remote add origin git@github.com:riuhsiya/riuhsiya_rcraps.git && git config --global user.name "riuhsiya" && git config --global user.email "riuhsiya@gmail.com" && git pull origin main --allow-unrelated-histories && git checkout -b main
```

## push-force
rm -rf .git && git init && git remote add origin git@github.com:riuhsiya/riuhsiya_rcraps.git && git config --global user.name "riuhsiya" && git config --global user.email "riuhsiya@gmail.com" && git checkout -b main && git add . && git commit -m "init" && git push origin main --force
```bash
rm -rf .git && git init && git remote add origin git@github.com:riuhsiya/riuhsiya_rcraps.git && git config --global user.name "riuhsiya" && git config --global user.email "riuhsiya@gmail.com" && git checkout -b main && git add . && git commit -m "init" && git push origin main --force
```

## push-lease
git add . && git commit -m "up" --amend && git push -u origin main --force-with-lease
```bash
git add . && git commit -m "up" --amend && git push -u origin main --force-with-lease
```

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
    // Alokasi memori secara dinamis untuk byte array
    unsigned char *x = (unsigned char *) malloc(3 * sizeof(unsigned char));
    if (x == NULL) {
        fprintf(stderr, "Memory allocation failed\n");
        return 1;
    }
    // Inisialisasi byte array
    x[0] = 0xe3;
    x[1] = 0x81;
    x[2] = 0xaf; // "あ"

    // Konversi UTF-8 ke string dan cetak
    // Dalam C, kita bisa langsung mencetak byte sebagai string
    printf("%s\n", x);

    // Bebaskan memori yang dialokasikan
    free(x);

    return 0;
}
```
```rust
fn main() {
    // Alokasi memori secara dinamis untuk byte array
    let mut x: Vec<u8> = Vec::with_capacity(3);
    x.push(0xe3);
    x.push(0x81);
    x.push(0xaf); // "あ" dalam UTF-8

    // Konversi byte array ke string
    match String::from_utf8(x) {
        Ok(s) => println!("{}", s),
        Err(e) => eprintln!("Invalid UTF-8 sequence: {}", e),
    }
}
```
```rust
fn main() {
    let x: [u8; 3] = [0xe3, 0x81, 0xaf];
    match std::str::from_utf8(&x) {
        Ok(s) => println!("{}", s),
        Err(e) => eprintln!("Invalid UTF-8 sequence: {}", e),
    }
}
```
```rust
fn main() {
    let x: &[u8] = &[0xe3, 0x81, 0xaf];
    match std::str::from_utf8(x) {
        Ok(s) => println!("{}", s),
        Err(e) => eprintln!("Invalid UTF-8 sequence: {}", e),
    }
}
```

Golang
```golang
package main

import (
	"fmt"
	"unicode/utf8"
)

func main() {
	var x []byte = []byte{0xe3, 0x81, 0xaf}
	if utf8.Valid(x) {
		fmt.Println("Valid: ", string(x))
	} else {
		fmt.Println("invalid")
	}
}
```

C
```c
#include <stdio.h>
#include <stdbool.h>
#include <string.h>

// Fungsi untuk memeriksa keabsahan UTF-8
bool is_valid_utf8(const unsigned char *data, size_t len) {
    size_t i = 0;
    while (i < len) {
        unsigned char c = data[i];
        size_t remaining;

        if (c <= 0x7F) {
            // ASCII (0xxxxxxx)
            i++;
        } else if ((c & 0xE0) == 0xC0) {
            // 2-byte sequence (110xxxxx 10xxxxxx)
            remaining = 1;
            if (i + remaining >= len) return false;
            if ((data[i + 1] & 0xC0) != 0x80) return false;
            // Overlong encoding check: 0xC0 0x80 is invalid
            if (c == 0xC0 || c == 0xC1) return false;
            i += 2;
        } else if ((c & 0xF0) == 0xE0) {
            // 3-byte sequence (1110xxxx 10xxxxxx 10xxxxxx)
            remaining = 2;
            if (i + remaining >= len) return false;
            if ((data[i + 1] & 0xC0) != 0x80) return false;
            if ((data[i + 2] & 0xC0) != 0x80) return false;
            // Check for overlong encoding and surrogates
            if (c == 0xE0 && (data[i + 1] & 0xE0) == 0x80) return false;
            if (c == 0xED && (data[i + 1] & 0xE0) == 0xA0) return false;
            i += 3;
        } else if ((c & 0xF8) == 0xF0) {
            // 4-byte sequence (11110xxx 10xxxxxx 10xxxxxx 10xxxxxx)
            remaining = 3;
            if (i + remaining >= len) return false;
            if ((data[i + 1] & 0xC0) != 0x80) return false;
            if ((data[i + 2] & 0xC0) != 0x80) return false;
            if ((data[i + 3] & 0xC0) != 0x80) return false;
            // Check for code points > U+10FFFF
            if (c == 0xF0 && (data[i + 1] & 0xF0) == 0x80) return false;
            if (c > 0xF4 || (c == 0xF4 && (data[i + 1] & 0xF0) > 0x80)) return false;
            i += 4;
        } else {
            return false;
        }
    }
    return true;
}

int main() {
    unsigned char x[] = {0xe3, 0x81, 0xa7};
    size_t len = sizeof(x) / sizeof(x[0]);

    if (is_valid_utf8(x, len)) {
        printf("Valid: %s\n", x);
    } else {
        printf("invalid\n");
    }
    return 0;
}
```

Rust
```rust
fn is_valid_utf8(data: &[u8]) -> bool {
    let mut i = 0;
    let len = data.len();

    while i < len {
        let c = data[i];

        if c <= 0x7F {
            // ASCII
            i += 1;
        } else if (c & 0xE0) == 0xC0 {
            // 2-byte sequence
            if i + 1 >= len {
                return false;
            }
            let c1 = data[i + 1];
            if (c1 & 0xC0) != 0x80 {
                return false;
            }
            // Overlong encoding check
            if c == 0xC0 || c == 0xC1 {
                return false;
            }
            i += 2;
        } else if (c & 0xF0) == 0xE0 {
            // 3-byte sequence
            if i + 2 >= len {
                return false;
            }
            let c1 = data[i + 1];
            let c2 = data[i + 2];
            if (c1 & 0xC0) != 0x80 || (c2 & 0xC0) != 0x80 {
                return false;
            }
            // Check for overlong encoding and surrogates
            if c == 0xE0 && (c1 & 0xE0) == 0x80 {
                return false;
            }
            if c == 0xED && (c1 & 0xE0) == 0xA0 {
                return false;
            }
            i += 3;
        } else if (c & 0xF8) == 0xF0 {
            // 4-byte sequence
            if i + 3 >= len {
                return false;
            }
            let c1 = data[i + 1];
            let c2 = data[i + 2];
            let c3 = data[i + 3];

            if (c1 & 0xC0) != 0x80 || (c2 & 0xC0) != 0x80 || (c3 & 0xC0) != 0x80 {
                return false;
            }
            // Check code points > U+10FFFF
            if c == 0xF0 && (c1 & 0xF0) == 0x80 {
                return false;
            }
            if c > 0xF4 || (c == 0xF4 && (c1 & 0xF0) > 0x80) {
                return false;
            }
            i += 4;
        } else {
            return false;
        }
    }
    true
}

fn main() {
    let x = [0xe3, 0x81, 0xa7];

    if is_valid_utf8(&x) {
        // Convert byte array to string if valid
        match std::str::from_utf8(&x) {
            Ok(s) => println!("Valid: {}", s),
            Err(_) => println!("Invalid UTF-8 sequence"),
        }
    } else {
        println!("invalid");
    }
}
```

rust
```rust
fn main() {
    let bytes: Vec<Vec<u8>> = vec![
        vec![0xe3, 0x81, 0x94], // ご
        vec![0xe3, 0x81, 0xaf], // は
        vec![0xe3, 0x81, 0xbf], // み
        vec![0xe3, 0x81, 0x9a], // ず
        vec![0xe3, 0x81, 0xb2], // ひ
        vec![0xe3, 0x81, 0xa8], // と
        vec![0xe3, 0x81, 0x95], // さ
        vec![0xe3, 0x81, 0x9b], // せ
        vec![0xe3, 0x81, 0xa7], // で
        vec![0xe3, 0x81, 0x8c], // が
        vec![0xe3, 0x81, 0x91], // け
    ];

    // Mendefinisikan tipe data secara eksplisit untuk labels
    let labels: [&str; 11] = [
        " (go)", " (ha)", " (mi)", " (zu)", " (hi)",
        " (to)", " (sa)", " (se)", " (de)", " (ga)", " (ke)",
    ];

    for (i, byte_vec) in bytes.iter().enumerate() {
        let s = String::from_utf8(byte_vec.clone()).unwrap();
        println!("{} {}: {}", i + 1, labels[i], s);
    }
}
```

C
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // Define the byte arrays representing the Japanese characters
    unsigned char bytes[][3] = {
        {0xe3, 0x81, 0x94}, // ご
        {0xe3, 0x81, 0xaf}, // は
        {0xe3, 0x81, 0xbf}, // み
        {0xe3, 0x81, 0x9a}, // ず
        {0xe3, 0x81, 0xb2}, // ひ
        {0xe3, 0x81, 0xa8}, // と
        {0xe3, 0x81, 0x95}, // さ
        {0xe3, 0x81, 0x9b}, // せ
        {0xe3, 0x81, 0xa7}, // で
        {0xe3, 0x81, 0x8c}, // が
        {0xe3, 0x81, 0x91}  // け
    };

    // Corresponding labels
    const char *labels[] = {
        " (go)", " (ha)", " (mi)", " (zu)", " (hi)",
        " (to)", " (sa)", " (se)", " (de)", " (ga)", " (ke)"
    };

    int num_chars = sizeof(bytes) / sizeof(bytes[0]);

    for (int i = 0; i < num_chars; i++) {
        // Allocate buffer for null-terminated string
        char str[4];
        for (int j = 0; j < 3; j++) {
            str[j] = bytes[i][j];
        }
        str[3] = '\0'; // Null-terminate the string

        // Print index, label, and character
        printf("%d %s: %s\n", i + 1, labels[i], str);
    }

    return 0;
}
```

+ c
```c
#include <stdio.h>
#include <stdbool.h>
#include <string.h>

// Fungsi untuk memeriksa keabsahan UTF-8
bool is_valid_utf8(const unsigned char *data, size_t len) {
    size_t i = 0;
    while (i < len) {
        unsigned char c = data[i];
        size_t remaining;

        if (c <= 0x7F) {
            // ASCII (0xxxxxxx)
            i++;
        } else if ((c & 0xE0) == 0xC0) {
            // 2-byte sequence
            remaining = 1;
            if (i + remaining >= len) return false;
            if ((data[i + 1] & 0xC0) != 0x80) return false;
            if (c == 0xC0 || c == 0xC1) return false; // overlong encoding
            i += 2;
        } else if ((c & 0xF0) == 0xE0) {
            // 3-byte sequence
            remaining = 2;
            if (i + remaining >= len) return false;
            if ((data[i + 1] & 0xC0) != 0x80 || (data[i + 2] & 0xC0) != 0x80) return false;
            if (c == 0xE0 && (data[i + 1] & 0xE0) == 0x80) return false; // overlong
            if (c == 0xED && (data[i + 1] & 0xE0) == 0xA0) return false; // surrogate
            i += 3;
        } else if ((c & 0xF8) == 0xF0) {
            // 4-byte sequence
            remaining = 3;
            if (i + remaining >= len) return false;
            if ((data[i + 1] & 0xC0) != 0x80 || (data[i + 2] & 0xC0) != 0x80 || (data[i + 3] & 0xC0) != 0x80) return false;
            if (c == 0xF0 && (data[i + 1] & 0xF0) == 0x80) return false; // overlong
            if (c > 0xF4 || (c == 0xF4 && (data[i + 1] & 0xF0) > 0x80)) return false; // > U+10FFFF
            i += 4;
        } else {
            return false;
        }
    }
    return true;
}

int main() {
    // Array of byte sequences representing characters
    unsigned char bytes[][3] = {
        {0xe3, 0x81, 0x94}, // ご
        {0xe3, 0x81, 0xaf}, // は
        {0xe3, 0x81, 0xbf}, // み
        {0xe3, 0x81, 0x9a}, // ず
        {0xe3, 0x81, 0xb2}, // ひ
        {0xe3, 0x81, 0xa8}, // と
        {0xe3, 0x81, 0x95}, // さ
        {0xe3, 0x81, 0x9b}, // せ
        {0xe3, 0x81, 0xa7}, // で
        {0xe3, 0x81, 0x8c}, // が
        {0xe3, 0x81, 0x91}  // け
    };

    // Labels
    const char *labels[] = {
        " (go)", " (ha)", " (mi)", " (zu)", " (hi)",
        " (to)", " (sa)", " (se)", " (de)", " (ga)", " (ke)"
    };

    int num_chars = sizeof(bytes) / sizeof(bytes[0]);

    for (int i = 0; i < num_chars; i++) {
        size_t len = sizeof(bytes[i]) / sizeof(bytes[i][0]);

        if (is_valid_utf8(bytes[i], len)) {
            // Membuat string null-terminated
            char str[4];
            for (int j = 0; j < 3; j++) {
                str[j] = bytes[i][j];
            }
            str[3] = '\0';

            // Tampilkan hasil
            printf("%d %s: %s\n", i + 1, labels[i], str);
        } else {
            printf("%d %s: invalid UTF-8 sequence\n", i + 1, labels[i]);
        }
    }

    return 0;
}
```

bytesSlices - stdout
```golang
package main

import (
    "bytes"
    "fmt"
    "io"
    "unicode/utf8"
)

func main() {
    var bytesSlices [][]byte = [][]byte{
        {0xe3, 0x81, 0x94}, // ご
        {0xe3, 0x81, 0xaf}, // は
        {0xe3, 0x81, 0xbf}, // み
        {0xe3, 0x81, 0x9a}, // ず
        {0xe3, 0x81, 0xb2}, // ひ
        {0xe3, 0x81, 0xa8}, // と
        {0xe3, 0x81, 0x95}, // さ
        {0xe3, 0x81, 0x9b}, // せ
        {0xe3, 0x81, 0xa7}, // で
        {0xe3, 0x81, 0x8c}, // が
        {0xe3, 0x81, 0x91}, // け
    }

    var labels []string = []string{
        " (go)", " (ha)", " (mi)", " (zu)", " (hi)",
        " (to)", " (sa)", " (se)", " (de)", " (ga)", " (ke)",
    }

    // Loop melalui setiap byte slice
    for i, byteSlice := range bytesSlices {
        var buffer bytes.Buffer

        if utf8.Valid(byteSlice) {
            s := string(byteSlice)
            // Format string ke buffer
            fmt.Fprintf(&buffer, "%d %s: %s\n", i+1, labels[i], s)
        } else {
            fmt.Fprintf(&buffer, "%d %s: Invalid UTF-8 sequence\n", i+1, labels[i])
        }

        // Tampilkan isi buffer ke layar
        io.Copy(os.Stdout, &buffer)
    }
}
```

bytesSlices - file
```golang
package main

import (
    "bytes"
    "fmt"
    "io"
    "os"
    "unicode/utf8"
)

func main() {
    var bytesSlices [][]byte = [][]byte{
        {0xe3, 0x81, 0x94}, // ご
        {0xe3, 0x81, 0xaf}, // は
        {0xe3, 0x81, 0xbf}, // み
        {0xe3, 0x81, 0x9a}, // ず
        {0xe3, 0x81, 0xb2}, // ひ
        {0xe3, 0x81, 0xa8}, // と
        {0xe3, 0x81, 0x95}, // さ
        {0xe3, 0x81, 0x9b}, // せ
        {0xe3, 0x81, 0xa7}, // で
        {0xe3, 0x81, 0x8c}, // が
        {0xe3, 0x81, 0x91}, // け
    }

    var labels []string = []string{
        " (go)", " (ha)", " (mi)", " (zu)", " (hi)",
        " (to)", " (sa)", " (se)", " (de)", " (ga)", " (ke)",
    }

    // Membuka file output.txt
    file, err := os.Create("output.txt")
    if err != nil {
        fmt.Println("Gagal membuat file:", err)
        return
    }
    defer file.Close()

    // Loop melalui setiap byte slice
    for i, byteSlice := range bytesSlices {
        var buffer bytes.Buffer

        if utf8.Valid(byteSlice) {
            s := string(byteSlice)
            // Format string ke buffer
            fmt.Fprintf(&buffer, "%d %s: %s\n", i+1, labels[i], s)
        } else {
            fmt.Fprintf(&buffer, "%d %s: Invalid UTF-8 sequence\n", i+1, labels[i])
        }

        // Tulis isi buffer ke file menggunakan io.Copy
        io.Copy(file, &buffer)
    }

    fmt.Println("Output berhasil disimpan ke output.txt")
}
```
