# AI Self Review Loop & Checklist

Sebelum memberikan output akhir atau mengakhiri sesi coding frontend, kamu **WAJIB** mengecek checklist berikut dan memastikan semuanya terpenuhi.

## Self Review Loop
Lakukan loop analisis internal ini sebelum menulis kode akhir:
1. **Check requirement:** Apakah solusi ini menyelesaikan masalah yang diminta user?
2. **Check UX:** Apakah alurnya mudah dimengerti user? Ada loading/error state?
3. **Check accessibility:** Apakah HTML semantic? Bisa dilalui dengan tab keyboard? Kontras cukup?
4. **Check responsive:** Apakah tampilannya pecah di layar HP (320px)?
5. **Check security:** Apakah input di-validate? Ada data sensitif yang bocor?
6. **Check performance:** Apakah image di-lazy load? Apakah ada looping/render yang tidak perlu?
7. **Check maintainability:** Apakah kode rapi? Apakah strukturnya feature-based?
8. **Generate test case:** Apakah edge case sudah dipikirkan?

## Output Checklist Akhir (Production Ready)
Pastikan hal-hal berikut dicentang (secara logika):
- [ ] TypeScript Strict (tanpa `any`).
- [ ] Responsive & Mobile-first approach.
- [ ] Mendukung Dark Mode (atau minimal color system yang extensible).
- [ ] Tersedia Loading state (skeleton/spinner).
- [ ] Tersedia Empty state.
- [ ] Tersedia Error state & Error recovery mechanism.
- [ ] Accessibility (ARIA, Semantic, Keyboard, Kontras).
- [ ] SEO metadata (Title, Description) diupdate jika berupa halaman baru.
- [ ] Performance optimized (Lazy load, memoization bijak, size terkontrol).
- [ ] Component reusable & mengikuti arsitektur yang benar.
- [ ] Tidak ada duplikasi kode berlebih (DRY).
- [ ] Testing/QA mindset diterapkan.
- [ ] Kode layak masuk ke lingkungan Production.
