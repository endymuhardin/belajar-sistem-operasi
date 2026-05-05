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

## 🗺️ Development Roadmap

Proyek ini dibagi menjadi 5 fase pengembangan untuk memastikan sistem dapat dites secara bertahap (Incremental Testing).

### Phase 1: The First Breath (Booting & Output)
*Fokus: Memastikan siklus build-run bekerja.*
- [ ] **Milestone 1:** Membuat `boot.asm` dengan Magic Number `0xAA55`.
- [ ] **Milestone 2:** Menggunakan BIOS Interrupt `int 0x10` untuk output karakter tunggal.
- [ ] **Milestone 3:** Setup `Makefile` untuk otomatisasi kompilasi dan emulasi QEMU.
- [ ] **Test:** QEMU berhasil booting tanpa pesan "No bootable device".

### Phase 2: Crossing the Bridge (Long Mode & C Entry)
*Fokus: Migrasi dari 16-bit Assembly ke 64-bit C Environment.*
- [ ] **Milestone 4:** Inisialisasi GDT (Global Descriptor Table) awal.
- [ ] **Milestone 5:** Transisi ke **Long Mode (64-bit)** dan setup Kernel Stack.
- [ ] **Milestone 6:** Implementasi VGA Text Driver di C (Menulis langsung ke `0xB8000`).
- [ ] **Test:** Layar QEMU bersih (clear screen) melalui fungsi yang ditulis dalam bahasa C.

### Phase 3: The Nervous System (Interrupts & Memory)
*Fokus: Komunikasi dengan hardware dan pengelolaan resource.*
- [ ] **Milestone 7:** Implementasi **IDT (Interrupt Descriptor Table)** untuk menangani Exceptions.
- [ ] **Milestone 8:** Driver Keyboard sederhana (Scancode to ASCII conversion).
- [ ] **Milestone 9:** **Physical Memory Manager (PMM)** menggunakan metode Bitmap.
- [ ] **Test:** Mengetik di keyboard dan karakter muncul di layar secara real-time.

### Phase 4: The Puppet Master (Multitasking)
*Fokus: Menjalankan beberapa tugas secara bersamaan (Core OS Concept).*
- [ ] **Milestone 10:** Struktur data **TCB (Task Control Block)** untuk menyimpan konteks CPU.
- [ ] **Milestone 11:** Implementasi **Context Switching** di dalam Timer Interrupt (PIT).
- [ ] **Milestone 12:** Scheduler sederhana dengan algoritma Round Robin.
- [ ] **Test:** Dua fungsi kernel berjalan secara bergantian (simulasi multitasking).

### Phase 5: The Interaction (Shell & Bare Metal)
*Fokus: User interface dan pengujian pada perangkat keras asli.*
- [ ] **Milestone 13:** Basic Command Shell (mendukung perintah `help`, `mem`, `clear`).
- [ ] **Milestone 14:** Final Binary Optimization.
- [ ] **Milestone 15:** Deployment ke USB Flash Drive menggunakan `dd`.
- [ ] **Test:** OS berhasil berjalan di laptop fisik melalui booting USB.

## 📚 Referensi Belajar
- [OSDev Wiki](https://wiki.osdev.org)
- "Operating System Concepts" oleh Silberschatz, Galvin, & Gagne.
- "The Little OS Book" oleh Erik Helin & Adam Renberg.

---
Built with ❤️ for learning purpose.
