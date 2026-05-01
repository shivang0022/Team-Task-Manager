# ProjectFlow

A full-stack project management app with authentication, project/team management, task assignment, status tracking, dashboard metrics, validations, relational data, and role-based access control.

## Tech Stack

- React + Vite frontend
- Express REST API
- MySQL database
- Prisma ORM and migrations
- JWT authentication
- Admin/Member global roles plus project Owner/Member access

## Local Setup

1. Install dependencies:

```bash
npm install
```

2. Create `.env` from `.env.example` and set `DATABASE_URL` and `JWT_SECRET`.

3. Run migrations:

```bash
npm run prisma:migrate
```

4. Start development:

```bash
npm run dev
```

The frontend runs on `http://localhost:5173` and proxies API requests to `http://localhost:3000`.

## Railway Deployment

1. Push this project to GitHub.
2. Create a new Railway project from the GitHub repo.
3. Add a MySQL service in Railway.
4. In the app service variables, set:

```bash
DATABASE_URL=${{MySQL.DATABASE_URL}}
JWT_SECRET=<long-random-secret>
NODE_ENV=production
```

5. Railway will use `railway.json`:

- Build: `npm ci --include=dev && npm run build`
- Start: `npm start`
- Health check: `/api/health`

`npm start` runs `prisma migrate deploy`, generates the Prisma client, and serves the built React app from Express.

## Role Rules

- The first signup becomes `ADMIN` automatically.
- Admins can see all projects and manage any project.
- Members only see projects they belong to.
- Project owners can edit projects and add members.
- Project members can create tasks and update task status inside their projects.
