# INIT.md

**NestJS Monolith Fullstack (Handlebars + Tailwind + PostgreSQL + Redis)**

Dokumen ini berisi **langkah inisialisasi project dari nol** sampai siap dijalankan di **development** dan **production (VPS)**.

---

## 1. Prasyarat

Pastikan sudah terinstall:

* Node.js **>= 20 (disarankan LTS)**
* npm **>= 9**
* PostgreSQL
* Redis
* Git

Cek versi:

```bash
node -v
npm -v
```

---

## 2. Create Project NestJS

```bash
npm i -g @nestjs/cli
nest new apnik
cd apnik
```

Pilih:

* Package manager: **npm**
* Testing: optional

---

## 3. Install Core Backend Dependencies

```bash
npm i \
@nestjs/config \
@nestjs/typeorm \
typeorm \
pg \
@nestjs/session \
express-session \
connect-redis \
redis
```

### Fungsi:

* `@nestjs/config` → load `.env`
* `typeorm` → ORM PostgreSQL
* `express-session` → session-based auth
* `redis` → session store & cache

---

## 4. Install View Engine (Handlebars)

```bash
npm i hbs handlebars
```

Digunakan untuk:

* SSR UI
* Role-based view (admin, user, auditor)
* Layout & partials

---

## 5. Install Tailwind CSS (v4)

```bash
npm install -D tailwindcss @tailwindcss/cli postcss autoprefixer
```

Init config:

```bash
npm exec @tailwindcss/cli init -p
```

---

## 6. Struktur Asset Tailwind

```txt
src/
└── assets/
    └── css/
        └── tailwind.css
```

Isi `tailwind.css`:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

---

## 7. Konfigurasi Tailwind

`tailwind.config.js`

```js
module.exports = {
  content: [
    './views/**/*.hbs',
    './src/**/*.ts'
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

---

## 8. Setup Static Assets di NestJS

`main.ts`

```ts
app.useStaticAssets(join(__dirname, '..', 'public'));
app.setBaseViewsDir(join(__dirname, '..', 'views'));
app.setViewEngine('hbs');
```

---

## 9. Install DevOps & Utility Tools

```bash
npm i -D cross-env dotenv-cli rimraf pm2
```

### Kegunaan:

* `cross-env` → ENV cross-platform
* `dotenv-cli` → load env via CLI
* `rimraf` → clean folder (Windows-safe)
* `pm2` → process manager production

---

## 10. Scripts `package.json`

```json
{
  "scripts": {
    "clean": "rimraf dist",
    "build": "npm run clean && nest build",
    "build:css": "tailwindcss -i ./src/assets/css/tailwind.css -o ./public/css/app.css --minify",
    "start:dev": "cross-env NODE_ENV=development nest start --watch",
    "start:prod": "dotenv -e .env.production -- pm2 start dist/main.js --name apnik",
    "stop:prod": "pm2 stop apnik",
    "restart:prod": "pm2 restart apnik"
  }
}
```

---

## 11. Environment Variable

Contoh `.env`:

```env
APP_NAME=apnik
NODE_ENV=development

DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASS=secret
DB_NAME=apnik

REDIS_HOST=127.0.0.1
REDIS_PORT=6379

SESSION_SECRET=supersecret
```

---

## 12. Build & Run

### Development

```bash
npm run build:css
npm run start:dev
```

### Production (VPS)

```bash
npm run build
npm run build:css
npm run start:prod
```

---

## 13. Catatan Auditor & DevOps

* `.env` **tidak pernah masuk repo**
* Semua dependency tercatat di `package-lock.json`
* PM2 menyimpan log & restart otomatis
* Struktur monolith memudahkan audit

---
