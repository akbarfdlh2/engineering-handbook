# Control Mapping Template (ISO/IEC 27001 dan SOC 2)

Template ini membantu proyek memetakan [control register](control-register.md) ke kerangka eksternal yang sering diminta auditor/pelanggan. Ini BUKAN sertifikasi atau bukti kepatuhan; pemetaan hanya pada tingkat kategori/keluarga kontrol dan harus diverifikasi terhadap teks resmi standar (berbayar/dilisensikan) dan/atau auditor bersertifikat sebelum diklaim ke pihak eksternal.

## Cara pakai

1. Salin tabel dan isi kolom "Bukti proyek" dengan tautan internal.
2. Verifikasi nomor klausul/kriteria persis terhadap edisi standar yang dilisensikan organisasi; kolom di sini hanya indikatif.
3. Tandai gap pada [adoption checklist](../07-adoption/adoption-checklist.md) dan/atau [risk register](risk-register-template.md) bila kontrol belum terpenuhi.

## Pemetaan

| ID control register | Kontrol | ISO/IEC 27001:2022 Annex A (kategori) | SOC 2 Trust Services Criteria | Bukti proyek |
| --- | --- | --- | --- | --- |
| GOV-01 | Owner dan tier | A.5 Organizational | CC1 — Control Environment | [tautan] |
| GOV-02 | Pengecualian | A.5 Organizational | CC1, CC9 — Risk Mitigation | [tautan] |
| GOV-03 | Risk register | A.5 Organizational | CC3 — Risk Assessment | [tautan] |
| ENG-01 | Review perubahan | A.5, A.8 Technological | CC8 — Change Management | [tautan] |
| ENG-02 | Quality gates | A.8 Technological | CC8 — Change Management | [tautan] |
| ENG-03 | Release traceability | A.5, A.8 | CC8 — Change Management | [tautan] |
| ENG-04 | Regulated change management | A.5, A.8 | CC8 — Change Management | [tautan] |
| IAM-01 | MFA untuk manusia | A.5, A.8 | CC6 — Logical and Physical Access | [tautan] |
| IAM-02 | Phishing-resistant untuk privileged | A.5, A.8 | CC6 — Logical and Physical Access | [tautan] |
| IAM-03 | Enrollment/recovery/sesi | A.5, A.8 | CC6 — Logical and Physical Access | [tautan] |
| IAM-04 | Lifecycle dan access review | A.5, A.8 | CC6 — Logical and Physical Access | [tautan] |
| IAM-05 | Service identities | A.5, A.8 | CC6 — Logical and Physical Access | [tautan] |
| IAM-06 | Authorization/tenant isolation | A.5, A.8 | CC6 — Logical and Physical Access | [tautan] |
| IAM-07 | Segregation of duties | A.5 Organizational, A.6 People | CC5 — Control Activities | [tautan] |
| DATA-01 | Klasifikasi dan retensi | A.5 Organizational | CC6, Privacy (bila dalam ruang lingkup) | [tautan] |
| DATA-02 | Data retention schedule | A.5 Organizational | C1 — Confidentiality / Privacy | [tautan] |
| SEC-01 | Threat model | A.5, A.8 | CC3 — Risk Assessment | [tautan] |
| SEC-02 | Secure build/supply chain | A.5, A.8 | CC8 — Change Management | [tautan] |
| SEC-03 | Vulnerability SLA | A.8 Technological | CC7 — System Operations | [tautan] |
| SEC-04 | Keys dan secrets | A.8 Technological | CC6 — Logical and Physical Access | [tautan] |
| SEC-05 | Third-party risk | A.5 Organizational | CC9 — Risk Mitigation | [tautan] |
| SEC-06 | Logging dan incident response | A.5, A.8 | CC7 — System Operations | [tautan] |
| SEC-07 | Independent assessment | A.5 Organizational | CC4 — Monitoring Activities | [tautan] |
| SEC-08 | Vendor due diligence | A.5 Organizational | CC9 — Risk Mitigation | [tautan] |
| OPS-01 | Reliability target | A.5 Organizational | A1 — Availability | [tautan] |
| OPS-02 | Backup dan restore | A.5, A.8 | A1 — Availability | [tautan] |
| OPS-03 | Business continuity | A.5 Organizational | A1 — Availability | [tautan] |
| PROD-01 | Kebutuhan produk | A.5 Organizational | CC1 — Control Environment | [tautan] |
| DES-01 | Aksesibilitas UI | Di luar Annex A umum; catat sebagai kontrol tambahan produk | Di luar TSC umum; catat sebagai kontrol tambahan produk | [tautan] |
| AI-01 | Model risk management | A.5, A.8 | CC3 — Risk Assessment | [tautan] |

Rujukan: [ISO/IEC 27001:2022, Information security management systems](https://www.iso.org/standard/27001) dan [AICPA 2017 Trust Services Criteria (revised 2022 points of focus)](https://www.aicpa-cima.com/resources/download/get-description-criteria-for-your-organizations-soc-2-r-report).
