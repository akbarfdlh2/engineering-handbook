# Adopsi di Repo Proyek

## Struktur dokumen proyek yang disarankan

Untuk source tree, gunakan [panduan struktur repository](../01-engineering/repository-structure.md). Contoh di bawah hanya memetakan dokumentasi proyek.

```text
AGENTS.md
docs/
  product/PRD.md
  product/features/<feature>.md
  architecture/README.md
  architecture/adr/ADR-0001-<judul>.md
  design-system/README.md
  engineering/standards.md
  operations/runbooks/<service>.md
```

Gunakan file yang dibutuhkan saja. Setiap proyek mencatat owner, stack/perintah validasi, tier, versi handbook, dan pengecualian di `AGENTS.md` atau `docs/engineering/standards.md`.

## Agar agent benar-benar membaca standar

Tag atau mention repo publik dapat membantu menemukan sumber, tetapi tidak menjamin setiap agent otomatis memuat dokumennya. Untuk pemakaian rutin:

1. Tambahkan instruksi di `AGENTS.md` proyek yang menautkan handbook dan menyebut file relevan.
2. Pin tag atau commit yang sudah ditinjau; jangan bergantung pada isi `main` yang dapat berubah.
3. Untuk akses offline dan hasil yang konsisten, tambahkan handbook sebagai Git submodule, misalnya `standards/engineering-handbook`, lalu minta agent membaca file di sana.
4. Jika submodule tidak dipakai, pastikan agent memiliki akses ke repo public/network dan minta secara eksplisit membaca tautan standar sebelum mengubah kode.
5. Simpan standar proyek, konteks produk, dan pengecualian tetap di proyek, bukan di handbook global.

Template ada di [project AGENTS.md](agents-template.md). Setiap repo mengadopsi kontrol secara bertahap; jangan mengklaim compliance hanya karena menautkan handbook.

Gunakan [adoption dan production readiness checklist](adoption-checklist.md) untuk merekam keputusan, gap, evidence, dan approval.

Untuk menerapkan standar di workflow harian, gunakan [template pull request](pull-request-template.md) dan [checklist code review](code-review-checklist.md). Stack khusus didokumentasikan memakai [stack guide template](../01-engineering/stack-guide-template.md).
