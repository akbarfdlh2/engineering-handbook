# Decision Layer: Judge–Evaluate–Verify (JEV)

JEV adalah istilah yang didefinisikan handbook ini, bukan standar eksternal. Decision layer JEV adalah lapisan keputusan yang berada di antara **pengusul** (manusia, coding agent, scanner, atau otomasi) dan **tindakan** (merge, rilis, auto-remediation, persetujuan pengecualian, penutupan temuan, rekomendasi arsitektur). Tujuannya agar keputusan konsisten, berbasis bukti, dapat diaudit, dan tidak bergantung pada keyakinan pengusul.

Tiga langkah, selalu berurutan:

1. **Judge** — mengklasifikasikan usulan: seberapa berisiko dan seberapa besar otonomi yang boleh dipakai.
2. **Evaluate** — mengumpulkan dan menilai bukti terhadap kriteria yang sudah ditetapkan sebelumnya.
3. **Verify** — mengonfirmasi secara independen bahwa bukti benar, segar, dan hasil tindakan sesuai yang diklaim.

Dokumen ini berlaku bagi keputusan manusia maupun agent. Untuk model yang menjadi bagian keputusan produk terhadap pelanggan, gunakan [model risk management](../00-governance/model-risk-management-template.md); JEV mengatur keputusan proses engineering, bukan menggantikan validasi model.

## Aturan inti

