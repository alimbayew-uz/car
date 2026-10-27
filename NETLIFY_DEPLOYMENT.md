# Netlify Deployment Guide - 3D Multiplayer Car Game

## Quick Start (5 Minutes)

### Option 1: Direct GitHub Integration (Recommended)

1. **Push to GitHub**
   ```bash
   cd your-project-folder
   git init
   git add index.html FIREBASE_SETUP.md NETLIFY_DEPLOYMENT.md
   git commit -m "Initial commit: 3D Car Game"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/3d-car-game.git
   git push -u origin main
   ```

2. **Connect to Netlify**
   - Go to [Netlify](https://netlify.com)
   - Sign up/login with GitHub
   - Click "New site from Git"
   - Select "GitHub"
   - Authorize Netlify to access GitHub
   - Select your repository
   - Basic build settings:
     - **Build command**: (leave empty - no build needed)
     - **Publish directory**: `.` (root directory)
   - Click "Deploy site"

3. **Done!** Your site is now live at `https://your-site-name.netlify.app`

### Option 2: Manual Deployment (Drag & Drop)

1. Go to [Netlify](https://netlify.com)
2. Sign up/login
3. Click "Create a new site" > "Deploy manually"
4. Drag and drop your `index.html` file
5. Site is deployed immediately

### Option 3: Netlify CLI

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Login to Netlify
netlify login

# Deploy
netlify deploy --prod --dir=.

# Or deploy with a folder
netlify deploy --prod --open
```

## GitHub Setup (Detailed)

### 1. Create GitHub Repository

```bash
# Initialize git in your project directory
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit: 3D Multiplayer Car Game"

# Create main branch
git branch -M main

# Add remote (replace with your GitHub URL)
git remote add origin https://github.com/USERNAME/3d-car-game.git

# Push to GitHub
git push -u origin main
```

### 2. Connect GitHub to Netlify

1. Go to [Netlify Dashboard](https://app.netlify.com)
2. Click "New site from Git"
3. Choose "GitHub" as provider
4. Authorize Netlify app on GitHub
5. Select your `3d-car-game` repository
6. Configure:
   - **Build command**: Leave empty
   - **Publish directory**: `.` (or leave empty)
7. Click "Deploy site"

### 3. Wait for Deployment

Netlify will:
1. Clone your repository
2. Detect it's a static site
3. Deploy to their CDN
4. Assign a temporary URL

## Custom Domain

1. In Netlify Dashboard, go to your site
2. Click "Domain settings"
3. Click "Add custom domain"
4. Enter your domain (e.g., `carrace.com`)
5. Follow DNS configuration instructions
6. Wait 24-48 hours for DNS propagation

### Update DNS for Custom Domain

If using external registrar:

1. In Netlify, copy the DNS records (usually CNAME or A records)
2. Log into your domain registrar (GoDaddy, Namecheap, etc.)
3. Update DNS settings
4. Paste Netlify's DNS records
5. Save and wait for propagation

## Environment Variables (Firebase Config)

### Option 1: Hardcoded in HTML (Current - OK for Dev)

Firebase config is embedded in `index.html`. This is fine for public web apps since Firebase has built-in security.

### Option 2: Netlify Secrets (If you want extra security)

1. In Netlify Dashboard, go to **Site settings** > **Build & deploy** > **Environment**
2. Add new variables:
   - `FIREBASE_API_KEY`
   - `FIREBASE_PROJECT_ID`
   - etc.
3. Update your HTML to use `window.ENV`:

```javascript
// This would require a build step (not recommended for this project)
const firebaseConfig = {
    apiKey: window.ENV.FIREBASE_API_KEY,
    // ...
};
```

For this project, keeping the config in HTML is fine since Firebase has security rules.

## Build Optimization

### Current Setup (No Build Step Needed)

This project is a single HTML file with no build process needed. It's:
- Fast to deploy
- Works instantly
- No build time

### Optional: Add Build Optimization

If you want to optimize in the future:

```toml
# netlify.toml file (create in root)
[build]
  command = ""
  publish = "."

[context.production]
  environment = { NEXT_PUBLIC_FIREBASE_KEY = "..." }

[[headers]]
  for = "/*.js"
  [headers.values]
    Cache-Control = "public, max-age=31536000"

[[headers]]
  for = "/index.html"
  [headers.values]
    Cache-Control = "no-cache"
```

## Automatic Deployments

Once connected to GitHub:

1. Make changes locally
2. Commit and push to main branch:
   ```bash
   git add .
   git commit -m "Update game features"
   git push origin main
   ```
3. Netlify automatically deploys within seconds
4. Get notifications when deploy is complete

## Monitor Deployments

1. In Netlify Dashboard, go to **Deploys**
2. See build logs and deployment history
3. Click on any deploy to see details
4. Rollback to previous version if needed

## Performance

- **CDN**: Netlify uses Fastly edge network globally
- **HTTPS**: Free SSL certificate (auto-renewed)
- **Assets**: Compressed and served from nearest edge location
- **Load time**: Typically < 1 second

## Enable Analytics (Optional)

1. In Netlify Dashboard, go to **Analytics**
2. Click "Enable Netlify Analytics"
3. View visitor stats, page views, etc.

## Enable Forms (Optional - For Future)

If you want to add a contact form:

1. Add `netlify` attribute to forms:
   ```html
   <form name="contact" netlify>
     <!-- form fields -->
   </form>
   ```
2. Form submissions appear in Netlify Dashboard > Forms
3. Set up email notifications

## Troubleshooting

### "Page Not Found" Error

**Problem**: Getting 404 on custom routes

**Solution**: For single-page apps, update `netlify.toml`:
```toml
[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

But this game doesn't use client routing, so not needed.

### Firebase Authentication Not Working

**Problem**: Auth fails with CORS errors

**Solution**: 
- Firebase CDN handles CORS automatically
- Check Firebase config is correct
- Clear browser cache and cookies
- Check Firestore security rules allow authenticated users

### Map Data Not Loading

**Problem**: Map appears blank after joining room

**Solution**:
- Verify room creator completed map
- Check Firestore has mapData field
- Look at browser console for errors
- Verify Firestore rules allow reads

### Three.js Not Loading

**Problem**: Game screen shows black

**Solution**:
- Check CDN link for Three.js is working
- Open browser DevTools > Console for errors
- Verify graphics hardware supports WebGL
- Try in Chrome/Firefox (best compatibility)

### Slow Performance

**Problem**: Game lag or stuttering

**Solution**:
- Reduce sync rate from 100ms to 200ms
- Reduce camera view distance in fog
- Lower player count in room
- Use Chrome for best performance

## Advanced: Deploy Preview

For pull requests:

1. Push feature branch to GitHub:
   ```bash
   git checkout -b feature/my-feature
   git push origin feature/my-feature
   ```
2. Open pull request
3. Netlify automatically creates preview URL
4. Test changes before merging
5. See preview link in PR

## Monitoring & Alerts

### Set Up Netlify Notifications

1. Go to **Site settings** > **Notifications**
2. Add Slack, email, or webhook notifications
3. Choose when to notify:
   - Build successful
   - Build failed
   - Deployment complete

## Backups & Version Control

Your site is automatically backed up in:
1. **GitHub**: Full version history
2. **Netlify**: Deployment history
3. Roll back anytime from Netlify Dashboard

## Cost

- **Free tier**: Unlimited bandwidth and builds
- **Paid plans**: Start at $19/month (optional features)
- **This project**: Runs completely free

## Next Steps

1. ✅ Deploy to Netlify
2. 📱 Test on mobile and desktop
3. 🔐 Update Firebase security rules for production
4. 🌍 Add custom domain
5. 📊 Monitor analytics
6. 🚀 Share with friends!

## Links

- [Netlify Docs](https://docs.netlify.com)
- [GitHub to Netlify](https://docs.netlify.com/integrations/repo-info/)
- [Site Configuration](https://docs.netlify.com/configure-builds/file-based-configuration/)
- [Netlify CLI](https://docs.netlify.com/cli/overview/)

## Support

- Netlify Status: https://status.netlify.com
- Netlify Community: https://community.netlify.com
- Support Email: support@netlify.com
