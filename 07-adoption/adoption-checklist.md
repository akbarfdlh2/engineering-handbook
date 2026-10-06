# Adoption dan Production Readiness Checklist

Isi checklist ini di repo proyek. Tautkan bukti internal yang sesuai izin akses; jangan menaruh secret, data pribadi, laporan pentest sensitif, atau rincian incident pada repo publik.

## Ownership dan scope

- [ ] Product/business, engineering, security, data/privacy, dan design/accessibility owner ditetapkan sesuai produk.
- [ ] Data class dan Tier 1/2/3 ditetapkan dengan alasan.
- [ ] Versi/tag handbook dicatat dan akses ke versi tersebut berfungsi.
- [ ] Stack, diagram system/data flow, trust boundary, environment, dan third-party dependencies terdokumentasi.
- [ ] Source tree mengikuti [struktur repository](../01-engineering/repository-structure.md) atau pengecualiannya dicatat dengan alasan.
- [ ] Hukum, kontrak, residency, retention, dan kewajiban customer yang relevan dipetakan oleh owner yang tepat.
- [ ] [Risk register](../00-governance/risk-register-template.md) proyek dibuat dan risiko di atas risk appetite memiliki rencana perlakuan.

## Product dan design

- [ ] PRD/feature specification menjelaskan scope, acceptance criteria, error/recovery states, dan metrik.
- [ ] Design system produk ditautkan; WCAG 2.2 AA target dan hasil accessibility review dicatat untuk UI.
- [ ] PRD lolos [readiness checklist](../03-product/prd-readiness-checklist.md) dan rekomendasi arsitektur dicatat dengan [panduan pemilihan arsitektur](../04-architecture/architecture-selection-guide.md).
- [ ] Login/MFA, empty/loading/error, keyboard, mobile, localization, dan destructive-action flows ditinjau bila berlaku.

## Security dan data

- [ ] MFA aktif bagi seluruh akun manusia; admin/production/Restricted access memakai phishing-resistant MFA.
- [ ] Enrollment, lost-device recovery, authenticator changes, session revocation, break-glass, dan access review diuji.
- [ ] Otorisasi server-side, tenant isolation, secrets, key management, logging redaction, dan data deletion diperiksa.
- [ ] Threat model dibuat sesuai tier dan perubahan; risiko residual memiliki penerima yang berwenang.
- [ ] Dependency/vendor review, secret/SCA/SAST scanning, dan vulnerability SLA berjalan.
- [ ] [Vendor due diligence questionnaire](../02-security/vendor-due-diligence-questionnaire.md) selesai untuk vendor Tier 1/2; [jadwal retensi data](../02-security/data-retention-schedule-template.md) dan [matriks segregation of duties](../02-security/segregation-of-duties-matrix-template.md) terisi.
- [ ] Jika proyek memakai model statistik/ML/AI untuk keputusan bisnis (credit, fraud, pricing, atau dampak pelanggan lain), [model risk management](../00-governance/model-risk-management-template.md) diisi dan divalidasi sesuai tier.
- [ ] Public repo hanya berisi data Public dan tidak memiliki secret, environment files, customer content, atau internal incident detail.

## Engineering dan release

- [ ] Main branch dilindungi; direct push dan force-push dinonaktifkan; required reviews dan CI checks aktif.
- [ ] Tes yang relevan, lint/static analysis, build, secret scan, dependency scan, dan security tests lulus.
- [ ] Migration, compatibility, rollback/recovery, feature flags, dan deployment owner ditetapkan.
- [ ] Fase dan gate [SDLC](../01-engineering/sdlc.md) dipetakan; keputusan rilis dan merge berisiko memakai [JEV](../01-engineering/decision-layer-jev.md).
- [ ] [Guardrails](../01-engineering/guardrails.md) baseline aktif (repo, CI, agent) dan teruji dengan tes negatif.
- [ ] Deteksi [vulnerability/bug/debt](../01-engineering/defect-and-debt-detection.md) berjalan dan [debt register](../00-governance/technical-debt-register-template.md) dipelihara.
- [ ] Release dapat ditelusuri ke reviewed commit/build; Tier 1 memiliki SBOM/provenance dan independent security assessment.
- [ ] Tidak ada temuan Critical yang belum ditutup. Temuan High ditutup atau memiliki pengecualian yang sah dan berjangka.

## Operations

- [ ] SLI/SLO, alert threshold, on-call/escalation, incident commander, dan runbook tersedia.
- [ ] RTO/RPO disetujui pemilik bisnis; backup terenkripsi dan restore diuji terhadap target.
- [ ] Incident response, customer/privacy notification, credential revocation, dan post-incident review path diketahui owner.
- [ ] Tier 1 telah menjalani incident tabletop serta restore exercise sesuai jadwal.
- [ ] Tier 1 memiliki [business continuity plan](../06-operations/business-continuity-plan-template.md) dengan BIA dan bukti tabletop exercise.

## Gap dan approval

| Gap/control | Risiko | Mitigasi sementara | Owner | Due date | Exception approval/evidence |
| --- | --- | --- | --- | --- | --- |
| [gap] | [dampak] | [mitigasi] | [owner] | [tanggal] | [tautan] |

Production release tidak boleh melewati kontrol MUST yang belum dipenuhi tanpa pengecualian berjangka yang disetujui penerima risiko yang tepat; kewajiban hukum/kontrak dan containment insiden tidak dapat dikecualikan.
