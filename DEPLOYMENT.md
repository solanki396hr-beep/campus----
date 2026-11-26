# 🚀 CampusHub Deployment Guide (Vercel & Render)

This project contains two parts:
1. **Frontend (Vercel)**: React + Vite Single Page Application at root (`./`).
2. **Backend (Render)**: Node.js + Express REST API inside `backend/` (or `server/`).

---

## 1. Deploy the Backend on Render

1. Go to [Render Dashboard](https://dashboard.render.com/) and click **New +** -> **Web Service**.
2. Connect your GitHub / GitLab repository.
3. Configure settings:
   - **Name**: `campushub-backend`
   - **Root Directory**: `backend` (or `server`)
   - **Environment**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
4. In **Environment Variables**, add the secrets:
   | Key | Value / Example | Note |
   |---|---|---|
   | `PORT` | `5000` | Port for Express |
   | `NODE_ENV` | `production` | Set to production |
   | `JWT_SECRET` | `generate-a-strong-secret-key-here` | Secret key for auth/tokens |
   | `CLIENT_URL` | `https://your-campushub.vercel.app` | Your deployed Vercel frontend domain |

5. Click **Create Web Service**. Once deployed, copy your backend URL:
   `https://<your-render-service>.onrender.com`

---

## 2. Deploy the Frontend on Vercel

1. Go to [Vercel Dashboard](https://vercel.com/dashboard) and click **Add New...** -> **Project**.
2. Import the same repository.
3. Configure settings:
   - **Framework Preset**: `Vite`
   - **Root Directory**: `./` (leave default root)
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
4. In **Environment Variables**, add:
   | Key | Value |
   |---|---|
   | `VITE_API_URL` | `https://<your-render-service>.onrender.com/api` |
5. Click **Deploy**.
6. Vercel uses the included [vercel.json](file:///c:/Users/hp/c.campushub/vercel.json) to handle Single Page App routing so refreshes work seamlessly.

---

## 3. Secret & Environment Files Overview

- `.gitignore` (Root) protects all `.env`, `.env*.local`, `backend/.env`, and `server/.env` files from being committed to Git.
- `.env.example`: Template for frontend environment variables.
- `backend/.env.example`: Template for backend server secrets.
- `render.yaml`: Blueprint configuration for Render pointing to `backend/`.
- `vercel.json`: Handles SPA URL rewrites for React Router.
