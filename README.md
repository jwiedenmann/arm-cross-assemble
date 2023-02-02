# ARM Cross Assemble

Sample project for setting up a cross assembler and running ARM binaries on x86_64.

[source](https://azeria-labs.com/arm-on-x86-qemu-user/)

## Setup

1. Install and setup WSL
2. Install qemu and gcc 32/64bit assembler

`sudo apt update -y && sudo apt upgrade -y`

`sudo apt install qemu-user qemu-user-static`

`sudo apt install gcc-aarch64-linux-gnu binutils-aarch64-linux-gnu binutils-aarch64-linux-gnu-dbg build-essential`

`sudo apt install gcc-arm-linux-gnueabihf binutils-arm-linux-gnueabihf binutils-arm-linux-gnueabihf-dbg`

## Assemble

### 64bit

`aarch64-linux-gnu-as "asm64.s" -o "asm64.o" && aarch64-linux-gnu-ld "asm64.o" -o "asm64"`

### 32bit

`arm-linux-gnueabihf-as "asm32.s" -o "asm32.o" && arm-linux-gnueabihf-ld -static "asm32.o" -o asm32`

## Run

### 64bit

`qemu-aarch64 "asm64"`

### 32bit

`qemu-arm "asm32"`

# Remote Debugging

## Setup

1. Install gdb-multiarch
2. Install [GEF](https://github.com/hugsy/gef)

## Run

1. Assemble ARM binaries
2. Open two terminal windows and navigate to the binaries
3. Execute Qemu with debug flags

    `qemu-arm -g 1234 asm32`

4. Connect to Qemu via GDB

    `gdb-multiarch`

    `gef-remote --qemu-user --qemu-binary asm32 localhost 1234`

## Commands

- nexti - Executes a line
- stepi - Steps in a function