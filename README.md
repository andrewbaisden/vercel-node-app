# vercel-node-app

A small Express demo that serves four text routes. It runs locally with Node and deploys to Vercel as a single serverless function using [zero-config Express detection](https://vercel.com/docs/frameworks/backend/express).

## Prerequisites

- [Node.js](https://nodejs.org/) 20 or later
- npm (bundled with Node)
- A [Vercel](https://vercel.com/) account (only required for deploy)

## Local setup

```bash
git clone https://github.com/andrewbaisden/vercel-node-app.git
cd vercel-node-app
npm install
npm start
```

The server listens on `http://localhost:3000` (or `PORT` if that environment variable is set).

To match production more closely, install the [Vercel CLI](https://vercel.com/docs/cli) and run:

```bash
npx vercel dev
```

## Routes

All routes are `GET` and return plain text.

| Path | Response |
| --- | --- |
| `/` | `Home Page Route` |
| `/about` | `About Page Route` |
| `/portfolio` | `Portfolio Page Route` |
| `/contact` | `Contact Page Route` |

Examples:

```bash
curl http://localhost:3000/
curl http://localhost:3000/about
curl http://localhost:3000/portfolio
curl http://localhost:3000/contact
```

## Deploy to Vercel

No `vercel.json` is required. Vercel finds `index.js`, uses the exported Express app, and sends every request to that one function.

### Git (recommended)

1. Push this repo to GitHub (or another Git provider Vercel supports).
2. Open [vercel.com/new](https://vercel.com/new) and import the repository.
3. Leave the defaults (no build command or output directory).
4. Click **Deploy**.

Later pushes to the production branch create new deployments automatically.

### CLI

```bash
npm install -g vercel
vercel login
vercel
```

The first `vercel` run creates a preview deployment and links the project. Promote it to production with:

```bash
vercel --prod
```

After deploy, the same paths work on your Vercel URL, for example `https://<project>.vercel.app/about`.

## How it works

`index.js` exports the Express app so Vercel can handle incoming requests. `app.listen()` only runs when you start the file directly (`npm start`), so local development still works.

```js
module.exports = app;

if (require.main === module) {
  app.listen(process.env.PORT || 3000);
}
```

This demo has no database, auth, or persistent disk. In-memory state will not survive between serverless invocations.

## Project layout

```
.
├── index.js          # Express app and routes
├── package.json
├── package-lock.json
└── README.md
```
