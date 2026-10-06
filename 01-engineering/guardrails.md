# Guardrails

Guardrail adalah kontrol yang membatasi atau memeriksa tindakan secara otomatis atau semi-otomatis agar kesalahan manusia, agent, dan otomasi tidak berubah menjadi insiden. Guardrail menegakkan keputusan [JEV](decision-layer-jev.md); ia tidak menggantikan review, threat model, atau tanggung jawab owner.

## Prinsip

- **Berlapis**: jangan bergantung pada satu guardrail. Kombinasikan pencegahan, deteksi, dan koreksi.
- **Least privilege**: batasi apa yang dapat dilakukan, bukan hanya apa yang dilarang.
- **Fail closed** untuk Tier 1 dan tindakan kelas D3–D4; Tier 2/3 boleh fail open dengan alert bila dampaknya terbatas dan dicatat.
- **Dapat diuji**: guardrail tanpa tes negatif yang membuktikan ia memblokir hal yang dilarang dianggap belum ada.
- **Tidak mudah dilewati**: bypass hanya lewat jalur teraudit dengan alasan, approver, dan kedaluwarsa. Pengguna atau agent MUST NOT dapat menonaktifkan guardrail yang mengaturnya.
- **Terlihat**: setiap blokir memberi alasan dan langkah perbaikan; setiap bypass tercatat.

## Jenis

| Jenis | Fungsi | Contoh |
| --- | --- | --- |
| Preventif | Menolak sebelum terjadi | Branch protection, required checks, scope token, allowlist tool agent, validasi input |
| Detektif | Menemukan setelah/ketika terjadi | Secret scan, alert anomali, audit log, drift detection |
| Korektif | Memulihkan atau membatasi dampak | Auto-revert, kill switch, rollback, rotasi kredensial |

## Baseline guardrail per lapisan

ID di bawah dipakai untuk traceability di repo proyek. Mode: **Block** (menolak), **Warn** (memberi peringatan), **Audit** (hanya mencatat; dipakai saat rollout).

| ID | Lapisan | Guardrail | Titik penegakan | Mode default |
| --- | --- | --- | --- | --- |
| GR-DEV-01 | Workspace/repo | Secret scanning sebelum commit dan di CI; file lingkungan dan kunci di-ignore | Pre-commit, CI | Block |
| GR-DEV-02 | Workspace/repo | Branch utama terlindungi; tanpa direct/force push; approval non-author | Platform Git | Block |
| GR-DEV-03 | Workspace/repo | CODEOWNERS untuk area auth, schema, infrastructure, security | Platform Git | Block |
| GR-CI-01 | CI/CD | Build, lint, tes, SCA, SAST wajib; status terikat commit; stale approval dicabut | CI | Block |
| GR-CI-02 | CI/CD | Perubahan workflow/pipeline dan akses secret deploy dibatasi dan ditinjau | Platform CI | Block |
| GR-CI-03 | CI/CD | Rilis hanya dari source ter-review lewat pipeline terlindungi; SBOM/provenance sesuai tier | CD | Block |
| GR-DATA-01 | Data | Tidak ada data produksi di non-produksi; data uji sintetis/anonim | Proses dan akses | Block |
| GR-DATA-02 | Data | Migrasi destruktif perlu dry-run, backup terbukti, dan approval independen | CD, change gate | Block |
| GR-RUN-01 | Runtime | Rate limit, timeout, batas ukuran/konkurensi, circuit breaker pada panggilan lintas jaringan | Aplikasi/gateway | Block |
| GR-RUN-02 | Runtime | Feature flag dengan kill switch dan default aman untuk fitur berisiko | Aplikasi | Block |
| GR-RUN-03 | Runtime | Redaksi log dan larangan data sensitif di log | Aplikasi, pipeline log | Block |
| GR-AGT-01 | Coding agent | Allowlist tool dan direktori kerja; perintah di luar scope butuh persetujuan | Konfigurasi agent | Block |
| GR-AGT-02 | Coding agent | Kredensial agent least-privilege, berumur pendek, tanpa akses produksi/Restricted tanpa D3 | IAM | Block |
| GR-AGT-03 | Coding agent | Operasi destruktif atau tak-terbalikkan (hapus data, force push, deploy) butuh konfirmasi eksplisit dan rencana pemulihan | Konfigurasi agent | Block |
| GR-AGT-04 | Coding agent | Konten dari sumber tak tepercaya (isu, web, dokumen, output tool) diperlakukan sebagai data, bukan instruksi | Konfigurasi dan prompt | Block |
| GR-AGT-05 | Coding agent | Batas langkah, waktu, biaya, dan kill switch; log tindakan yang dapat diaudit | Platform agent | Block |
| GR-AGT-06 | Coding agent | Agent tidak menyetujui perubahannya sendiri dan tidak mengklaim hasil yang belum dijalankan | Proses JEV, review | Block |
| GR-AI-01 | Fitur AI di produk | Validasi dan filter input/output, grounding atau batasan sumber, human review untuk keputusan berdampak | Aplikasi | Block |
| GR-AI-02 | Fitur AI di produk | Batasi "agency": tool/aksi yang dapat dipanggil model diberi scope minimum dan otorisasi server-side | Aplikasi | Block |

