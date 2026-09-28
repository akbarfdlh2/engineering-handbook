# Reliability, Backup, dan Recovery

- Setiap layanan menetapkan owner, critical user journeys, SLI, SLO, alert thresholds, support hours, dan escalation route sesuai tier.
- SLI MUST mengukur pengalaman pengguna atau hasil layanan yang relevan; SLO harus memiliki window, target, sumber data, dan owner. Tier 1/2 SHOULD meninjau error budget dan tren reliability sekurangnya triwulanan.
- Bila Tier 1/2 menghabiskan error budget, owner MUST membuat rencana pemulihan reliability dan membatasi perubahan berisiko sampai stabil; pengecualian harus disetujui business dan engineering owner.
- RTO dan RPO MUST disepakati pemilik bisnis dan engineering berdasarkan dampak, dicatat, serta diuji; jangan memilih angka tanpa kebutuhan bisnis. Untuk gangguan yang memengaruhi fungsi bisnis, bukan hanya satu layanan, gunakan [business continuity plan](business-continuity-plan-template.md).
- Backup production MUST terenkripsi, akses-terbatas, terpisah dari failure domain utama, dan dilindungi dari perubahan/penghapusan tak sengaja atau malicious.
- Prosedur restore production MUST diuji sekurangnya tahunan untuk Tier 2/3 dan sekurangnya triwulanan untuk Tier 1. Backup yang belum pernah direstore bukan bukti pemulihan yang berhasil.
- Backup Tier 1 MUST memiliki salinan terisolasi/immutable yang tidak dapat dihapus oleh credential production harian; uji pemulihan mencakup validasi integritas dan waktu aktual terhadap RTO/RPO.
- Recovery plan mencakup database, file/object storage, konfigurasi, identity dependencies, DNS/network, secrets, dan integrasi penting.
- Pantau kapasitas, error rate, latency, dependency health, backup jobs, replication lag, dan umur sertifikat/credential yang relevan.
- Post-incident review MUST mencatat dampak, timeline, penyebab sistemik, faktor kontributor, mitigasi segera, tindakan pencegahan, owner, dan tenggat.
- Tetapkan batas waktu data loss/service outage yang dapat diterima untuk tiap tier; validasi melalui latihan recovery.
