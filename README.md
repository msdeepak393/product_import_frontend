# 📦 Product Import Frontend (Vue 3 + Vite)

This is the frontend Single Page Application (SPA) built with **Vue 3**, **Vue Router**, and **Bootstrap 5** to connect with the [Laravel Product Import Backend](https://github.com/msdeepak393/product_import_backend).  

The app allows users to **register, login, upload a CSV file**, and **view imported products** using token-based authentication with Laravel Sanctum.

---

## 🔗 Backend API

Make sure to set up and run the backend first:  
🔗 **Laravel Backend Repo**: [https://github.com/msdeepak393/product_import_backend](https://github.com/msdeepak393/product_import_backend)

---

## 📄 Sample CSV Format

https://github.com/msdeepak393/product_import_frontend/blob/main/Sample%20products/Products.csv

### Clone the Repository

```bash
git clone https://github.com/msdeepak393/product_import_frontend
cd product_import_frontend
```

---

##  Project Setup

```bash
npm install
```

### Start Dev Server

```bash
npm run dev
```

###  Build for Production

```bash
npm run build
```
###  Build with
Node version: v20.14.0
NPM: 10.7.0

## Note

- The frontend is configured to use the API base URL: `http://localhost:8000/api`
- Tokens are stored in `localStorage`
- CORS must be properly set up on the Laravel backend for requests to succeed

---