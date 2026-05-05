# MyOS: A Minimalist x86_64 Learning Operating System

MyOS adalah proyek sistem operasi edukatif yang dibangun dari nol untuk memahami konsep fundamental Sistem Operasi langsung di atas arsitektur x86_64. Proyek ini berfokus pada implementasi kernel minimalis tanpa bergantung pada pustaka standar eksternal.

## 🎯 Tujuan Proyek
Tujuan utama dari MyOS bukan untuk menjadi OS yang kompleks, melainkan sebagai media belajar untuk memahami:
- **Booting Sequence:** Bagaimana CPU bertransisi dari BIOS ke Kernel.
- **Memory Management:** Implementasi Paging dan Physical Memory Management.
- **Process Management:** Memahami TCB (Task Control Block) dan Context Switching.
- **Interrupt Handling:** Menangani interupsi hardware seperti Keyboard dan Timer.
- **Scheduling:** Implementasi algoritma Round Robin sederhana.

## 🏗️ Arsitektur & Fitur
Proyek ini menggunakan desain **Monolithic Kernel** sederhana dengan fitur-fitur berikut:
- [x] **Custom Bootloader:** Inisialisasi CPU 16-bit ke 64-bit (Long Mode).
- [x] **VGA Text Driver:** Output teks langsung ke memori `0xB8000`.
- [x] **GDT & IDT:** Pengaturan tabel deskriptor CPU dan Interrupt Service Routines.
- [x] **Multitasking:** Kernel threads dengan Context Switching berbasis Assembly.
- [x] **Basic CLI:** Shell sederhana untuk berinteraksi dengan kernel.

## 📂 Struktur Proyek
```text
my-os/
├── src/
│   ├── boot/           # Assembly: Bootloader & Mode Switching
│   ├── kernel/         # C: Logika Utama (Main, IDT, GDT)
│   │   ├── cpu/        # Manajemen CPU & Interrupts
│   │   ├── mem/        # Manajemen Memori (Paging/PMM)
│   │   ├── proc/       # Scheduler & TCB (Task Control Block)
│   │   └── drivers/    # Driver Screen & Keyboard
│   └── common/         # Library utilitas internal
├── linker.ld           # Layout memori kernel
└── Makefile            # Otomatisasi Build & Emulasi
```

## Tech Stack ##

Berikut adalah teknologi yang digunakan untuk project ini:

* Assembler: nasm
* Compiler: x86_64-elf-gcc (Cross-compiler)
* Linker: x86_64-elf-ld
* Emulator: qemu-system-x86_64
* Build System: make

## Setup ##

Berikut adalah cara setup di Ubuntu/Debian

```bash
sudo apt update
sudo apt install nasm qemu-system-x86 build-essential
# Catatan: Sangat disarankan menggunakan cross-compiler GCC untuk x86_64-elf
```

## 📚 Referensi Belajar
- [OSDev Wiki](https://wiki.osdev.org)
- "Operating System Concepts" oleh Silberschatz, Galvin, & Gagne.
- "The Little OS Book" oleh Erik Helin & Adam Renberg.

---
Built with ❤️ for learning purpose.
