# Environments dan Release Management

- Pisahkan development, test, staging, dan production sesuai kebutuhan risiko. Data dan kredensial production MUST NOT disalin ke non-production secara terbuka.
- Konfigurasi dan infrastruktur SHOULD dikelola sebagai code, ditinjau, dan dipisahkan dari secret values.
- Akses production dibatasi berdasarkan role dan kebutuhan; untuk operasi sensitif gunakan approval, just-in-time access, dan audit.
- Deployment production MUST dapat ditelusuri ke commit/build yang ditinjau dan quality gates yang lulus.
- Perubahan berisiko SHOULD memakai staged rollout/canary atau feature flag dengan kill switch dan rencana rollback.
- Database migration direncanakan agar aplikasi versi lama/baru dapat hidup selama rollout bila diperlukan. Backup harus tersedia sebelum operasi destruktif.
- Operasi production yang menghapus, mengubah massal, atau sulit dibalik MUST memiliki dry-run/reconciliation plan, approval independen, backup/restore plan yang terbukti, batas scope, dan audit trail.
- Tier 1 release MUST mendapat approval eksplisit dari engineering owner dan business/product risk owner; perubahan auth, privilege, key, atau data memerlukan security approval. Perubahan infrastruktur/security produksi yang memerlukan gate formal di luar review kode mengikuti [regulated change management](regulated-change-management.md).
- Rilis mencatat owner, versi, waktu, perubahan utama, hasil pipeline, migrasi, dan cara rollback.
- Hotfix mengikuti pemeriksaan minimum yang aman dan mendapat post-release review.
- Feature flag yang tidak lagi digunakan SHOULD dihapus; flag security-critical harus memiliki owner dan default yang aman.
