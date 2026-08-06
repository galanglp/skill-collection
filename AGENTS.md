
# Wajib Dokumentasi Fungsi
- **Setiap fungsi yang ditulis atau dimodifikasi harus memiliki dokumentasi fungsi yang jelas.**
- Dokumentasi ini harus menjelaskan tujuan fungsi, parameter yang diterima, nilai kembalian (return value), dan efek samping (side effects) jika ada.
- Gunakan standar dokumentasi yang sesuai dengan bahasa pemrograman yang digunakan (misalnya JSDoc untuk JavaScript/TypeScript, Docstrings untuk Python/Go, dll).
- Tujuannya adalah memastikan kode mudah dibaca, dipahami, dan dilanjutkan oleh developer lain (maintainability).

<!-- sequential-thinking-mandatory:start -->
# Mandatory Sequential Thinking Protocol (Self-Assessed Dynamic Complexity & Documentation-Aware)

Anda WAJIB menjalankan tool MCP `sequential-thinking` (`sequentialthinking`) untuk SETIAP instruksi atau pesan yang diterima dari pengguna SEBELUM melakukan eksekusi alat lain (file edit, shell command, create artifact) atau memberikan jawaban akhir.

## 1. Aturan Utama (Hard Invariants)
1. **Zero-Turn Direct Execution Forbidden**: Dilarang keras melakukan aksi langsung, menulis kode, atau menjawab prompt tanpa melewati siklus berpikir bertahap pada MCP `sequentialthinking`.
2. **Autonomous Complexity Assessment (Thought 1)**: Pengguna TIDAK PERLU menentukan kompleksitas tugas. Pada Thought 1, model AI WAJIB menilai kompleksitas tugas secara otonom berdasarkan *Scope*, *Cognitive Depth*, dan *Blast Radius*, lalu menetapkan `totalThoughts` secara dinamis.
3. **Adaptive Thought Expansion**: Jika dalam proses analisis ditemukan dependensi baru, edge-case, atau risiko tak terduga, `totalThoughts` WAJIB dinaikkan secara dinamis (`needsMoreThoughts: true`).
4. **Mandatory Documentation Thinking**: Setiap perancangan atau modifikasi kode WAJIB memetakan dokumentasi fungsi (tujuan, parameter, return value, side effects, standar JSDoc/Docstring) di dalam proses berpikir sebelum implementasi.
5. **Convergence & Guardrails**:
   - `revision_limit = 2`: Hindari merevisi pemikiran yang sama lebih dari 2 kali.
   - `stop_when_confident = true`: Akhiri pemikiran (`nextThoughtNeeded: false`) setelah verifikasi dan execution plan tervalidasi solid tanpa membuang token untuk padding.
   - `default_baseline = 5–8 thoughts` untuk tugas dengan kompleksitas menengah.

## 2. Dynamic Complexity & Thought Allocation Spectrum
Model AI menentukan rentang target langkah pemikiran secara proporsional:
- **Tier 1: Micro / Quick Fix (3–5 thoughts)**: Perubahan 1 file terisolasi, perbaikan typo/dokumentasi, klarifikasi direct, penyesuaian config sederhana.
- **Tier 2: Standard Feature / Moderate (5–8 thoughts - Default)**: Fitur multi-file, integrasi logika baru (misal NestJS + React), modifikasi utility/komponen.
- **Tier 3: In-Depth Debugging / Complex PR Review (8–12 thoughts)**: Investigasi bug sulit (race condition, state issue), audit keamanan/performa, code review komprehensif.
- **Tier 4: System Architecture / Core Refactor (10–15 thoughts)**: Perancangan arsitektur baru, perombakan database/schema, integrasi multi-service.
- **Tier 5: Massive System Migration / Redesign (15–20 thoughts)**: Migrasi framework besar, breaking API redesign yang melibatkan puluhan modul.

## 3. Thought Execution Protocol (5 Tahapan Wajib)
Setiap siklus pemikiran harus mencakup tahapan berikut secara berurutan:
- **Step 1 - Deconstruction, Goal & Auto-Complexity**: Membedah maksud instruksi, mengklasifikasikan tingkat kompleksitas (Tier 1-5), dan menginisialisasi `totalThoughts`.
- **Step 2 - Context, Knowledge Graph & Dependency Mapping**: Menghubungkan tugas dengan arsitektur kode saat ini, relasi file, dan dependensi terkait.
- **Step 3 - Hypothesis Generation & Alternative Exploration**: Merumuskan hipotesis solusi utama dan mengeksplorasi cabang solusi alternatif jika diperlukan (`branchId`, `branchFromThought`).
- **Step 4 - Risk Assessment, Side-Effects & Documentation Scope**: Menguji kelemahan solusi, potensi *side-effects*, dan memetakan kontrak fungsi (parameter, return type, exception/error) yang wajib didokumentasikan.
- **Step 5 - Execution Blueprint & Verification Criteria**: Merancang urutan aksi nyata, skema dokumentasi fungsi (JSDoc/Docstring lengkap), dan metode verifikasi yang terukur sebelum menyetel `nextThoughtNeeded: false`.

## 4. Urutan Integrasi & Prioritas Tool
1. `sequential-thinking` (Analisis & Rencana) ➔ 2. `codebase-memory-mcp` (Graph Discovery) ➔ 3. `lean-ctx` (Context & Read) ➔ 4. `Native Edit / Command` (Eksekusi + Dokumentasi Fungsi) ➔ 5. `Verification`.
<!-- sequential-thinking-mandatory:end -->
