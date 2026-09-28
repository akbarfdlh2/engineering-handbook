# Identity, Login, dan MFA

## Kebijakan login

- Semua akun manusia yang dapat login MUST menggunakan MFA. MFA harus diselesaikan saat membuat sesi baru; sesi tepercaya hanya boleh mengurangi prompt selama batas waktu dan kondisi risiko yang disetujui proyek.
- Semua akun administrator, developer, operator produksi, dan akun yang mengakses data sensitif MUST memakai MFA phishing-resistant (WebAuthn/FIDO2 dengan user verification atau metode yang dinilai setara oleh security owner). TOTP hanya boleh menjadi fallback sementara dengan persetujuan tertulis security owner, mitigasi, owner, dan masa berlaku maksimal 90 hari. SMS/email tidak memenuhi syarat pengecualian untuk akun privileged.
- Akun privileged MUST terpisah dari akun kerja biasa bila memungkinkan, memakai hak minimum, dan tidak digunakan untuk email/web umum.
- Provisioning akun MUST didasarkan pada identitas dan kebutuhan kerja yang terverifikasi; undangan atau enrollment token harus sekali pakai dan kedaluwarsa. Dilarang membuat akun production dengan default password atau self-asserted privilege.
- MFA bukan opsi opt-in tersembunyi. Enrollment wajib, bantuan setup jelas, dan pengguna tidak boleh terus memakai akun terlindungi tanpa MFA.
- Produk yang belum dapat mewajibkan MFA MUST NOT membuka login manusia baru ke production. Rollout bertahap hanya boleh memakai pengecualian berjangka maksimal 90 hari, dengan cakupan, mitigasi, owner, tanggal penghentian, dan persetujuan security owner. Akses admin dan fitur sensitif tetap diblokir sampai MFA terdaftar.
- Akun bersama MUST NOT dipakai untuk manusia. Setiap orang harus memiliki identitas unik agar tindakan dapat diaudit dan akses dapat dicabut secara tepat.

## Metode autentikasi

Urutan pilihan:

1. **Phishing-resistant**: WebAuthn/FIDO2 security key atau passkey yang tervalidasi pada alur produk.
2. **TOTP authenticator** sebagai fallback yang dapat diterima; batasi percobaan, cegah replay, dan proteksi seed dengan enkripsi serta kontrol akses.
3. **Push approval** hanya dengan number matching/context, anti-fatigue controls, dan pemantauan; jangan gunakan push tanpa konteks sebagai metode utama atau untuk memenuhi phishing-resistant MFA.
4. **SMS/voice/email OTP** MUST NOT menjadi satu-satunya faktor untuk akun internal, privileged, atau akses sensitif. Jika terpaksa sebagai fallback sementara, batasi cakupan/waktu, berikan alternatif, dan catat risiko.

Metode passwordless hanya boleh disebut MFA jika mekanismenya benar-benar memenuhi faktor autentikasi yang dibutuhkan. Jangan menganggap biometrik server-side sebagai pengganti kepemilikan authenticator; verifikasi biometrik sebaiknya lokal pada perangkat.

## Password dan credential

- Password yang dipakai bersama MFA MUST minimal 8 karakter; password sebagai satu-satunya faktor MUST minimal 15 karakter. Izinkan passphrase panjang (setidaknya 64 karakter), spasi, paste, password manager, dan autofill. Nilai ini adalah minimum, bukan target agar password menggantikan MFA.
- Tolak password yang umum, kontekstual, atau diketahui bocor melalui blocklist; jangan memaksa aturan komposisi karakter atau rotasi periodik tanpa bukti kompromi.
- Simpan password hanya dalam bentuk salted, adaptive hash dengan parameter yang ditinjau dan dapat dinaikkan; utamakan Argon2id (OWASP saat review ini: minimal 19 MiB memory, 2 iterations, parallelism 1, lalu benchmark/tune ke atas). Gunakan scrypt jika Argon2id tidak tersedia; pertahankan bcrypt legacy hanya dengan parameter memadai dan rencana migrasi. Gunakan PBKDF2 bila diwajibkan lingkungan FIPS/kebijakan. Pakai implementasi teruji/framework, bukan algoritma buatan sendiri.
- Password, OTP, recovery code, dan seed MUST NOT muncul di log, analytics, URL, atau pesan error.
- Password reset MUST memakai token acak berentropi tinggi, sekali pakai, dengan masa berlaku pendek dan pembatalan token/sesi yang sesuai; response tidak boleh mengungkap keberadaan akun.
- Sediakan pesan login yang tidak membocorkan apakah akun ada, terkunci, atau memakai metode tertentu.

## Enrollment dan pemulihan akun

