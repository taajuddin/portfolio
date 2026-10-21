# MD Taaj Uddin — Full Stack + GenAI Portfolio

A responsive dark-themed portfolio built with **React + Vite**, **Node.js + Express**, and **MongoDB/Mongoose**. Features: animated hero, projects, skills, career timeline, filtering, contact form, rate limiting, and single-service deployment.

## Quick start (Node.js 20+; Node 22 recommended)

```bash
npm install
cp server/.env.example server/.env
# Edit server/.env and set MONGODB_URI
npm run dev
```

Open http://localhost:5173. Vite proxies `/api` to Express on port 5000.

## Production

```bash
npm run build
npm start
```

Open http://localhost:5000. Express serves the built React site and `/api` from the same origin. A MongoDB Atlas connection is needed for the contact form to save messages. The rest of the site works without MongoDB. Contact submissions are **saved to MongoDB, not emailed**; inspect messages through Atlas or implement notifications.

## Deploy to Render (single web service)

1. Push this directory to a new GitHub repository.
2. Create a **Render Blueprint** using `render.yaml`, or a Node Web Service with build `npm install && npm run build` and start `npm start`.
3. Add `MONGODB_URI` as a secret environment variable (MongoDB Atlas connection string). Configure Atlas network access appropriately.
4. Set `CLIENT_ORIGIN` to the final Render site URL (e.g. `https://your-service.onrender.com`). For the same-origin production deployment the browser does not need cross-origin API access, but this setting is useful for other clients.
5. Deploy. Test `/api/health` and the contact form.

**Alternative:** Deploy frontend to Vercel/Netlify and backend to Render; set `VITE_API_URL` on the frontend to your backend HTTPS URL and `CLIENT_ORIGIN` on the backend to your frontend origin. Rebuild frontend after changing `VITE_API_URL`.

## Customize before going live

- Edit `client/src/data.js`: project descriptions, skills, work history. Prototype projects are explicitly labeled; adjust status to reflect actual completed work.
- Edit `client/src/main.jsx`: LinkedIn and GitHub placeholder links; contact copy and any other personal details.
- Add your own resume PDF to `client/public/resume.pdf` if you want a downloadable resume, then add a button linking to `/resume.pdf`.
- Add real project links only if public and authorized. Do not publish private client details, code or internal screenshots.
- Replace `5+` with your preferred current experience figure.
- Add email delivery (e.g., an email provider) if you want notifications; currently messages are only stored in MongoDB.

## Structure

- `client/src/main.jsx`: page sections, animations and contact form
- `client/src/data.js`: editable project/skill/career content
- `client/src/style.css`: responsive visual design
- `server/src/index.js`: Express API, MongoDB storage and static hosting
- `render.yaml`: one-click Render Blueprint config

## Security notes

Input validation, JSON size limits, security headers and contact endpoint rate limiting are included. Before significant public traffic, consider CAPTCHA/spam detection, managed rate-limit storage, stricter CSP, MongoDB IP allowlisting and email notifications. Do not expose MongoDB credentials in the frontend.
