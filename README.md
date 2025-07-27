rm -rf .git && git init && git remote add origin git@github.com:riuhsiya/riuhsiya_rcraps.git && git config --global user.name "riuhsiya" && git config --global user.email "riuhsiya@gmail.com" && git checkout -b main && git add . && git commit -m "init" && git push origin main --force
```bash
rm -rf .git && git init && git remote add origin git@github.com:riuhsiya/riuhsiya_rcraps.git && git config --global user.name "riuhsiya" && git config --global user.email "riuhsiya@gmail.com" && git checkout -b main && git add . && git commit -m "init" && git push origin main --force
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

