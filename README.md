# Apnik
<p align="center">
  <img src="https://img.shields.io/badge/build-passing-brightgreen" />
  <img src="https://img.shields.io/badge/version-1.0.0-blue" />
  <img src="https://img.shields.io/badge/license-AGPLv3-yellow" />
</p>

Aplikasi layanan publik berbasis **NestJS**, **PostgreSQL**, **Redis**, **TailwindCSS**, dan **Handlebars**.  
Dirancang untuk dipakai oleh developer, institusi, dan auditor, tetapi **tidak boleh dijual ulang sebagai closed-source**.

## Fitur Utama
- Manajemen antrean & layanan publik
- Dashboard monitoring real-time
- Otentikasi berbasis session
- REST API dan dokumentasi OpenAPI (Swagger)
- Fullstack: TailwindCSS + Handlebars untuk UI
- Logging & monitoring dengan Winston dan Nest-Winston
- DevOps tools: PM2, dotenv-cli, rimraf

## Requirements
- Node.js >= 22
- PostgreSQL
- Redis
- NPM >= 9

## Installation

```bash
git clone https://github.com/tarasare/apnik.git
cd apnik
npm install
```

## Configuration
Buat file .env di root project (contoh: .env.development):

```bash
# Database
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=yourpassword
DB_DATABASE=apnik

# Redis
REDIS_HOST=127.0.0.1
REDIS_PORT=6379
REDIS_PASSWORD=

# Session
SESSION_SECRET=yourSecretKey

# App
PORT=3000
NODE_ENV=development
```

Untuk production, buat .env.production sesuai environment VPS atau server production.


## Build & Run

### Development
```bash
npm run start:dev
```

### Debug
```bash
npm run start:debug
```

### Production
```bash
npm run build
npm run start:prod
```


### Stop/Restart Production
```bash
npm run stop:prod
npm run restart:prod
```


## Tailwind CSS

Tailwind CSS
```bash
npm run tailwind:build
```
Watch mode (opsional):
```bash
npx tailwindcss -i ./src/assets/css/tailwind.css -o ./public/css/app.css --watch
```

## Testing
```bash
npm run test
npm run test:watch
npm run test:cov
```

## Documentation
  - Code Documentation: npm run docs:code
  - UI Documentation: npm run docs:ui
  - All docs: npm run docs:all

Swagger (OpenAPI) dapat diakses di:
```bash
http://localhost:3000/api
```

## Deployment
Deployment
 1. Upload source ke server
 2. Install dependencies: npm install --production
 3. Set environment .env.production
 4. Build aplikasi: npm run build
 5. Jalankan dengan PM2: npm run start:prod
 6. Monitoring: pm2 list, pm2 logs apnik

## Auditing & Logging
 - Logging menggunakan Winston + Nest-Winston
 - Logs disimpan di folder logs/ (pastikan .gitignore menutup logs)
 - Sistem monitoring siap untuk auditor dengan endpoints dan dashboard

## License
This project is licensed under the GNU AGPL v3 – see the LICENSE
 file for details.
 
⚠️ Anda boleh menggunakan, fork, atau modify software ini, tetapi tidak boleh menjual ulang sebagai closed-source.

## Third-Party Libraries
  All third-party libraries are used under their respective licenses.
  See THIRD_PARTY_LICENSES.md for full details.

## Contributing

Jika ingin berkontribusi:
 - Fork repository
 - Buat branch baru: git checkout -b feature/your-feature
 - Commit perubahan: git commit -am 'Add new feature'
 - Push ke branch: git push origin feature/your-feature
 - Buat Pull Request

Pastikan semua perubahan tetap mematuhi AGPL v3.

## Notes for Roles
 - Developer: fokus pada setup, build, testing, Tailwind, docs
 - User: fokus pada install, run, dan UI usage
 - Auditor: fokus pada logging, monitoring, dan license compliance

