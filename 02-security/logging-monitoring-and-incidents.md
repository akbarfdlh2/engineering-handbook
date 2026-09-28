# Logging, Monitoring, dan Incident Response

## Audit dan observabilitas

- Catat login berhasil/gagal, MFA/recovery changes, perubahan akses/role, aksi privileged, akses/ekspor data sensitif, perubahan konfigurasi, dan hasil deployment.
- Audit event MUST memuat actor, waktu tersinkronisasi, aksi, target, hasil, sumber/correlation ID yang sesuai; lindungi dari modifikasi dan akses tidak sah.
- Log MUST NOT memuat password, token, session ID penuh, OTP, secret, data pembayaran, atau data pribadi yang tidak diperlukan.
- Alerting MUST memiliki owner, tingkat keparahan, jalur eskalasi, dan prosedur respons; alert tanpa penanggung jawab bukan kontrol operasional.
- Pantau anomali login, MFA fatigue, aktivitas service account, perubahan privilege, ekspor besar, kegagalan backup, dan pipeline/deploy yang tidak biasa.

## Respons insiden

Siapa pun yang melihat dugaan insiden MUST segera melapor melalui jalur organisasi; jangan menunggu bukti lengkap atau mencoba investigasi yang merusak bukti. Setiap layanan production MUST menunjuk incident commander, security escalation path, contact cadangan, dan jalur 24/7 untuk Tier 1. Target acknowledgment dan eskalasi ditetapkan dalam profil organisasi. Runbook mencakup:

1. triage dampak dan klasifikasi severity;
2. containment dengan mempertahankan bukti;
3. rotasi/revokasi credential dan isolasi sistem sesuai kebutuhan;
4. pemulihan layanan dan verifikasi integritas;
5. komunikasi ke stakeholder dan pihak terdampak sesuai kewajiban;
6. post-incident review tanpa menyalahkan individu, dengan action owner dan tenggat.

Insiden yang menyentuh data atau credential MUST dievaluasi segera untuk dampak privasi, kewajiban kontrak/hukum, notifikasi pihak terdampak, dan kebutuhan melibatkan legal/privacy. Ikuti tenggat hukum yang berlaku; jangan memakai target internal untuk menunda kewajiban tersebut. Jangan menghapus log atau melakukan perubahan destruktif sebelum bukti yang diperlukan diamankan.

Setiap Tier 1 MUST melakukan tabletop incident exercise sekurangnya tahunan dan menindaklanjuti temuan dengan owner serta tenggat.
