# Prinsip Design System

## Fondasi dan token

- Mulai dari tujuan produk, audiens, brand, platform, dan konteks penggunaan.
- Gunakan tiga lapisan: primitive tokens, semantic tokens, component tokens. UI menggunakan token semantik/komponen, bukan nilai warna atau spacing acak.
- Token dinamai berdasarkan makna/fungsi (`color.text.primary`, `space.control.md`), memiliki nilai, konteks, contoh, dan aturan tema.
- Dokumentasikan tipografi, warna, spacing, grid, radius, elevation, iconography, motion, breakpoint, dan dukungan dark/high-contrast mode bila relevan.

## Komponen dan pola

- Setiap komponen memiliki tujuan, kapan digunakan, API/varian, state, aturan responsive, accessibility behavior, contoh benar/salah, dan status Draft/Stable/Deprecated.
- State penting meliputi default, hover, focus-visible, active, disabled, loading, success, empty, dan error sesuai komponen.
- Gunakan elemen semantik dan pola keyboard yang dapat diprediksi; seluruh aksi utama harus dapat dicapai dengan keyboard.
- Jangan menjadikan warna satu-satunya pembawa makna. Focus indicator harus terlihat dan tidak tertutup komponen lain.
- Form menjelaskan label, format, error, koreksi, dan dampak input. Jangan menghapus input pengguna saat error.
- Motion harus menghormati `prefers-reduced-motion` dan tidak menghalangi pemahaman atau penyelesaian tugas.

## Aksesibilitas dan verifikasi

- Target web MUST memenuhi WCAG 2.2 AA pada halaman/alur yang termasuk ruang lingkup.
- Teks normal memiliki contrast ratio minimal 4.5:1; teks besar minimal 3:1; batas komponen dan indikator visual penting minimal 3:1 sesuai kriteria WCAG.
- Target sentuh web MUST memenuhi minimum WCAG 2.2 2.5.8 (24 × 24 CSS px atau pengecualian yang diizinkan kriterianya); untuk kontrol yang sering digunakan, target 44 × 44 CSS px SHOULD dipakai bila layout memungkinkan.
- Authentication MUST tidak mengandalkan tes kognitif yang tidak perlu dan harus mendukung password manager, paste, serta mekanisme aksesibel.
- Review mencakup keyboard-only, zoom/reflow, screen reader smoke check, contrast, error states, touch target, dan reduced motion sesuai risiko.
- Otomatisasi accessibility membantu tetapi tidak menggantikan pemeriksaan manual dengan teknologi bantu.

## Pemeliharaan

- Perubahan token/komponen breaking memerlukan deprecation dan panduan migrasi.
- Design review dan code review harus membandingkan implementasi terhadap source design yang disetujui.
- Jangan mendokumentasikan komponen sebagai tersedia bila belum ada implementasi yang dirawat.

Rujukan: [W3C WCAG 2.2](https://www.w3.org/TR/WCAG22/) dan [What's new in WCAG 2.2](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/).
