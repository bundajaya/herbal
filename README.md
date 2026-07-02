# XREZZKY OFFICIAL STORE

## Struktur Repo (1 repo, deploy ke Vercel)

```
xrezzky-store/
├── public/                  ← Static frontend (auto-serve Vercel)
│   ├── index.html           ← Halaman utama toko
│   ├── admin.html           ← Admin panel (hanya muncul untuk role:admin)
│   ├── css/
│   │   ├── main.css         ← CSS toko utama
│   │   └── admin.css        ← CSS admin panel
│   ├── js/
│   │   ├── app.js           ← JS utama (Firebase, order, rating, dll)
│   │   └── admin.js         ← JS admin panel
│   └── assets/              ← Gambar, icon, dll
│
├── api/                     ← Vercel Serverless Functions
│   ├── orders/
│   │   ├── index.js         ← GET/POST /api/orders
│   │   └── generate-id.js   ← GET /api/orders/generate-id (HBJ-DDMMYY-001)
│   ├── users/
│   │   └── role.js          ← GET/POST /api/users/role
│   └── ratings.js           ← GET /api/ratings (avg semua testimoni)
│
├── lib/
│   ├── firebase.js          ← Firebase Admin SDK singleton
│   └── auth.js              ← verifyToken / requireAdmin middleware
│
├── vercel.json              ← Config routing + CORS
├── package.json
└── .env.example             ← Template env vars
```

## Deploy

```bash
# 1. Install deps
npm install

# 2. Isi env vars
cp .env.example .env.local   # untuk dev lokal

# 3. Deploy
vercel --prod
```

## Env vars (set di Vercel Dashboard → Settings → Environment Variables)

Lihat `.env.example` untuk daftar lengkap.

## Fitur

- **ID Pesanan**: Format `HBJ-DDMMYY-001`, unik per hari, auto-increment
- **Rating Otomatis**: Rata-rata dari semua testimoni, update real-time di hero
- **Admin Link**: Tersembunyi untuk non-admin, muncul otomatis jika `role === 'admin'`
- **API Vercel**: Serverless backend terpisah, auth via Firebase ID Token
