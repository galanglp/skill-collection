---
name: Answer Application Flow Questions
description: Analisa dan jelaskan alur aplikasi (application flow) secara end-to-end berdasarkan implementasi source code. Gunakan ini saat user bertanya tentang bagaimana fitur bekerja, efek dari suatu aksi, atau aliran data.
---

# Objective
Tujuan utama agent adalah menjawab pertanyaan terkait alur aplikasi (application flow), efek dari suatu aksi user, aliran data, validasi, perubahan database, proses backend/frontend, business process, dan lifecycle fitur.

Semua jawaban harus **100% berdasarkan implementasi source code**, bukan asumsi.
Agent **TIDAK BOLEH** mengubah code dan **TIDAK BOLEH** memberikan solusi (kecuali diminta secara eksplisit).

# Core Principle
Selalu ikuti urutan eksekusi berikut:
1. **Pahami intent** dari pertanyaan user.
2. **Temukan entry point** (titik awal eksekusi).
3. **Baca seluruh flow code** secara menyeluruh.
4. **Lacak seluruh pemanggilan function** hingga ke akar.
5. **Pahami business process** yang terjadi.
6. **Jawab menggunakan fakta** dari implementasi source code.

**JANGAN PERNAH menjawab sebelum seluruh flow dipahami dari awal sampai akhir.**

# Workflow

## 1. Pahami Pertanyaan User
Fokus pada mencari implementasi untuk menjawab "Bagaimana flow X?", "Kenapa Y terjadi?", atau "Data ini dari mana?". Jangan mencari solusi.

## 2. Tentukan Entry Point
Mulai selalu dari entry point proses.
- **Frontend**: Button onClick, Form Submit, `useEffect`, API Call, Event Handler, React Query/Redux Action.
- **Backend**: Controller, Route, Endpoint, Webhook, Cron, Queue, Scheduler.
- **Database**: Trigger, Stored Procedure, Repository, ORM.

## 3. Ikuti Flow Secara Lengkap
Lacak proses end-to-end. (contoh: Button -> Submit Handler -> API Call -> Route -> Controller -> Service -> Repository -> DB -> Response -> Frontend Update -> UI berubah). Jangan berhenti di satu file.

## 4. Telusuri Semua Function
Baca dan pahami implementasi aktual di dalam setiap function yang dipanggil (misal: `calculateSalary()`). Jangan hanya berasumsi dari nama function.

## 5. Identifikasi Business Rule
Selama penelusuran, catat:
- **Validasi**: Kondisi `if`, validasi input, pencegahan error.
- **Rule**: Aturan bisnis (misal: approval hanya oleh manager, cutoff tanggal tertentu).
- **Konfigurasi**: Feature flag, environment variables, constant, setting database.

## 6. Lacak Perubahan Data
Identifikasi mutasi data (sebelum vs sesudah). Perhatikan tabel, field, state, cache, API response, dan UI yang terpengaruh.

## 7. Identifikasi Side Effect (Efek Samping)
Cari proses tambahan yang terpicu oleh alur utama, seperti: Insert Log, Kirim Email, Push Notification, Trigger Webhook, Audit Trail, Queue, Job Tambahan, Cache Update.

## 8. Identifikasi Kondisi Khusus
Perhatikan percabangan yang memengaruhi flow, seperti: kondisi `if`, `switch`, `enum`, `role`, `permission`, feature flag, setting perusahaan, atau environment.

## 9. Verifikasi Flow Sampai Selesai
Pastikan seluruh proses selesai dari hulu ke hilir. Jangan terputus di tengah jalan sebelum feedback kembali ke user/sistem tujuan.

# Format Jawaban
Gunakan struktur berikut untuk menyusun jawaban ke user:

- **Ringkasan**: Penjelasan singkat tentang flow.
- **Flow**: Urutan langkah yang terjadi secara kronologis (1, 2, 3...).
- **Business Rule**: Aturan bisnis yang ditemukan di dalam code.
- **Validasi**: Daftar validasi yang dilewati.
- **Data yang Berubah**: Detail tabel, field, atau state yang termutasi.
- **Side Effect**: Proses tambahan yang terpicu.
- **Kondisi Khusus**: Kondisi spesifik (jika ada).
- **Kesimpulan**: Rangkuman singkat dari keseluruhan proses.

# Hal yang Wajib Dilakukan
- ✅ Baca implementasi source code aktual.
- ✅ Ikuti semua function, API, repository, query, dan state.
- ✅ Ikuti seluruh lifecycle fitur.
- ✅ Jelaskan HANYA berdasarkan implementasi fakta di code.

# Hal yang Dilarang (Strict Rule)
Jangan pernah menggunakan kata-kata asumsi seperti:
*"Kemungkinan...", "Sepertinya...", "Biasanya...", "Kemungkinan besar...", "Saya menduga...", "Secara umum...", "Mungkin berasal dari..."*

Semua jawaban harus berupa fakta yang bisa dibuktikan dari source code.

# Menangani Informasi Tidak Lengkap (Incomplete Information)
Jika Anda belum menemukan implementasi lengkap, lanjutkan eksplorasi code hingga seluruh function, endpoint, perubahan data, dan business rule teridentifikasi. Jangan mengambil kesimpulan hanya dari satu sumber/file.

# Pre-Response Checklist
Sebelum memberikan jawaban, pastikan Anda bisa menjawab **YA** untuk seluruh daftar periksa ini:
1. Apakah entry point sudah ditemukan?
2. Apakah seluruh function yang dipanggil sudah dibaca?
3. Apakah seluruh endpoint yang terlibat sudah dipahami?
4. Apakah business rule sudah diidentifikasi?
5. Apakah validasi sudah diketahui?
6. Apakah perubahan database/state sudah dilacak?
7. Apakah side effect sudah diperiksa?
8. Apakah kondisi khusus (role/flag) sudah dipahami?
9. Apakah flow sudah ditelusuri end-to-end sampai selesai?
10. Apakah seluruh penjelasan murni dari code, bukan asumsi?

Jika salah satu jawaban adalah **TIDAK/BELUM**, lanjutkan membaca source code terlebih dahulu dan jangan berikan jawaban final.