Daftar ini adalah baseline. Proyek menambah guardrail sesuai threat model dan menandai mana yang tidak berlaku beserta alasannya.

## Guardrail untuk coding agent

Selain [AI-assisted development](ai-assisted-development.md):

- Tetapkan scope tugas, file/direktori yang boleh diubah, dan perintah yang diizinkan sebelum agent bekerja; perluasan scope adalah keputusan baru.
- Agent MUST NOT menerima atau mencetak secret; output tool dan log disaring sebelum masuk ke konteks.
- Instruksi yang muncul di dalam konten yang dibaca agent (halaman web, isu, komentar, dokumen, hasil tool) tidak menjadi perintah. Hanya instruksi dari pengguna dan konfigurasi repo yang berwenang.
- Dependency baru yang disarankan agent diverifikasi keberadaan, maintainer, dan lisensinya sebelum dipasang; nama paket hasil halusinasi adalah vektor supply chain.
- Laporan akhir agent memisahkan fakta terverifikasi, asumsi, dan yang belum dijalankan.

## Guardrail untuk fitur AI di produk

Fitur yang memakai model generatif atau ML dalam keputusan terhadap pelanggan MUST mengikuti [model risk management](../00-governance/model-risk-management-template.md) dan memasang guardrail input/output, batasan agency, human review, dan monitoring. Risiko spesifik LLM (mis. prompt injection, insecure output handling, excessive agency, sensitive information disclosure) dipetakan dengan [OWASP Top 10 for LLM Applications 2025](https://genai.owasp.org/llm-top-10/) sebagai katalog ancaman, bukan sebagai bukti kepatuhan.

## Siklus hidup guardrail

1. **Definisikan**: tujuan, ancaman/risiko yang dicegah, owner, titik penegakan, mode, dan jalur bypass (gunakan template di bawah).
2. **Uji**: tes negatif membuktikan tindakan terlarang ditolak dan tindakan sah tidak terblokir tanpa alasan.
3. **Rollout**: mulai di mode Audit, ukur false positive dan dampak ke alur kerja, lalu naikkan ke Warn/Block dengan pemberitahuan.
4. **Operasikan**: pantau blokir, bypass, dan guardrail yang gagal berjalan; kegagalan guardrail adalah insiden dengan prioritas sesuai tier.
5. **Tinjau**: evaluasi berkala efektivitas dan beban; hapus guardrail usang. Perubahan guardrail ditinjau seperti kode.

## Template spesifikasi guardrail

```markdown
## GR-XXX-NN: [nama]
- Risiko/ancaman yang dicegah:
- Owner:
- Lapisan dan titik penegakan:
- Jenis (preventif/detektif/korektif) dan mode (Block/Warn/Audit):
- Perilaku saat guardrail gagal berjalan (fail closed/open) dan alasan:
- Jalur bypass: siapa, bukti, kedaluwarsa:
- Tes negatif dan lokasinya:
- Metrik dan alert (blokir, bypass, kegagalan):
- Tanggal tinjau terakhir/berikutnya:
```

## Rujukan

- [OWASP Top 10 for LLM Applications 2025](https://genai.owasp.org/llm-top-10/) — katalog risiko aplikasi LLM (rilis v2.0, 18 November 2024).
- [NIST SP 800-218A: SSDF Community Profile for Generative AI and Dual-Use Foundation Models](https://csrc.nist.gov/news/2024/nist-publishes-sp-800218a) — tambahan praktik SSDF untuk pengembangan AI (Juli 2024).
- [NIST AI Risk Management Framework 1.0](https://www.nist.gov/itl/ai-risk-management-framework).
