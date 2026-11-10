# 🔄 Piscine Reload

A targeted refresher engineering suite validating core low-level C concepts, pointer arithmetic, memory management, function pointers, and build system configurations.

## 📖 Overview

This repository consolidates a rapid-fire review of foundational Unix shell administration, manual C memory manipulation, custom string operations, dynamic array allocation, higher-order function pointers, and `Makefile` automation. It serves as a benchmark for verifying low-level programming readiness before advancing to complex system architectures.

## ⚙️ Technical Standards & Constraints

- **Language:** C (compiled with `gcc -Wall -Wextra -Werror`).
- **Coding Standard:** 100% compliance with 42's **Norminette** linter.
- **Low-Level Execution:** Zero reliance on standard library abstractions. Custom implementations written using primitive system calls (`write`, `malloc`, `free`).
- **Memory Safety:** Strict heap memory lifecycle management with zero tolerance for dangling pointers or memory leaks.

---

## 🗺️ Topic Breakdown & Implementation Summary

| Category | Key Concepts | Implementations & Technical Scope |
| :--- | :--- | :--- |
| **Shell & Environment** | Terminal Pipelines & POSIX | File system queries (`find`, `ls`), attribute filtering, line counting pipelines. |
| **Pointers & Addressing** | Pointer Arithmetic & In-Place Ops | Single and multi-level pointer dereferencing (`ft_ft`, `ft_ultimate_ft`), variable swaps, quotient/remainder calculation via reference. |
| **String Manipulation** | Null-Terminated Buffers | Reimplementation of core string utilities (`ft_putstr`, `ft_strlen`, `ft_strcmp`). |
| **Dynamic Memory** | Heap Allocation & Buffer Duplication | Dynamic memory allocation via `malloc` (`ft_range`, `ft_strdup`, argument array concatenation). |
| **Function Pointers** | Higher-Order Functions in C | Passing function addresses as parameters to iterate over, transform, or evaluate dynamic arrays (`ft_foreach`, `ft_map`, `ft_any`, `ft_count_if`). |
| **Builds & Preprocessor** | Build Systems & Header Guards | Writing robust `Makefile` automation (`all`, `clean`, `fclean`, `re`), macro definitions (`ft_abs.h`), and custom structure definitions (`ft_point.h`). |

---

## 🛠️ Quickstart & Compilation

### Testing Utility Functions

To test individual exercises (such as string manipulation or memory allocation routines), compile the target source file alongside a test runner `main.c`:

```c
#include <unistd.h>

void ft_putstr(char *str);

int main(void)
{
    ft_putstr("Testing Piscine Reload utilities...\n");
    return (0);
}
