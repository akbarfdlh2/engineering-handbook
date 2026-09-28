# Contributing

## Usulkan perubahan standar

Buka pull request dengan:

- masalah atau risiko yang ditangani;
- perubahan persyaratan dan alasan;
- siapa dan repo mana yang terdampak;
- sumber primer atau bukti yang mendukung;
- perubahan MUST/SHOULD/MAY, pengecualian, dan panduan migrasi;
- pembaruan `CHANGELOG.md`.

## Review dan penerbitan

- Perubahan umum memerlukan minimal satu reviewer engineering.
- Perubahan authentication, security, privacy, cryptography, atau incident response memerlukan review security owner.
- Perubahan accessibility/design system memerlukan review design/accessibility owner.
- Tidak ada self-approval. Pastikan internal links dan source links tetap benar.
- Persetujuan versi wajib diberikan owner organisasi setelah `organization-profile-template.md` dilengkapi. Gunakan tag release `vMAJOR.MINOR.PATCH` dan catat perubahan yang berdampak pada repo pengguna.

## Checklist sebelum publikasi/tag

- [ ] Pemilik standar dan versi yang akan dirilis disetujui.
- [ ] Profil organisasi dan control register ditinjau; detail internal sensitif tidak dipublikasikan.
- [ ] Tautan internal/eksternal, versi rujukan, dan tanggal tinjau diperiksa.
- [ ] `SECURITY.md` memiliki jalur private vulnerability reporting yang aktif dan jelas.
- [ ] Branch protection, required review, dan CI policy repo diatur.
- [ ] Changelog diperbarui; tag dan release notes sesuai perubahan.

## Informasi sensitif

Jangan membuka isu/PR berisi secret, data customer, laporan vulnerability yang belum diperbaiki, detail incident, atau bukti audit yang dibatasi. Gunakan kanal privat organisasi.