- Keputusan MUST fail closed: bukti hilang, usang, tidak dapat diverifikasi, atau verifier tidak tersedia berarti hasilnya bukan lulus.
- Pengusul MUST NOT menjadi verifier atas usulannya sendiri. Untuk agent, konteks, sesi, atau model yang sama tidak dihitung independen; dua agent yang setuju bukan bukti kebenaran.
- Kriteria dan kelas keputusan MUST ditetapkan sebelum melihat hasil, agar kriteria tidak diubah menyesuaikan hasil.
- Ambiguitas pada Judge menaikkan kelas keputusan, tidak menurunkannya.
- Setiap keputusan di atas kelas D0 MUST menghasilkan [catatan keputusan](#catatan-keputusan).
- Override manusia atas verdict DENY atau ESCALATE MUST dicatat dengan alasan, pemberi approval, dan tanggal kedaluwarsa, mengikuti [pengecualian](../00-governance/README.md#pengecualian).

## 1. Judge: klasifikasi

Judge menetapkan **kelas keputusan** dari faktor berikut. Nilainya kualitatif; organisasi menetapkan pemetaan rinci di profil organisasi.

| Faktor | Pertanyaan |
| --- | --- |
| Tier dan data | Tier berapa, data apa yang tersentuh? |
| Reversibilitas | Dapat dibatalkan cepat dan utuh, atau merusak/permanen? |
| Blast radius | Satu pengguna, satu tenant, seluruh sistem, atau pihak ketiga? |
| Privilege | Mengubah akses, kunci, identitas, atau batas trust? |
| Efek eksternal | Mengirim data keluar, membayar, menghubungi pelanggan, memanggil produksi? |
| Kebaruan dan keyakinan | Pola yang sudah terbukti atau pertama kali? Seberapa kuat bukti awal? |
| Pengusul | Manusia berpengalaman, agent, atau scanner (tingkat false positive yang diketahui)? |

| Kelas | Arti | Contoh | Persyaratan |
| --- | --- | --- | --- |
| D0 | Otonom, reversibel, dampak lokal | Format kode, update dokumentasi, perbaikan lint | Guardrails otomatis; log ringkas |
| D1 | Otonom dengan pemberitahuan | Update dependency patch yang lolos tes, perbaikan di cabang kerja | Evaluate otomatis lulus; pemilik diberi tahu; mudah di-revert |
| D2 | Perlu approval manusia | Merge ke branch utama, rilis Tier 3/2 biasa, penutupan temuan | Evaluate + verifier independen + approval satu reviewer yang memahami area |
| D3 | Dual approval dan owner domain/security | Rilis Tier 1, perubahan auth/kripto/privilege, migrasi destruktif, pengecualian risiko tinggi | Dua approver, satu domain/security owner; rencana rollback terbukti |
| D4 | Tidak boleh diotomasi | Operasi destruktif produksi tanpa rencana pemulihan, akses ke data Restricted oleh agent yang tidak disetujui | Hanya melalui prosedur manusia yang diaudit atau ditolak |

## 2. Evaluate: bukti terhadap kriteria

- Kriteria berupa **hard gate** (harus lulus; mis. tes wajib, secret scan, tidak ada temuan critical terbuka) dan **rubrik** (penilaian kualitatif dengan alasan; mis. kejelasan rollback, kecukupan tes negatif). Hindari satu skor numerik buram yang menutupi hard gate yang gagal.
- Bukti MUST terikat pada artefak yang diputuskan (commit SHA, digest build, versi dokumen) dan dihasilkan dari eksekusi yang teramati. Beri label status bukti:
  - **Verified**: teramati langsung dalam konteks keputusan ini.
  - **Reported**: berasal dari sumber lain dan belum diperiksa ulang.
  - **Assumed**: asumsi atau inferensi tanpa pengamatan.
- Hard gate tidak dapat dipenuhi oleh bukti Reported atau Assumed untuk kelas D2 ke atas.
- Evaluate mencatat apa yang **tidak** diperiksa. Pemeriksaan yang dilewati atau gagal karena lingkungan dicatat sebagai belum terverifikasi.

## 3. Verify: konfirmasi independen

- **Independensi**: verifier berbeda dari pengusul; untuk D2 ke atas, minimal satu verifier adalah manusia yang kompeten atau pemeriksaan deterministik yang tidak dikendalikan pengusul.
- **Reproduksi**: jalankan ulang pemeriksaan kunci atau sampel bukti secara independen, bukan hanya membaca laporan pengusul.
- **Kesegaran**: bukti MUST dinyatakan basi bila artefak berubah setelah evaluasi; approval lama tidak berlaku (sejalan dengan aturan stale approval di [Git dan review](git-and-code-review.md)).
- **Pra-tindakan**: rollback, dry-run, atau recovery plan tersedia sesuai kelas.
- **Pasca-tindakan**: konfirmasi hasil aktual (health check, rekonsiliasi, retest) dan catat bila menyimpang dari klaim. Penyimpangan memicu rollback atau eskalasi sesuai runbook.
- **Verifikasi verifier**: secara berkala sisipkan kasus yang diketahui buruk (known-bad) dan baik untuk memastikan decision layer menolak dan menerima dengan benar.

## Verdict

| Verdict | Arti | Tindakan |
| --- | --- | --- |
| ALLOW | Semua hard gate lulus, bukti Verified | Eksekusi sesuai kelas |
| ALLOW_WITH_CONDITIONS | Lulus dengan syarat yang dapat diperiksa (mis. staged rollout, tenggat tindak lanjut) | Eksekusi; syarat dipantau dan ditutup oleh owner |
| ESCALATE | Bukti ambigu, kelas naik, atau di luar wewenang | Naikkan ke approver kelas lebih tinggi |
| DENY | Hard gate gagal atau risiko tidak dapat diterima | Tidak dieksekusi; alasan dan perbaikan dicatat |
| NOT_VERIFIED | Bukti tidak dapat dikumpulkan atau diverifikasi | Diperlakukan sebagai bukan lulus |

## Titik penerapan

| Keputusan | Kelas tipikal | Hard gate contoh | Verifier |
| --- | --- | --- | --- |
| Merge PR | D1–D3 | Build, tes, scanner lulus; approval non-author | Reviewer independen |
| Rilis produksi | D2–D3 | Pipeline hijau terikat commit, rollback siap, approval sesuai tier | Release approver + owner risiko |
| Triase temuan scanner | D1–D2 | Jalur terjangkau dan dampak dinilai | Security owner atau reviewer kedua |
| Auto-remediation oleh agent | D1–D3 | Perubahan terbatas, tes regresi, tidak menyentuh area sensitif tanpa D3 | Manusia atau pemeriksaan deterministik |
| Persetujuan pengecualian | D3 | Risiko, mitigasi, kedaluwarsa tercatat | Penerima risiko yang berwenang |
| Rekomendasi arsitektur | D2–D3 | Drivers dan constraint terdokumentasi, alternatif dievaluasi | Architect/security reviewer |
| Penutupan temuan | D2 | Retest membuktikan akar masalah tertutup | Pihak selain yang memperbaiki |

## Catatan keputusan

Simpan sebagai bagian PR, ADR, tiket, atau log keputusan di repo proyek. Jangan menaruh secret, data pelanggan, atau detail exploit di catatan yang berada di repo publik.

```markdown
## Catatan keputusan JEV
- ID / tanggal:
- Keputusan yang diminta dan artefak (commit/digest/versi):
- Pengusul (manusia/agent/scanner) dan verifier:
- Judge: tier, reversibilitas, blast radius, privilege, kelas (D0–D4), alasan:
- Evaluate: hard gate (lulus/gagal + bukti), rubrik, bukti berstatus Verified/Reported/Assumed:
- Tidak diperiksa / belum terverifikasi:
- Verify: metode independen, hasil reproduksi, kesegaran bukti:
- Verdict: ALLOW / ALLOW_WITH_CONDITIONS / ESCALATE / DENY / NOT_VERIFIED
- Syarat, owner, tenggat:
- Verifikasi pasca-tindakan dan hasilnya:
```

## Tata kelola decision layer

- Setiap decision layer MUST punya owner yang bertanggung jawab atas kriteria, kelas, dan perubahan; perubahan kriteria ditinjau seperti kode (CODEOWNERS atau setara).
- Tinjau berkala: tingkat override, keputusan yang belakangan terbukti salah (false allow dan false deny), cacat lolos ke produksi, dan waktu keputusan. Gunakan hasilnya untuk mengencangkan atau melonggarkan kriteria melalui perubahan yang tercatat.
- Log keputusan MUST tahan ubah sesuai tier dan dapat dikaitkan ke artefak dan identitas pengusul/verifier.
- Pemasangan teknis (policy-as-code, required checks, approval gate) adalah [guardrails](guardrails.md); JEV menentukan isi keputusan, guardrails menegakkannya.
