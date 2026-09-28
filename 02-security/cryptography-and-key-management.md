# Cryptography dan Key Management

- Gunakan protokol, algoritma, dan library kriptografi yang terpelihara serta disetujui security owner. Dilarang membuat algoritma, protokol, atau format enkripsi sendiri.
- Data Confidential/Restricted MUST dienkripsi saat transit melalui jaringan yang tidak sepenuhnya dipercaya dan saat tersimpan; pilih kontrol sesuai threat model dan kebutuhan pencarian/operasional.
- Kunci encryption/signing MUST dikelola melalui KMS/HSM atau secret manager yang disetujui, terpisah dari data yang dilindungi, dengan hak minimum dan audit akses.
- Setiap kunci memiliki owner, tujuan, scope, lingkungan, masa pakai, rotasi/revocation path, dan prosedur recovery. Pisahkan key antara dev/test/staging/production.
- Kunci yang bocor atau diduga bocor MUST segera dicabut/dirotasi, dampak ditelusuri, dan penggunaan lama dibatasi. Rotasi rutin ditetapkan menurut umur, algoritma, exposure, dan aturan pihak terkait.
- Akses master/root key dibatasi sangat ketat dan memerlukan approval/audit; jangan menyimpan key material di source code, image, log, issue, dokumen publik, atau backup yang tidak dilindungi.
- Backup dan pemulihan key harus memungkinkan data dipulihkan tanpa menghilangkan kontrol pemisahan akses.
- Sertifikat, signing key, dan credential berumur pendek dipantau sebelum kedaluwarsa; proses renewal diuji dan memiliki owner.
- Token/API key harus dibatasi scope, audience, lifetime, dan environment; dukung revocation dan jangan menaruhnya di URL.

Rujukan implementasi: [OWASP Cryptographic Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html) dan, untuk password, [Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html).
