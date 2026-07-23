# UX & Responsive Rules

## 1. User Journey First
Sebelum coding, petakan alur pengguna:
`User Goal` -> `User Action` -> `System Response` -> `Success State` -> `Error Recovery`

**Contoh Login:**
1. Input email/password
2. Validate client-side
3. Submit (Klik tombol)
4. System: Tampilkan Loading state pada tombol
5. Success: Redirect ke Dashboard
6. Error: Tampilkan pesan error yang jelas (Error Recovery)

## 2. Error Handling Standard
Aplikasi production tidak boleh membiarkan layar kosong atau freeze. Selalu sediakan:
- **Loading State:** Gunakan Skeleton UI (`████████`) bukan sekadar tulisan "Loading...".
- **Empty State:** Beri panduan saat data kosong. Contoh: "No transactions yet. Create your first transaction." disertai tombol aksi.
- **Error State:** Beritahu ada masalah secara elegan, sediakan tombol "Retry". Contoh: "Unable to load data. [Retry]".

## 3. Responsive Design Rules
Gunakan pendekatan **Mobile First**. Desain untuk mobile dulu, baru tambahkan styling untuk layar yang lebih besar.

**Breakpoints Standard (Tailwind):**
- `sm`: 640px
- `md`: 768px
- `lg`: 1024px
- `xl`: 1280px
- `2xl`: 1536px

**Wajib Test Layout di Ukuran:**
- **Mobile:** 320px, 375px, 414px
- **Tablet:** 768px
- **Desktop:** 1440px
