# Risk Register Template

Gunakan register ini di repo/proyek untuk mencatat risiko yang berjalan (bukan pengecualian satu kali; untuk itu gunakan [template pengecualian](exception-template.md)). Proses mengikuti siklus ISO 31000: tetapkan konteks, identifikasi, analisis, evaluasi, perlakuan, lalu pantau dan tinjau ulang secara berkala.

## Prinsip

- Setiap risiko MUST memiliki owner tunggal yang berwenang menerima atau memperlakukan risiko tersebut.
- Rating likelihood dan impact MUST memakai skala yang konsisten di seluruh proyek (mis. 1-5) yang didefinisikan pemilik risiko organisasi, bukan asumsi individu.
- Risiko di atas risk appetite organisasi MUST memiliki rencana perlakuan (mitigate/transfer/avoid/accept) dan tenggat; jangan dibiarkan terbuka tanpa keputusan.
- Register ditinjau ulang saat ada insiden, perubahan arsitektur/regulasi material, dan sekurangnya tiap kuartal untuk Tier 1.
- Risiko yang diterima (accept) MUST disetujui pemilik risiko yang berwenang sesuai levelnya, bukan oleh tim yang menimbulkan risiko tersebut.

## Register

| ID | Risiko | Kategori | Likelihood | Impact | Rating inheren | Kontrol saat ini | Rating residual | Perlakuan | Owner | Tenggat | Status |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [RISK-001] | [deskripsi skenario] | [security/operational/compliance/financial/reputational] | [1-5] | [1-5] | [L×I] | [kontrol eksis] | [L×I setelah kontrol] | [mitigate/transfer/avoid/accept] | [nama/role] | [tanggal] | [Open/In progress/Closed/Accepted] |

## Eskalasi

Risiko dengan rating residual di atas ambang yang ditetapkan pemilik organisasi MUST dieskalasi ke [profil organisasi](organization-profile-template.md) untuk keputusan risk appetite, dan dapat memicu [pengecualian kontrol](exception-template.md) atau [threat model](../02-security/threat-model-template.md) tambahan.

Rujukan: [ISO 31000:2018, Risk management — Guidelines](https://www.iso.org/standard/65694.html) dan [NIST SP 800-30 Rev. 1, Guide for Conducting Risk Assessments](https://csrc.nist.gov/pubs/sp/800/30/r1/final).
