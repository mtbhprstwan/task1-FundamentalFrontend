# 📘 Tugas Bab 2 — Tailwind CSS

> **Mata Kuliah:** Pengembangan Frontend Dasar  
> **Topik:** Tailwind CSS — Utility-first, Responsive Design, Component Styling, Best Practices  
> **Durasi:** 1 Minggu | **Sifat:** Individu

---

## 🎯 Deskripsi Tugas

Kamu berperan sebagai **Frontend Developer** di tim EduSmart — sebuah platform edukasi digital yang sedang membangun ulang website mereka dari nol.

Tugasmu adalah membuat **satu halaman landing page lengkap** untuk EduSmart menggunakan **Tailwind CSS**. Halaman ini harus mencakup tiga bagian utama: **Hero Section**, **Card Section fitur**, dan **Footer** — sekaligus menerapkan empat aspek materi Tailwind CSS secara terpadu dalam satu proyek.

---

## 📋 Aspek Penilaian

### 1 Hero Section — Utility-first CSS 

Bangun bagian Hero **tanpa menulis CSS kustom sama sekali** — seluruh styling hanya menggunakan class utilitas Tailwind langsung di markup HTML.

**Elemen yang wajib ada:**
- Background berwarna menggunakan class Tailwind (bukan `style=""` atau `<style>`)
- Judul utama (`h1`) berwarna putih, besar, dan menarik
- Paragraf deskripsi singkat tentang platform EduSmart
- Tombol "Mulai Belajar" dengan hover state menggunakan Tailwind
- Seluruh padding, alignment, dan spacing hanya dari utilitas Tailwind


---

### 2 Card Section Fitur — Responsive Design 

Buat section yang menampilkan fitur-fitur EduSmart dalam **grid yang responsif** menggunakan breakpoint mobile-first Tailwind.

**Spesifikasi layout:**

| Ukuran Layar | Tampilan | Class Tailwind |
|---|---|---|
| Mobile (default) | 1 kolom | `grid-cols-1` |
| Tablet (`md:` ≥768px) | 2 kolom | `md:grid-cols-2` |
| Desktop (`lg:` ≥1024px) | 3 kolom | `lg:grid-cols-3` |

**Isi tiap card (minimal 3 card):**
- Icon atau emoji yang relevan di bagian atas card
- Judul fitur (misal: Materi Interaktif, Mentor Profesional, Sertifikat Resmi)
- Deskripsi singkat 1–2 kalimat
- Shadow dan sudut membulat: `shadow-md rounded-lg`


---

### 3 Tombol Reusable — Component Styling 

Halaman EduSmart memiliki banyak tombol dengan styling yang sama. **Refactor** agar tidak ada pengulangan class panjang — pilih salah satu pendekatan berikut:

**Pendekatan A — `@apply`:**  
Buat class `.btn-primary` dan `.btn-secondary` di file CSS menggunakan direktif `@apply` dari Tailwind.

```css
/* Contoh */
.btn-primary {
  @apply px-6 py-3 bg-primary text-white rounded-lg font-semibold hover:bg-primary/90 transition;
}

.btn-secondary {
  @apply px-6 py-3 border-2 border-primary text-primary rounded-lg font-semibold hover:bg-primary hover:text-white transition;
}
```

**Pendekatan B — React Component:**  
Buat komponen `<Button>` reusable dengan TypeScript props untuk label dan variant.

```tsx
// Contoh
type ButtonProps = {
  label: string;
  variant?: 'primary' | 'secondary';
};

export default function Button({ label, variant = 'primary' }: ButtonProps) {
  const base = 'px-6 py-3 rounded-lg font-semibold transition';
  const styles = {
    primary: 'bg-primary text-white hover:bg-primary/90',
    secondary: 'border-2 border-primary text-primary hover:bg-primary hover:text-white',
  };
  return <button className={`${base} ${styles[variant]}`}>{label}</button>;
}
```

**Spesifikasi:**
- Minimal 2 variant: *primary* (solid) dan *secondary* (outline/berbeda warna)
- Hover state yang terlihat jelas pada kedua variant
- Transisi animasi dengan class `transition`
- Tombol digunakan di minimal **3 tempat**: Hero, Card Section, dan Footer


---

### 4 Custom Theme — Best Practices 

Daftarkan warna brand EduSmart ke dalam `tailwind.config.js` dan gunakan secara konsisten di seluruh halaman. **Tidak boleh ada nilai hex/rgb yang ditulis langsung di markup.**

**Design token yang harus didefinisikan (nilai warna bebas):**

| Token | Contoh Nilai | Digunakan Di |
|---|---|---|
| `primary` | `#2563EB` | Background hero, tombol utama |
| `secondary` | `#16A34A` | Badge, tombol aksen, hover |
| `background` | `#F8FAFC` | Background halaman dan card |

```js
// tailwind.config.js
module.exports = {
  content: ['./*.html', './src/**/*.{js,ts,jsx,tsx}'],
  theme: {
    extend: {
      colors: {
        primary: '#2563EB',
        secondary: '#16A34A',
        background: '#F8FAFC',
      },
    },
  },
};
```

**Yang harus dikerjakan:**
- Setup proyek Tailwind dengan `tailwind.config.js` menggunakan instalasi npm (bukan CDN)
- Definisikan minimal 3 warna custom di `theme.extend.colors`
- Terapkan token warna tersebut di seluruh halaman (contoh: `bg-primary`, `text-secondary`)
- Tidak boleh ada nilai hex, rgb, atau hsl yang ditulis langsung di markup HTML


---


## 🗂️ Struktur Folder yang Dikumpulkan

```
NRP_Nama_TugasTailwind/
├── index.html              # (atau App.tsx jika React)
├── tailwind.config.js      # Konfigurasi custom theme
├── input.css               # File CSS Tailwind (dengan @apply jika Pendekatan A)
├── output.css              # CSS hasil build Tailwind
├── screenshots/
│   ├── mobile.png          # Tampilan ≤640px
│   ├── tablet.png          # Tampilan 768px
│   └── desktop.png         # Tampilan ≥1024px
└── src/                    # (opsional, jika React)
    └── components/
        └── Button.tsx

---

## 🚀 Cara Menjalankan Proyek

```bash
# 1. Install dependencies
npm install -D tailwindcss

# 2. Generate file konfigurasi
npx tailwindcss init

# 3. Build CSS (mode watch selama development)
npx tailwindcss -i ./input.css -o ./output.css --watch

# 4. Buka index.html di browser
```

> 💡 Pastikan `content` di `tailwind.config.js` sudah mengarah ke file HTML/JSX agar semua class ter-generate dengan benar.

---

## 📚 Referensi

- [Dokumentasi Resmi Tailwind CSS](https://tailwindcss.com/docs)
- [Utility-First Fundamentals](https://tailwindcss.com/docs/utility-first)
- [Responsive Design](https://tailwindcss.com/docs/responsive-design)
- [Reusing Styles dengan @apply](https://tailwindcss.com/docs/reusing-styles)
- [Konfigurasi Theme](https://tailwindcss.com/docs/theme)
- [Modul Pengembangan Frontend Dasar](https://github.com/mtbhprstwan/Modul_Pengembangan-Frontend-Dasar/wiki/Tailwind-CSS)

---

> ❓ Ada pertanyaan? Diskusikan di forum kelas atau buka *Issue* di repositori ini.
