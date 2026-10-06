# PRD Readiness Checklist (Definition of Ready)

Gunakan checklist ini sebelum PRD berstatus Approved dan sebelum pekerjaan build dimulai. Item yang tidak berlaku ditandai dengan alasan; item yang tidak terpenuhi dicatat sebagai gap dengan owner dan tenggat.

## Masalah dan nilai

- [ ] Masalah, pengguna, dan dampak didukung bukti bersumber; asumsi dipisahkan dari fakta.
- [ ] Alternatif, termasuk tidak membangun, dipertimbangkan dan alasannya dicatat.
- [ ] Hasil punya metrik, baseline, target, sumber data, dan owner pengukuran.

## Ruang lingkup dan kebutuhan

- [ ] In scope dan out of scope eksplisit.
- [ ] Setiap kebutuhan Must punya ID stabil, acceptance criteria yang dapat diverifikasi, dan skenario kegagalan/penolakan.
- [ ] Tidak ada kata ambigu tanpa definisi (mis. "cepat", "aman", "mudah") yang dipakai sebagai kriteria.
- [ ] Dependency, asumsi, dan kendala tercatat beserta status dan pemiliknya.

## Risiko, security, dan privacy

- [ ] Tier ditetapkan dengan alasan; klasifikasi data dan aktor jelas.
- [ ] Authorization, tenant boundary, dan abuse cases dibahas; threat model ada bila dipersyaratkan tier.
- [ ] Retensi, consent, audit, pihak ketiga, dan kewajiban hukum/kontrak sudah divalidasi oleh pihak yang berwenang.
- [ ] Jika ada komponen AI/model: model risk management dan guardrails direncanakan.

## Pengalaman, kualitas, dan operasi

- [ ] Keadaan error/empty/loading/recovery, aksesibilitas, dan bahasa dijelaskan.
- [ ] Persyaratan nonfungsional dinyatakan sebagai skenario terukur dengan alasan.
- [ ] Rollout, feature flag, rollback, migrasi data, dan metrik penghentian ditentukan.
- [ ] Rekomendasi arsitektur atau alasan tidak diperlukan dicatat.

## Persetujuan

- [ ] Product, engineering, dan (sesuai tier) security/privacy menyetujui; tidak ada self-approval atas risiko sendiri.
- [ ] Pertanyaan terbuka punya pemilik dan tenggat; tidak ada yang memblokir build tanpa rencana.
- [ ] Keputusan persetujuan dicatat memakai [JEV](../01-engineering/decision-layer-jev.md) untuk Tier 1/2.
