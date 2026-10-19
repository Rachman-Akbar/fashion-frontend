# Fashionku Frontend

Frontend React untuk **Fashionku** — marketplace fashion single-store (satu toko, dua role: seller & buyer). Berasal dari salinan proyek `market-frontend` yang ditransformasi (proyek sumber tidak diubah).

## Ringkasan Transformasi

- **Branding**: seluruh UI memakai merek "Fashionku" (navbar, footer, judul halaman, `package.json`).
- **Dihapus**: seluruh panel admin (`/admin/*`, `/admin/login`), PPOB (`/ppob`, receipt, widget top-up di home & riwayat), Misi & Hadiah (`/profile/missions`, mission rewards di voucher), planner jadwal seller, etalase (showcase), pembayaran promosi, bahan baku.
- **Dipertahankan**: katalog buyer (home, cari, kategori, produk, promo, toko), cart/checkout/pesanan, profil (alamat, notifikasi, pembayaran, voucher, bantuan), chat, seller center (dashboard, produk, stock, voucher, promosi, pesanan, pelanggan, review, cashflow, hutang-piutang, info toko, banner, preview, rumus kode).
- **Single store**: onboarding seller (`/auth/seller/onboarding`) mendaftarkan seller ke toko singleton; multi-store UI dihapus.

## Kebutuhan

- Node.js 20+ (dikembangkan dengan Node 26), npm

## Setup

```bash
npm ci
cp .env.example .env    # atau buat .env manual (lihat di bawah)
npm run dev             # dev server di http://127.0.0.1:5174
```

`.env`:

```
VITE_DEV_BROWSER_HOST=127.0.0.1
VITE_DEV_BROWSER_PORT=5174
VITE_DEV_BACKEND_TARGET=http://127.0.0.1:8001
```

Dev server mem-proxy `/api` dan `/storage` ke backend (`fashion-api`, port 8001).

## Perintah

| Perintah | Fungsi |
|---|---|
| `npm run dev` | Dev server (port 5174) |
| `npm run lint` | ESLint — 0 error (warning react-hooks pre-existing) |
| `npm test` | Vitest — 154 tests, 18 files, semua lulus |
| `npm run build` | Production build ke `dist/` |

## Arsitektur Singkat

- React 18 + Vite 7 + Tailwind CSS 4, React Query, axios, react-router v7 (basis JavaScript, bukan TypeScript).
- Struktur fitur per domain: `src/features/{catalog,order,seller,profile,auth,advanced}`; shared layout di `src/shared/layout`.
- `src/features/admin/order/` dipertahankan sebagai service bersama untuk manajemen pesanan seller (bukan panel admin).
- Auth: token disimpan lalu dikirim sebagai Bearer; role aktif (buyer/seller) berlaku per token — seller panel membutuhkan `switch-role` ke seller.
# fashion-frontend
