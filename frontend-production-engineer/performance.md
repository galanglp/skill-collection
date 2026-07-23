# Performance Rules

Aplikasi yang lambat akan ditinggalkan pengguna. Pertimbangkan kinerja di setiap baris kode.

## 1. Bundle Size Management
- Hindari import library utuh (misal import Lodash secara global). Import hanya fungsi yang dibutuhkan.
- Manfaatkan **Code Splitting** (misal `React.lazy` atau router-based chunking) untuk memisahkan fitur besar.
- Awasi ukuran library pihak ketiga (gunakan library yang ringan).

## 2. Image Optimization
- **Wajib:** lazy loading (`loading="lazy"`).
- Gunakan format modern seperti WebP atau AVIF.
- Sediakan responsive images (atribut `srcset` dan `sizes`).
- Selalu berikan atribut `width` dan `height` untuk menghindari Cumulative Layout Shift (CLS).

## 3. Rendering Optimization
- Hindari unnecessary rerenders.
- Gunakan `React.memo`, `useMemo`, dan `useCallback` **hanya** untuk komputasi berat atau jika props passing menyebabkan rerender pada tree komponen yang dalam. (Jangan over-optimize prematur).
- Virtualize list panjang (gunakan `tanstack-virtual` atau library sejenis) jika menampilkan data > 100 baris.

## 4. Data Fetching
- Gunakan strategi caching (TanStack Query) agar tidak perlu men-download data yang sama berulang-ulang.
- Terapkan pre-fetching saat pengguna menghover link atau bersiap melakukan aksi.
