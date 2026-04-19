# Deployment Guide for GitHub Pages

## Prerequisites
- Git installed on your computer
- Node.js and pnpm installed
- Your GitHub repository ready

## Option 1: Automatic Deployment with GitHub Actions (Recommended)

### Initial Setup

1. **Configure your repository name in vite.config.ts**
   
   If your repo is `https://github.com/yourusername/portfolio`:
   - For `yourusername.github.io` repo: keep `base: '/'`
   - For other repos: change to `base: '/repository-name/'`

2. **Push your code to GitHub**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/yourusername/your-repo.git
   git branch -M main
   git push -u origin main
   ```

3. **Enable GitHub Pages**
   - Go to your repository on GitHub
   - Click **Settings** → **Pages**
   - Under "Source", select **GitHub Actions**

4. **Automatic Deployment**
   - Every push to `main` will automatically build and deploy
   - Check the **Actions** tab to see deployment progress
   - Your site will be live at: `https://yourusername.github.io/repository-name/`

## Option 2: Manual Deployment

1. **Install gh-pages package**
   ```bash
   pnpm add -D gh-pages
   ```

2. **Build and deploy**
   ```bash
   pnpm run build
   pnpm run deploy
   ```

3. **Enable GitHub Pages**
   - Go to Settings → Pages
   - Under "Source", select **Deploy from a branch**
   - Select **gh-pages** branch
   - Click Save

## Custom Domain (Optional)

1. Add a file named `CNAME` in the `public` folder with your domain:
   ```
   yourdomain.com
   ```

2. Configure DNS settings at your domain provider:
   - Add A records pointing to GitHub's IPs
   - Or add a CNAME record pointing to `yourusername.github.io`

3. In GitHub Settings → Pages → Custom domain, enter your domain

## Troubleshooting

### Blank page after deployment
- Check that `base` in `vite.config.ts` matches your repo name
- Ensure GitHub Pages is enabled in repository settings

### Images not loading
- Verify all images are in the `src/imports` folder
- Check import paths are correct

### Build fails
- Run `pnpm install` to ensure all dependencies are installed
- Check the Actions tab for detailed error messages

## Local Development

Test your build locally before deploying:
```bash
pnpm run build
pnpm run preview
```

Visit http://localhost:4173 to preview the production build.

## Updates

To update your site:
1. Make changes to your code
2. Commit and push to GitHub
3. GitHub Actions will automatically rebuild and deploy

Or manually:
```bash
pnpm run deploy
```
