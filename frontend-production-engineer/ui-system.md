# Design System & UI Rules

## 1. Design Tokens
Selalu ekstrak nilai-nilai desain (warna, spacing, radius) ke dalam variabel CSS atau konfigurasi Tailwind.
```css
:root {
  --primary: #2563EB;
  --secondary: #64748B;
  --radius-sm: 0.25rem;
  --radius-md: 0.375rem;
  --spacing-1: 0.25rem;
  --spacing-2: 0.5rem;
}
```

## 2. Color Philosophy (60-30-10 Rule)
Jangan memilih warna secara random.
- **60% Background:** `#FFFFFF` (Light), `#09090B` (Dark).
- **30% Surface:** Card, sidebar, section background.
- **10% Accent:** Button, CTA, highlight.

**Semantic Colors Wajib:**
- `primary`, `secondary`, `success`, `warning`, `danger`, `info`, `muted`, `background`, `foreground`, `border`.

**Dark Mode Ready:**
Semua warna harus memikirkan versi Light dan Dark.
- *Light:* background: white, text: black
- *Dark:* background: #09090B, text: white

## 3. Typography System
Gunakan hierarchy yang jelas dan hindari ukuran font acak.
- **Heading XL (H1):** 48px
- **Heading L (H2):** 36px
- **Heading M (H3):** 24px
- **Body Large:** 18px
- **Body:** 16px
- **Caption:** 14px

## 4. Spacing System (8px Grid)
Wajib menggunakan kelipatan 4px atau 8px.
- `4, 8, 12, 16, 24, 32, 40, 48, 64`
- **Jangan:** `margin-top: 17px; padding: 13px;`

## 5. Component Quality & States
Setiap komponen interaktif WAJIB memiliki state berikut:
- **Normal:** Tampilan default.
- **Hover:** Indikasi bisa diinteraksi.
- **Focus / Focus-visible:** Penting untuk keyboard accessibility.
- **Active / Pressed:** Saat di-klik.
- **Disabled:** Visually disabled, tidak bisa di-klik.
- **Loading:** Spinner atau indikator proses.
- **Error:** Indikasi ada yang salah.

## 6. Animation Philosophy
- Gunakan animasi yang **subtle** (halus dan tidak berlebihan).
- Durasi ideal: `200ms - 300ms` dengan easing `ease-out`.
- Hindari animasi bouncing berlebihan yang memusingkan.
- Gunakan Framer Motion atau CSS Transition murni.

## 7. Design References
Ambil inspirasi komponen dan UX dari:
- Apple Human Interface Guidelines
- Material Design 3
- shadcn/ui philosophy
- Stripe Dashboard UX
- Linear App UX
- Vercel Dashboard UX
