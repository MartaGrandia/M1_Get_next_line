# 🧵 Get Next Line (GNL)

> A low-level C function designed to read line-by-line from a file descriptor using static memory persistence and dynamically allocated buffers.

## 📖 Overview

`get_next_line` is a core C system programming project focused on file stream parsing, dynamic heap allocation, and state retention across function invocations. The function reads a single line ending with a newline (`\n`) or EOF from a given file descriptor without loading the entire file into memory at once.

## ⚙️ Technical Constraints & Architecture

- **Language:** C (compiled with `gcc -Wall -Wextra -Werror -D BUFFER_SIZE=n`).
- **Allowed System Calls:** Restricted to primitive POSIX I/O (`read`), dynamic memory management (`malloc`, `free`).
- **State Persistence:** Preserves unread stream data ("stash") across function calls using internal `static` variables.
- **Memory Safety:** Strictly audited zero-leak lifecycle management across both successful reads and unhandled I/O failures (verified via Valgrind).
- **Standards:** 100% compliant with 42's **Norminette** coding standard.

---

## ✨ Key Features & Technical Implementation

- **Arbitrary Buffer Execution:** Operates deterministically regardless of the specified `BUFFER_SIZE` macro (from 1-byte stress tests to large multi-megabyte I/O streams).
- **Stateful Stream Tracking:** Extracts text up to the first newline delimiter, returns a newly allocated string, and stores remaining bytes in static memory for subsequent calls.
- **Multi-File Descriptor Support (Bonus):** Supports simultaneous reading from multiple file descriptors concurrently using an indexed static pointer array without state cross-contamination.
- **Edge-Case Resilience:** Handles EOF, empty files, invalid file descriptors, dynamic allocation failures, and files missing trailing newlines gracefully.

---

## 🛠️ Quickstart & Integration Example

Since `get_next_line` is a utility function, you can test its behavior by integrating it into a test runner like `main.c`:

```c
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include "get_next_line.h"

int main(int argc, char **argv)
{
    int     fd;
    char    *line;
    int     lines_read;

    if (argc < 2)
    {
        printf("Usage: %s <filename>\n", argv[0]);
        return (1);
    }

    fd = open(argv[1], O_RDONLY);
    if (fd < 0)
    {
        perror("Error opening file");
        return (1);
    }

    lines_read = 0;
    while ((line = get_next_line(fd)) != NULL && lines_read < 5)
    {
        printf("%s", line);
        free(line); // Caller is responsible for freeing allocated line memory
        lines_read++;
    }

    close(fd);
    return (0);
}
