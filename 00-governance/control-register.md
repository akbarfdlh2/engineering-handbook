# Control Register

Register ini memberi ID stabil dan lokasi persyaratan kanonis untuk perencanaan/adopsi. Persyaratan rinci tetap berada di dokumen tujuan; register ini tidak menggantikan bukti implementasi atau control mapping audit.

| ID | Kontrol | Persyaratan kanonis | Bukti proyek yang disimpan internal |
| --- | --- | --- | --- |
| GOV-01 | Owner dan tier | [Peran minimum](README.md#peran-minimum), [profil organisasi](organization-profile-template.md) | Owner, klasifikasi data, tier, approval |
| GOV-02 | Pengecualian | [Pengecualian](README.md#pengecualian), [template](exception-template.md) | Risk acceptance, mitigasi, due date, approval |
| ENG-01 | Review perubahan | [Git dan code review](../01-engineering/git-and-code-review.md) | Branch rules, CODEOWNERS, PR approvals |
| ENG-02 | Quality gates | [Testing dan quality gates](../01-engineering/testing-and-quality-gates.md) | CI policy, hasil pipeline, security scan |
| ENG-03 | Release traceability | [Release management](../06-operations/environments-and-release-management.md) | Commit/build/deploy record, rollback plan |
| IAM-01 | MFA untuk manusia | [Kebijakan login](../02-security/identity-and-authentication.md#kebijakan-login) | IdP/app enforcement dan enrollment report |
| IAM-02 | Phishing-resistant untuk privileged | [Kebijakan login](../02-security/identity-and-authentication.md#kebijakan-login) | Authenticator policy, exception register |
| IAM-03 | Enrollment/recovery/sesi | [Pemulihan akun](../02-security/identity-and-authentication.md#enrollment-dan-pemulihan-akun), [sesi](../02-security/identity-and-authentication.md#sesi-dan-proteksi-login) | Test evidence, recovery runbook, revocation proof |
| IAM-04 | Lifecycle dan access review | [SSO dan akun mesin](../02-security/identity-and-authentication.md#sso-dan-akun-mesin) | Provision/deprovision logs, review record |
| IAM-05 | Service identities | [SSO dan akun mesin](../02-security/identity-and-authentication.md#sso-dan-akun-mesin) | Owner, scope, credential/workload identity inventory |
| IAM-06 | Authorization/tenant isolation | [Access control](../02-security/access-control.md) | Negative tests, role matrix, tenant isolation evidence |
| DATA-01 | Klasifikasi dan retensi | [Data protection](../02-security/data-protection-and-privacy.md) | Data inventory, retention/deletion rules |
| SEC-01 | Threat model | [Threat model](../02-security/threat-model-template.md) | Approved model and tracked mitigations |
| SEC-02 | Secure build/supply chain | [Secure development](../02-security/secure-development.md) | CI scanning, SBOM/provenance per tier |
| SEC-03 | Vulnerability SLA | [Vulnerability management](../02-security/vulnerability-management.md) | Findings, severity, due dates, retest, exceptions |
| SEC-04 | Keys dan secrets | [Cryptography/key management](../02-security/cryptography-and-key-management.md) | Key inventory, rotation/revocation test, access audit |
| SEC-05 | Third-party risk | [Third-party risk](../02-security/third-party-risk.md) | Vendor assessment, contract, data flow, exit plan |
| SEC-06 | Logging dan incident response | [Logging/incident response](../02-security/logging-monitoring-and-incidents.md) | Redaction tests, alert owner, runbook/exercise |
| SEC-07 | Independent assessment | [Secure development](../02-security/secure-development.md) | Assessment scope, report access, remediation closure |
| OPS-01 | Reliability target | [Reliability/recovery](../06-operations/reliability-backup-and-recovery.md) | Approved SLI/SLO, RTO/RPO, alerts |
| OPS-02 | Backup dan restore | [Reliability/recovery](../06-operations/reliability-backup-and-recovery.md) | Backup config, restore results, integrity checks |
| PROD-01 | Kebutuhan produk | [PRD template](../03-product/prd-template.md) | Approved PRD and acceptance criteria |
| DES-01 | Aksesibilitas UI | [Design principles](../05-design-system/design-principles.md) | WCAG review, remediation, exception if any |

Simpan bukti sensitif pada sistem akses-terbatas dan tautkan ID bukti internal. Jangan menaruh laporan pentest, temuan exploit, data pengguna, credential, atau log sensitif di repo handbook publik.
