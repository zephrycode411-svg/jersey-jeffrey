# Deploy the storefront to Vercel

This project uses a static Vercel deployment for the website and keeps the Flask API, SQLite database, and uploaded product images on the existing Render service. Vercel's function filesystem is temporary, so the store database and uploads should not be moved into a Vercel Function without first migrating them to persistent hosted services.

## Deploy

1. Push this repository to GitHub, GitLab, or Bitbucket.
2. In Vercel, select **Add New Project** and import the repository.
3. Keep the project root at the repository root. The included `vercel.json` builds the HTML, CSS, JavaScript, SVG, and image assets as static files and forwards `/api/*` and `/images/products/*` to Render.
4. Deploy. No Vercel environment variables are required for this frontend configuration.

The proxy destinations currently use `https://dej-jersey-store-api.onrender.com`, matching `netlify.toml`. If the Render service URL changes, update both destinations in `vercel.json` and redeploy. Before testing orders or the admin page, open `https://dej-jersey-store-api.onrender.com/api/health` and confirm it returns JSON containing `"status":"ok"`. A 404 means the Render service URL or deployed application route needs attention; changing frontend fetch URLs or CORS will not fix that.

## Local preview

Install the Vercel CLI, then run `vercel dev` from the repository root. The same proxy destinations are used in local preview.