- Enrollment atau penghapusan MFA MUST meminta autentikasi ulang dengan faktor yang sudah terdaftar; bila tidak tersedia, jalankan proses recovery berjaminan setara. Perubahan email/nomor kontak yang memengaruhi recovery juga memerlukan autentikasi ulang.
- Akun privileged dan akun yang mengakses data Restricted MUST memiliki sedikitnya dua authenticator independen yang terdaftar; jangan menyimpan keduanya hanya pada perangkat atau faktor pemulihan yang sama.
- Recovery codes MUST acak, sekali pakai, disimpan ter-hash, hanya ditampilkan saat penerbitan, dan penerbitan ulang membatalkan kode lama.
- Helpdesk MUST tidak boleh menonaktifkan MFA hanya berdasarkan data yang mudah dicari atau caller ID. Recovery manual memerlukan verifikasi identitas, approval independen untuk akun privileged, audit trail, notifikasi ke kanal terdaftar, dan pencabutan sesi lama.
- Perubahan authenticator, recovery, password reset, dan perubahan faktor MUST memberi notifikasi kepada pengguna. Sediakan cara melaporkan perubahan yang tidak dikenal.

## Sesi dan proteksi login

- Gunakan TLS untuk seluruh sesi; cookie sesi browser MUST `Secure`, `HttpOnly`, dan `SameSite` sesuai alur. Token MUST disimpan di lokasi yang mengurangi dampak XSS; jangan menyimpan bearer token jangka panjang di local storage.
- Browser application SHOULD memakai server-managed session/BFF bila sesuai arsitektur. Native app MUST memakai system browser dan Authorization Code + PKCE; token disimpan di secure storage OS, tidak di plain preferences atau log.
- Rotasi session identifier setelah login, MFA, perubahan privilege, dan re-authentication. Logout dan pencabutan akses harus membatalkan sesi/token terkait.
- Refresh token MUST dirotasi atau dibatasi dengan mekanisme reuse detection; revokasi password/factor/session harus mencabut token terkait. Setiap proyek MUST menetapkan idle timeout, absolute lifetime, refresh-token lifetime/revocation, dan kondisi trusted-device menurut tier dan dampak data. Sampai nilainya disetujui, jangan aktifkan trusted-device bypass atau sesi tanpa batas. Minta step-up authentication untuk ekspor massal, perubahan MFA, pembayaran, perubahan privilege, atau aksi berisiko tinggi.
- Rate-limit percobaan per akun dan sumber dengan kontrol anti-automation; cegah credential stuffing, brute force, MFA fatigue, enumeration, dan denial-of-service akibat lockout berlebihan.
- Waspadai perubahan perangkat, lokasi, IP, pola login, dan perilaku anomali tanpa menjadikan satu sinyal lemah sebagai bukti identitas.
- Semua autentikasi dan perubahan faktor penting MUST menghasilkan audit event tanpa menyimpan credential atau data sensitif yang tidak diperlukan.

## SSO dan akun mesin

- Aplikasi internal yang mendukung federasi MUST menggunakan identity provider terpusat dengan SSO dan MFA. Local account exception harus memiliki owner, scope, alasan, kontrol setara, dan review berkala.
- Keanggotaan dan hak akses MUST ditinjau setidaknya triwulanan untuk akun privileged dan setidaknya tahunan untuk akun lainnya; cabut akses segera saat tidak lagi dibutuhkan dan paling lambat pada saat hubungan kerja/kontrak berakhir.
- Aplikasi yang memakai OIDC/OAuth MUST memvalidasi issuer, audience, signature, expiry, state/nonce, redirect URI, dan PKCE sesuai jenis client; public client MUST memakai Authorization Code flow dengan PKCE. Jangan gunakan implicit flow atau Resource Owner Password Credentials grant untuk login pengguna.
- Akun machine/service MUST punya identitas unik, owner, scope minimum, masa berlaku/rotasi, dan penyimpanan di secret manager. Utamakan workload identity/short-lived credentials daripada secret jangka panjang. Dilarang memakai akun manusia bersama atau default credentials.
- Akun break-glass dibatasi, jumlahnya minimum, dilindungi dengan authenticator independen dari IdP utama, dan disimpan di vault dengan akses dua orang bila memungkinkan. Setiap penggunaan memicu alert dan review; uji akses secara berkala, lalu ganti credential setelah dipakai.

## Rujukan

- [NIST SP 800-63B-4](https://pages.nist.gov/800-63-4/sp800-63b.html) untuk authenticator, password, dan assurance level.
- [OWASP ASVS 5.0.0](https://owasp.org/projects/asvs) untuk requirement verifikasi autentikasi, sesi, otorisasi, dan proteksi data aplikasi.
- [OWASP Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html) untuk konfigurasi password hashing.
- [IETF RFC 9700](https://www.rfc-editor.org/rfc/rfc9700.html) untuk keamanan OAuth 2.0.
- [CISA: Require Multifactor Authentication](https://www.cisa.gov/audiences/small-and-medium-businesses/secure-your-business/require-multifactor-authentication) untuk penerapan MFA dan prioritas phishing-resistant.
