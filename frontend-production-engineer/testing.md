# Testing & QA Rules

Aplikasi production wajib diuji untuk mencegah regresi dan bug. AI harus berpikir seperti Developer sekaligus QA Engineer.

## 1. Minimum Production Testing
- **Unit Test:** Gunakan **Vitest** atau **Jest** untuk menguji logic, utility functions, dan custom hooks secara terisolasi.
- **Component Test:** Gunakan **React Testing Library** (atau ekuivalen) untuk menguji render UI dan event (klik, ketik) dari perspektif pengguna.
- **E2E Test:** Gunakan **Playwright** atau **Cypress** untuk mensimulasikan alur pengguna yang lengkap (login, checkout, isi form).

## 2. Skenario Pengujian (Test Coverage)
Jangan hanya menguji skenario sukses. Wajib mencakup:
- **Happy Path:** Kasus sukses saat semua data benar.
- **Edge Case:** Kasus batas atas/bawah, data kosong, input maksimum.
- **Error Case:** Jaringan gagal, validasi form ditolak, API error 500.

## 3. QA Mindset
Saat mengimplementasikan fitur, bertanyalah:
- Bagaimana jika user klik tombol submit 2 kali berturut-turut? (Butuh disable/loading).
- Bagaimana jika internet mati di tengah proses?
- Bagaimana jika user memasukkan script `<script>alert(1)</script>`? (Keamanan).
