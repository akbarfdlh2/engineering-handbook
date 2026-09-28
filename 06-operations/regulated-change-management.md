# Regulated Change Management (CAB)

Dokumen ini melengkapi [git dan code review](../01-engineering/git-and-code-review.md) dan [environments dan release management](environments-and-release-management.md) untuk perubahan yang memerlukan gate persetujuan formal di luar review kode: perubahan infrastruktur produksi, konfigurasi jaringan/security, dan perubahan pada sistem teregulasi/Tier 1.

## Klasifikasi perubahan

| Kelas | Contoh | Approval |
| --- | --- | --- |
| Standard | Perubahan berulang, berisiko rendah, prosedurnya sudah pre-approved | Pre-approved oleh engineering owner; tidak perlu CAB per kejadian |
| Normal | Perubahan terencana dengan risiko material | Review CAB sebelum implementasi |
| Emergency | Mengurangi dampak insiden aktif | Jalur dipercepat sesuai [emergency change](../01-engineering/git-and-code-review.md#emergency-change); retrospective review wajib |

## Change Advisory Board

- Komposisi minimum: engineering owner, security owner (untuk perubahan security/infrastructure/auth), dan business/product owner untuk perubahan Tier 1.
- CAB MUST menilai dampak, rencana rollback, rencana komunikasi, jadwal (freeze window), dan hasil test sebelum menyetujui perubahan Normal.
- Perubahan yang ditolak MUST dicatat alasan dan syarat resubmission.

## Checklist pra-implementasi

- [ ] Rencana rollback terbukti dapat dijalankan.
- [ ] Dampak terhadap SLO/pelanggan dinilai dan komunikasi disiapkan bila perlu.
- [ ] Tidak bertabrakan dengan freeze window (mis. periode puncak bisnis) tanpa pengecualian yang disetujui.
- [ ] Owner pemantauan pasca-implementasi ditetapkan.

## Freeze window

Tetapkan periode freeze (mis. akhir tahun finansial, event bisnis besar) di mana perubahan Normal non-esensial ditunda; perubahan darurat tetap mengikuti jalur emergency.

## Setelah implementasi

- Post-implementation review MUST mencatat hasil aktual vs rencana, insiden yang timbul, dan pembaruan ke runbook/dokumentasi.
- Audit trail (siapa approve, kapan, apa yang berubah) MUST dapat ditelusuri untuk kebutuhan audit eksternal.

Prinsip mengikuti praktik change enablement yang umum dipakai kerangka manajemen layanan (mis. ITIL 4); [environments dan release management](environments-and-release-management.md) tetap menjadi kontrol pelaksana teknisnya.
