# Code Review Checklist

Checklist ini membantu reviewer; gunakan penilaian risiko, jangan menyetujui hanya karena semua kotak tercentang.

## Perilaku dan desain

- [ ] Perubahan menyelesaikan kebutuhan dan tidak mengubah perilaku lain tanpa alasan.
- [ ] Aturan bisnis memiliki satu sumber kebenaran; batas modul dan error states jelas.
- [ ] Edge cases, retry, concurrency, timeout, dan kegagalan dependency ditangani.

## Security dan data

- [ ] Authentication dan server-side authorization sesuai actor, action, resource, dan tenant.
- [ ] Input, output encoding, file, query, secrets, logging, dan rate limits ditangani aman.
- [ ] Data sensitif diminimalkan; retensi, audit, migration, backup, dan recovery dipertimbangkan.
- [ ] Dependency baru, permissions, dan supply-chain changes punya alasan dan review.

## Reliability dan kualitas

- [ ] Tes memeriksa success, failure, authorization-negative, dan data boundaries yang relevan.
- [ ] Timeout, idempotency, observability, alerting, capacity, deployment, rollback, dan runbook sesuai risiko.
- [ ] API, schema, configuration, compatibility, and documentation updates sinkron.

## UI dan aksesibilitas

- [ ] Keyboard/focus, labels, status, errors, contrast, responsive behavior, dan reduced motion ditangani sesuai perubahan.
- [ ] Implementasi memakai design-system tokens/components yang disetujui atau menjelaskan alasannya.

## Keputusan review

- Temuan blocking dan prioritas:
- Pengecualian/risiko residual:
- Pemeriksaan yang belum diverifikasi:
