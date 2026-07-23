# Code Architecture Rules

## 1. Component Design
Gunakan prinsip **Single Responsibility Component**.
- **Buruk:** `<UserDashboard />` yang berisi API call, filtering, table, modal, form, dan validation sekaligus.
- **Baik:** Pisahkan menjadi komponen-komponen kecil, hooks, dan services sesuai feature.

## 2. Folder Structure Standard
Gunakan **Feature-based Architecture**. Hindari membuang semua komponen ke dalam satu folder `/components`.
```text
src/
├── app/
├── components/       # Global reusable UI components (Button, Input)
├── features/         # Feature-based modules
│   └── user/
│       ├── components/  # UserTable, UserFilter, UserModal
│       ├── hooks/       # useUsers
│       ├── api/         # userApi
│       └── schemas/     # user.schema.ts
├── hooks/            # Global hooks
├── lib/              # 3rd party library wrappers (axios, utils)
├── services/
├── stores/           # Global state
├── utils/
├── types/
└── styles/
```

## 3. TypeScript Rules
- **Wajib menggunakan strict typing.** Definisikan `interface` atau `type`.
- **Haram menggunakan `any`** kecuali benar-benar situasi darurat/tidak terelakkan.
- **Validasi Runtime:** Jangan sekadar type casting.
  - **Buruk:** `const data = response.data as User`
  - **Baik:** `const data = userSchema.parse(response.data)` (Gunakan Zod/Valibot)

## 4. State Management Philosophy
Pisahkan antara **Server State** dan **Client State**.
- **Server State:** Gunakan alat seperti **TanStack Query (React Query)** atau SWR.
  - Contoh: Fetching list user, detail produk.
- **Client State:** Gunakan **Zustand**, Jotai, atau React Context.
  - Untuk: Theme (dark/light), authentication state, UI state (sidebar open/close).
  - *Jangan simpan API data hasil fetch manual ke dalam Zustand.*

## 5. API Layer Rules
- **Jangan** melakukan data fetching langsung di dalam `useEffect` komponen kecuali sangat terpaksa.
- **Gunakan layer service:**
  ```typescript
  // services/user.service.ts
  export async function getUsers() {
    return api.get("/users");
  }
  ```
- Integrasikan service ini dengan TanStack Query di level custom hooks.
