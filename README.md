# ARGsoft Solutions — Complete Static Prototype

A polished, responsive corporate website + careers experience + HR recruiting portal prototype built with plain HTML, CSS and vanilla JavaScript.

## Run locally

Because this is a static site, you can use any static server:

```bash
python -m http.server 8080
```

Then open `http://localhost:8080`.

You can also deploy the folder directly to a static hosting provider.

## Routes

- `#/` — Home
- `#/about` — About
- `#/services` — Services
- `#/industries` — Industries
- `#/careers` — Careers/job search
- `#/job/ARG-2401` — Job detail example
- `#/contact` — Contact
- `#/hr-login` — HR login
- `#/hr` — HR dashboard after prototype sign-in
- `#/hr/jobs` — Job management
- `#/hr/post` — Create a job
- `#/hr/applicants` — Applicant pipeline
- `#/hr/settings` — Production-readiness notes

## ARGsoft branding

Official supplied logo: `assets/argsoft-logo.jpeg`

Office: Flat No. 404, Sashi Arkade, JNTU Road, KPHB Phase - 9, Hyderabad - 500072, Telangana, India

HR: `hr@argsoft.net`

## Prototype behavior

Jobs and applicants are persisted to browser `localStorage`, so posting/editing/deleting jobs and changing applicant statuses survive page refreshes in the same browser.

Application submissions add a new applicant to the prototype pipeline.

The HR login deliberately does **not** contain a hardcoded username/password. The "Enter prototype HR portal" flow creates a browser session only to demonstrate the UI. This is not secure authentication.

## Production architecture

Recommended:

Browser → CDN/static frontend → API gateway → application API → PostgreSQL/MySQL

Supporting services:

- OIDC/SAML identity provider for HR
- Private object storage for resumes
- Queue/worker for email notifications
- Centralized audit logs
- Secrets manager
- WAF/rate limiting
- Monitoring and error tracking

### Suggested API

`POST /api/auth/login`
`POST /api/auth/logout`
`GET /api/jobs`
`POST /api/jobs`
`PATCH /api/jobs/:id`
`DELETE /api/jobs/:id`
`GET /api/applicants`
`GET /api/applicants/:id`
`PATCH /api/applicants/:id`
`POST /api/applications`
`POST /api/resumes/upload-url`

### Resume security

Do not expose a public resume directory. Generate short-lived signed upload/download URLs on the server. Validate MIME type and file size, scan uploaded files, encrypt storage, restrict bucket access, and record access events.

### Email

A production API can publish events such as `application.created`, `application.status_changed`, and `job.published` to a worker. The worker can send candidate confirmations and recruiter notifications through the organization's transactional email provider.

## Deployment

### Simple static deployment

Upload `index.html`, `styles.css`, and `app.js` to any static hosting/CDN. Configure SPA fallback to `index.html` if converting the hash router to clean URLs.

### Production

Recommended frontend deployment:

- CDN/static hosting
- HTTPS
- custom domain
- security headers
- compressed assets
- cache control
- analytics with consent controls
- real API environment variables

## Design note

The reference website was used only for high-level inspiration around the technology-consulting context. The ARGsoft visual system, copy, navigation, components and interactions are original.
