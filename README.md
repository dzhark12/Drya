# Drya — Minimal RISC-V Kernel Demo

This repository contains a very small RISC-V kernel demo that clears BSS and prints a simple "Hello World" message using an SBI `ecall` helper.

## Prerequisites

- A RISC-V cross toolchain (if you plan to build manually).
- QEMU or other emulator for running RISC-V binaries, or your hardware toolchain.
- The provided `run.sh` script (may already wrap build + run steps).

## Build & Run

Use the provided run script if present:

```bash
./run.sh
```

Manual example (adjust to your toolchain and flags):

```bash
# Example, may require riscv64-unknown-elf-* toolchain
riscv64-unknown-elf-gcc -nostdlib -march=rv64imac -mabi=lp64 -T kernel.ld -o kernel.elf *.c
# convert to binary/bootable image as needed, then run in QEMU
qemu-system-riscv64 -machine virt -nographic -bios none -kernel kernel.elf
```

## Files

- `kernel.c` — Kernel entry, BSS clear, SBI `sbi_call`, `putchar`, and `kernel_main` printing "Hello World".
- `kernel.h` — Small header (SBI return struct, etc.).
- `kernel.ld` — Linker script for the kernel (layout and sections).
- `run.sh` — Helper script to build/run (if present).

## Notes

- A backup of the previous `kernel.c` was saved as `kernel.c.bak` during merging.
- The code uses inline assembly for `ecall` and assumes an SBI implementation that services console output.

## References
https://operating-system-in-1000-lines.vercel.app/en/

