# API dan Compatibility

- Setiap operasi API non-publik MUST mengautentikasi dan mengotorisasi actor sesuai tenant, resource, dan tindakan. Endpoint publik harus dinyatakan sebagai public, membatasi data yang dikembalikan, dan memiliki proteksi abuse yang sesuai.
- Validasi input dan batas ukuran/kecepatan MUST diterapkan di server. Error tidak menampilkan stack trace, secret, atau detail internal.
- Perubahan breaking MUST memiliki versi atau rencana migrasi, tanggal penghentian, pemilik konsumen, dan mekanisme rollback.
- API yang terekspos SHOULD memiliki spesifikasi kontrak dan contoh request/response yang selalu diperbarui bersama implementasi.
- Idempotency MUST dipertimbangkan untuk operasi retryable yang membuat transaksi atau side effect.
- Data sensitif MUST diminimalkan dari response, event, log, dan analytics.
