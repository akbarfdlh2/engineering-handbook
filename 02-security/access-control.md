# Access Control dan Privileged Access

- Otorisasi MUST ditegakkan server-side pada setiap request dan memeriksa subject, action, resource, tenant, status, dan konteks yang relevan.
- Default access MUST deny. Role/permission didefinisikan berdasarkan pekerjaan; jangan menerima role, tenant, owner, atau scope yang dikirim client sebagai bukti izin.
- Multi-tenant service MUST menguji isolasi tenant pada read, update, delete, export, search, background jobs, cache, dan object storage.
- Gunakan hak minimum dan pisahkan tugas untuk perubahan yang dapat memengaruhi uang, identitas, security policy, production data, atau approval audit. Dokumentasikan kombinasi peran yang tidak boleh dipegang satu orang pada [matriks segregation of duties](segregation-of-duties-matrix-template.md).
- Production privilege SHOULD diberikan just-in-time, dibatasi waktu, memerlukan approval sesuai tier, dan meninggalkan audit record. Akses database langsung hanya untuk kebutuhan tertentu yang disetujui.
- Tinjau keanggotaan privileged sekurangnya triwulanan dan akses lainnya sekurangnya tahunan; cabut segera saat tidak lagi dibutuhkan, perubahan role, kontrak berakhir, atau dugaan compromise.
- Identitas machine-to-machine MUST terpisah dari identitas pengguna; setiap service identity memiliki owner, audience, scope, environment, lifetime, dan revocation path.
- Perubahan permission/role dan akses export/bulk MUST dapat diaudit. Hindari role gabungan yang mengizinkan satu orang membuat sekaligus menyetujui perubahan kritis.
- Tes authorization MUST mencakup user tanpa izin, role salah, resource tenant lain, status tidak valid, dan percobaan privilege escalation.
- Break-glass harus minimum, terpisah, dipantau, serta diuji sesuai [kebijakan identity](identity-and-authentication.md#sso-dan-akun-mesin).
