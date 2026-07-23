# Security Rules

Frontend sering kali menjadi garis depan. Keamanan tidak boleh diabaikan.

## 1. Jangan Percaya Input User
- Validasi semua input di sisi client untuk UX yang baik, **sebelum** mengirim ke server.
- Gunakan library schema validation seperti **Zod**, **Yup**, atau **Valibot**.
- Jangan render HTML mentah dari input pengguna tanpa sanitasi (hindari `dangerouslySetInnerHTML` sebisa mungkin).

## 2. Manajemen Secrets
- **JANGAN PERNAH** meletakkan API Secret, Database Key, atau Private Token di frontend (client-side code).
- Gunakan Environment Variables (`NEXT_PUBLIC_*` atau `VITE_*`) hanya untuk API endpoint URL atau public key (seperti Stripe Publishable Key).

## 3. Authentication & Authorization
- Amankan akses route menggunakan Middleware atau Auth Guard.
- Pahami konsep penyimpanan token: HttpOnly Cookies lebih disukai daripada `localStorage` untuk mencegah serangan XSS.
- Jika terpaksa memakai `localStorage`, pastikan aplikasi kebal dari serangan XSS.

## 4. Proteksi Dasar
- Cegah CSRF jika tidak menggunakan framework fullstack yang sudah menanganinya (pastikan backend CORS dan header tersetup dengan benar).
- Lindungi aplikasi dari Clickjacking (header `X-Frame-Options` di server/meta).
