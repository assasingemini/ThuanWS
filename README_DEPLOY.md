# Quick Deploy for Hugo → GitHub Pages

## 1) Create a new GitHub repo
- Go to GitHub → New repository
- Name it: <repo>
- Keep it Public (recommended)
- Do NOT add README for now

## 2) Prepare your local project
Copy this pack into the root of your Hugo project so it contains:

- .github/workflows/hugo.yml
- .gitignore

Optional: update `config.toml` or `config.yaml`:
```
baseURL = "https://<username>.github.io/<repo>/"
publishDir = "public"
relativeURLs = true
```

Also consider changing image links in your markdown from `/images/...` to `images/...`.

## 3) Initialize Git and push
```
git init
git add .
git commit -m "Initial Hugo site"
git branch -M main
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main
```

## 4) Enable Pages
- In GitHub, open your repo → Settings → Pages
- Source: **GitHub Actions**
- Wait for the workflow to finish (tab Actions).

## 5) Open your site
The URL will be shown in the deploy job log, typically:
`https://<username>.github.io/<repo>/`
