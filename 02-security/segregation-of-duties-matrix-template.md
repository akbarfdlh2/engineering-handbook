# Segregation of Duties Matrix Template

Gunakan matriks ini untuk mengidentifikasi kombinasi peran/tindakan yang tidak boleh dipegang satu orang yang sama, melengkapi prinsip di [access control](access-control.md).

## Matriks konflik

| Fungsi A | Fungsi B | Konflik bila dipegang orang sama | Kontrol pemisahan/kompensasi |
| --- | --- | --- | --- |
| Menulis/merge kode | Approve deployment production | Ya — pembuat perubahan menyetujui perubahannya sendiri | Review independen wajib; author tidak boleh self-approve |
| Inisiasi pembayaran/transaksi | Approve/otorisasi pembayaran | Ya — risiko fraud | Dual control; limit approval per role |
| Memberi akses (grant) | Meninjau/mengaudit akses | Ya — tidak ada pengecekan independen | Access review oleh pihak berbeda dari yang memberi akses |
| Mengelola infrastruktur production | Mengelola/menghapus audit log | Ya — dapat menyembunyikan jejak | Log terpusat, akses terbatas, immutable/write-once bila memungkinkan |
| Mengembangkan model/keputusan otomatis | Memvalidasi model tersebut | Ya — bias validasi | Validator independen sesuai [model risk management](../00-governance/model-risk-management-template.md) |
| [tambahkan sesuai konteks proyek] | | | |

## Saat pemisahan penuh tidak memungkinkan (tim kecil)

- Dokumentasikan kompensasi: review pihak ketiga berkala, dual-approval manual, atau monitoring tambahan.
- Catat sebagai [pengecualian kontrol](../00-governance/exception-template.md) bila menyimpang dari baseline SoD organisasi, dengan owner dan tanggal review.

## Review

- Tinjau matriks saat struktur tim, role, atau sistem akses berubah, dan sekurangnya tahunan.
- Hasil review dan temuan konflik yang belum diselesaikan dicatat pada [risk register](../00-governance/risk-register-template.md).

Rujukan: prinsip segregation of duties pada [ISO/IEC 27001:2022](https://www.iso.org/standard/27001) Annex A dan [AICPA Trust Services Criteria CC5 — Control Activities](https://www.aicpa-cima.com/resources/download/get-description-criteria-for-your-organizations-soc-2-r-report).
