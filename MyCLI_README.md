# MyCLI Tool

## Overview
MyCLI is a simple command-line tool built using the [Cosmopolitan C Library (Cosmo)](https://github.com/jart/cosmopolitan). It demonstrates how to create portable CLI applications that work across Windows, Linux, and macOS using a single binary.

## Features
- **Cross-Platform Support**: One binary runs on multiple operating systems.
- **Lightweight**: Minimal dependencies and small binary size.
- **Portable**: Static compilation ensures easy distribution.
- **Custom Commands**: Includes basic commands like `hello` and `goodbye`.

## Prerequisites
- A C compiler like `gcc` or `clang`.
- Cosmopolitan library (download from [GitHub](https://github.com/jart/cosmopolitan)).

## Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/jart/cosmopolitan.git
cd cosmopolitan
```

### 2. Write Your CLI Code
Create a file named `mycli.c` with the following content:

```c
#include "libc/log/log.h"
#include "libc/stdio/stdio.h"
#include "libc/str/str.h"

int main(int argc, char *argv[]) {
    if (argc < 2) {
        printf("Usage: %s <command>\n", argv[0]);
        return 1;
    }
    if (!strcmp(argv[1], "hello")) {
        printf("Hello, World!\n");
    } else if (!strcmp(argv[1], "goodbye")) {
        printf("Goodbye, World!\n");
    } else {
        printf("Unknown command: %s\n", argv[1]);
    }
    return 0;
}
```

### 3. Compile the Program
Compile your CLI application using the Cosmopolitan library:

```bash
gcc -static -nostdlib -o mycli.com -Os -fno-pie -no-pie mycli.c cosmopolitan.a
```
This generates a portable binary named `mycli.com`.

### 4. Run the CLI
Test the binary:

```bash
./mycli.com hello
./mycli.com goodbye
./mycli.com unknown
```

## Advanced Features

### Argument Parsing
Add argument parsing for more complex commands:
```c
if (!strncmp(argv[1], "--name=", 7)) {
    printf("Hello, %s!\n", argv[1] + 7);
}
```

### File Operations
Read files using Cosmopolitan's file handling APIs:
```c
FILE *file = fopen("example.txt", "r");
if (file) {
    char buffer[256];
    while (fgets(buffer, sizeof(buffer), file)) {
        printf("%s", buffer);
    }
    fclose(file);
} else {
    perror("Error opening file");
}
```

### Error Logging
Use logging for debugging:
```c
LOGF("An error occurred: %s", strerror(errno));
```

## Example
Below is a more detailed CLI example:

```c
#include "libc/stdio/stdio.h"
#include "libc/str/str.h"

void print_help() {
    printf("MyCLI Tool\n");
    printf("Usage:\n");
    printf("  mycli hello       - Say hello\n");
    printf("  mycli goodbye     - Say goodbye\n");
    printf("  mycli --help      - Show this help message\n");
}

int main(int argc, char *argv[]) {
    if (argc < 2 || !strcmp(argv[1], "--help")) {
        print_help();
        return 0;
    }
    if (!strcmp(argv[1], "hello")) {
        printf("Hello, World!\n");
    } else if (!strcmp(argv[1], "goodbye")) {
        printf("Goodbye, World!\n");
    } else {
        printf("Unknown command: %s\n", argv[1]);
    }
    return 0;
}
```

## License
This project is licensed under the MIT License. For more details, see the [LICENSE](LICENSE) file.

## Contributing
Contributions are welcome! Feel free to open issues or submit pull requests to enhance functionality.

---

### References
- [Cosmopolitan GitHub](https://github.com/jart/cosmopolitan)
- [Cosmopolitan Documentation](https://justine.lol/cosmopolitan/index.html)
