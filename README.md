# Orbit Frontend

Responsive React + Vite frontend for Orbit.

## Development

1. Start the Django backend from the `social-network` repository on `http://127.0.0.1:8000`.
2. In this repository, run:
   ```bash
   npm install
   npm run dev
   ```
3. Open the Vite URL (normally `http://localhost:5173`).

The Vite development server proxies `/api` and `/login/` to Django. This keeps local session cookies on the same origin and avoids needing permissive CORS settings during local development.

## Authentication

The frontend checks the signed-in Django session with `GET /api/auth/me/` and sends requests with `credentials: 'include'`. A signed-out visitor is sent to the Django login page.

For a deployed frontend, set these Vercel environment variables:

- `VITE_API_BASE_URL`: the public origin of the Django backend, without a trailing slash (for example, `https://api.example.com`).
- `VITE_AUTH_LOGIN_URL`: the full Django login-page URL (for example, `https://api.example.com/login/`).

The Django backend must allow the deployed frontend origin in CORS, enable credentialed requests, and trust the frontend origin for CSRF. Cross-site session cookies must use `SameSite=None; Secure`. Do not disable CSRF protection.

## Build

- `npm run build`
- `npm run preview`

Posting, messaging, media uploads, profile editing, and other data actions still need their corresponding authenticated backend API integration. The current UI keeps several of those interactions local/demo-only.
