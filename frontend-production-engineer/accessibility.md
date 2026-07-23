# Accessibility (WCAG) Rules

Aplikasi production harus bisa diakses oleh semua orang, termasuk mereka yang menggunakan screen reader atau navigasi keyboard.

## 1. Semantic HTML
Gunakan tag HTML sesuai fungsinya.
- **Buruk:** `<div onclick="submit()">Submit</div>`
- **Baik:** `<button type="submit">Submit</button>`
- Gunakan `<nav>`, `<aside>`, `<header>`, `<footer>`, `<main>`, `<section>`.

## 2. Keyboard Navigation
Semua elemen interaktif (button, link, input, modal, dropdown) harus bisa dinavigasi dengan tombol `Tab`.
- Jangan hilangkan outline `focus` tanpa memberikan alternatif visual `focus-visible`.
- Pastikan urutan tab (DOM order) logis.
- Pastikan ada mekanisme **Focus Trap** di dalam Modal/Dialog.

## 3. Contrast Ratio
Pastikan teks mudah dibaca di atas background.
- **Minimal WCAG AA:** Rasio kontras 4.5:1 untuk teks biasa, dan 3:1 untuk teks besar.

## 4. ARIA Attributes
Gunakan atribut ARIA hanya jika semantic HTML tidak cukup.
- `aria-label` untuk ikon tanpa teks.
- `aria-expanded` untuk accordion/dropdown.
- `aria-hidden="true"` untuk dekorasi yang tidak penting dibaca screen reader.
- `role="alert"` atau `aria-live="polite"` untuk notifikasi atau toast.
