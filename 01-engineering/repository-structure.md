# Struktur Repository

Struktur harus membantu orang menemukan kode, tes, konfigurasi, dan dokumen dengan cepat. Ikuti konvensi framework/toolchain yang resmi; gunakan contoh di sini sebagai baseline, bukan alasan untuk membangun ulang struktur framework.

## Prinsip

- Root repository MUST menjelaskan tujuan, cara menjalankan, verifikasi, deployment/operasi yang penting, owner, serta lokasi dokumentasi.
- Nama folder harus menyatakan tanggung jawab atau batas deployable; hindari folder `misc`, `common2`, atau lapisan generik tanpa pemilik yang jelas.
- Pisahkan aplikasi yang dapat dirilis sendiri (`apps/`, `services/`) dan library yang dipakai bersama (`packages/`, `libs/`) hanya jika memang ada batas tersebut.
- Kode domain/business tidak bergantung langsung pada transport, framework UI, atau provider eksternal bila pemisahan itu mengurangi coupling dan memudahkan pengujian.
- Tes harus mudah dipetakan ke kode yang diuji; gunakan konvensi yang sudah ditetapkan framework.
- Ikuti satu pola penamaan dan casing per toolchain. Jangan memindahkan file atau mengganti nama folder tanpa alasan dan pembaruan import/build/docs.
- Jangan simpan secrets, production data, dependency cache, build output, IDE state, atau artefak sementara di source control kecuali ada alasan eksplisit.

## Bentuk repository aplikasi

```text
repo-root/
  README.md
  AGENTS.md
  CHANGELOG.md                 # bila proyek merilis versi
  docs/
    README.md
    product/
    architecture/
      adr/
    design-system/             # bila proyek memiliki UI
    engineering/
    operations/
      runbooks/
  src/                         # atau folder resmi framework
  tests/                       # atau test folders sesuai toolchain
  migrations/                  # bila schema/data versioned di sini
  scripts/                     # hanya script yang dirawat
  infra/                       # hanya infrastructure-as-code
```

Tidak semua folder harus ada. Jangan membuat folder kosong; gunakan lokasi resmi framework bila berbeda dari contoh.

## Bentuk monorepo

```text
repo-root/
  apps/                        # deployable user-facing applications
  services/                    # deployable backend services, bila diperlukan
  packages/                    # library bersama dengan owner dan kontrak jelas
  docs/                        # standar lintas aplikasi dan arsitektur
  infra/                       # environment/deployment code
```

Monorepo MUST memiliki owner dan quality gates per deployable unit; dependency antar package harus eksplisit. Jangan memecah repository atau membuat shared package sebelum ada kebutuhan reuse/deployment/ownership yang nyata.

## Dokumentasi proyek

```text
docs/
  README.md
  product/PRD.md
  product/features/<feature>.md
  architecture/README.md
  architecture/adr/ADR-0001-<decision>.md
  design-system/README.md
  engineering/standards.md
  operations/runbooks/<service>.md
```

Simpan isi sesuai template di [Product](../03-product/README.md), [Architecture](../04-architecture/README.md), [Design System](../05-design-system/README.md), dan [Operations](../06-operations/README.md). `docs/README.md` harus menjadi indeks dokumen aktif. Pindahkan atau tandai dokumen usang; hindari salinan template handbook yang tidak diperbarui.

## Instruksi agent

- Root `AGENTS.md` menjelaskan konteks repo, stack, validasi, batas data/operasi, handbook yang dipin, dan jalur dokumentasi.
- Gunakan `AGENTS.md` bertingkat hanya untuk subfolder yang benar-benar memiliki aturan berbeda; jangan salin instruksi yang sama ke setiap folder.
- Instruksi agent bukan pengganti dokumentasi produk, kontrol akses, atau quality gates yang ditegakkan tooling.
