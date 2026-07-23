# Frontend Engineering Philosophy

## Prinsip Utama

### 1. User First
- Setiap keputusan teknis harus berdampak pada pengalaman pengguna.
- Jangan membuat fitur hanya karena mudah di-code.
- Prioritaskan: Usability, Accessibility, Performance, Maintainability.

### 2. Simplicity Over Complexity
- Hindari over-engineering.
- Gunakan solusi paling sederhana yang scalable.
- Jangan membuat abstraction sebelum ada kebutuhan nyata.
- **Buruk:** `<UniversalDynamicComponentRenderer>` untuk button biasa.
- **Baik:** `<Button />`

### 3. Consistency Over Creativity
- UI production harus konsisten.
- **Jangan:** Setiap halaman punya card berbeda, spacing random, warna berbeda, typography berubah-ubah.
- **Gunakan:** Design token, Component system, Reusable pattern.

### 4. Production Mindset
- AI harus berpikir: *"Apakah kode ini aman dipakai 3 tahun?"*
- Bukan: *"Apakah kode ini berjalan sekarang?"*

## Tambahan Mindset (Product & Engineering)

### Product Thinking
- **Pahami User:** Siapa user yang akan menggunakan fitur ini?
- **Masalah & Solusi:** Apa masalah sebenarnya dan apakah fitur ini menyelesaikannya?
- **Business Goal:** Apa metrik keberhasilan bisnisnya (conversion, engagement)?

### Design Critique
- **Pertanyakan Desain:** Mampu menjawab *"Kenapa desain ini dibuat?"* bukan hanya *"Bagaimana membuat desain ini?"*.

### Refactoring & Debugging
- **Membaca Kode Lama:** Pahami konteks sebelum mengubah.
- **Aman Refactor:** Memperbaiki tanpa merusak fungsionalitas lain.
- **Root Cause Analysis:** Cari sumber bug, bukan hanya menambal gejala. Buat regression test jika perlu.
