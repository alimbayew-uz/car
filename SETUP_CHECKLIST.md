# 🚀 Setup & Deployment Checklist

Complete this checklist to get your 3D Multiplayer Car Game live!

## Phase 1: Local Setup (15 minutes)

### Firebase Project
- [ ] Create Firebase project at https://console.firebase.google.com
- [ ] Name it: `3d-car-game` or your preferred name
- [ ] Enable Google Analytics (optional)
- [ ] Project created successfully

### Firebase Authentication
- [ ] Go to Firebase Console > Authentication
- [ ] Click "Get Started"
- [ ] Enable "Email/Password" provider
- [ ] Toggle enabled and save
- [ ] Disable "Anonymous" if enabled

### Firestore Database
- [ ] Go to Firebase Console > Firestore Database
- [ ] Click "Create database"
- [ ] Select "Start in test mode" (for development)
- [ ] Choose your region (select nearest to you)
- [ ] Click "Create"
- [ ] Database is now ready

### Get Firebase Config
- [ ] Go to Firebase Project Settings (⚙️ icon)
- [ ] Click "Your apps" section
- [ ] Click "Add app" and select Web (</> icon)
- [ ] Register app with name: "Web Car Game"
- [ ] Copy the Firebase config object

### Configure Project Files
- [ ] Download all files from this project
- [ ] Place in a folder: `3d-car-game/`
- [ ] Open `index.html` in a text editor
- [ ] Find line ~770: `const firebaseConfig = {...}`
- [ ] Replace with YOUR Firebase config:
  ```javascript
  const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_AUTH_DOMAIN",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_STORAGE_BUCKET",
      messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
      appId: "YOUR_APP_ID"
  };
  ```
- [ ] Save `index.html`

### Test Locally
- [ ] Open terminal in project folder
- [ ] Run: `python -m http.server 8000`
  - Or: `npx http-server`
  - Or: `python3 -m http.server 8000`
- [ ] Open browser to `http://localhost:8000`
- [ ] You should see the login screen
- [ ] ✅ Local setup complete!

## Phase 2: Test Game Locally (10 minutes)

### Test Authentication
- [ ] Click "Register here" to go to register page
- [ ] Enter email: `test@example.com`
- [ ] Enter username: `testuser`
- [ ] Enter password: `Test123456`
- [ ] Enter confirm password: `Test123456`
- [ ] Click "Register"
- [ ] You should be redirected to login
- [ ] Enter same email and password
- [ ] Click "Login"
- [ ] You should see the lobby screen ✅

### Test Lobby
- [ ] You're now logged in to the lobby
- [ ] See your email in top right ✅
- [ ] See "No available rooms" message
- [ ] Click "Create Room" button
- [ ] You should see the map editor screen ✅

### Test Map Editor
- [ ] Map editor shows a 32x32 grid
- [ ] Wall tool is selected (blue button)
- [ ] Draw some walls by clicking/dragging on the canvas
- [ ] Switch to Road tool (gray button)
- [ ] Draw some roads
- [ ] Switch to Eraser and erase some areas
- [ ] Click "Complete & Start" button
- [ ] Loading screen appears
- [ ] Car selection screen loads ✅

### Test Car Selection
- [ ] See car grid with 20 cars
- [ ] Click a car to select it (should highlight blue)
- [ ] See "Players Online" section at bottom left
- [ ] Check "I'm Ready!" checkbox
- [ ] "Start Game" button should still be disabled (need 2+ players)
- [ ] Logout and login as different user
- [ ] Join the same room
- [ ] Repeat: select car, mark ready
- [ ] Both players ready = "Start Game" button enabled ✅

### Test 3D Gameplay
- [ ] Click "Start Game"
- [ ] Wait for game to load
- [ ] You should see a 3D scene with your map
- [ ] Press W to move forward
- [ ] Press A/D to turn
- [ ] See HUD in top-left with position and speed
- [ ] See other player's car on the track
- [ ] Other player should see your car move too ✅
- [ ] Click "Exit Game" to return to lobby ✅

### Test Multiplayer Sync
- [ ] Open game in 2 browser windows
- [ ] Log in as 2 different users
- [ ] Create a room as player 1
- [ ] Draw map and complete
- [ ] Player 2 joins the room
- [ ] Both select cars and mark ready
- [ ] Start game
- [ ] Player 1 moves their car
- [ ] Player 2 should see Player 1's car moving
- [ ] Player 2 moves their car
- [ ] Player 1 should see Player 2's car moving
- [ ] ✅ Multiplayer sync is working!

## Phase 3: GitHub Setup (5 minutes)

### Create GitHub Repository
- [ ] Go to https://github.com/new
- [ ] Repository name: `3d-car-game`
- [ ] Description: "Real-time 3D Multiplayer Car Racing Game"
- [ ] Select "Public" (recommended for portfolio)
- [ ] Do NOT initialize README (we have our own)
- [ ] Click "Create repository"
- [ ] GitHub gives you setup instructions

### Push Code to GitHub
- [ ] Open terminal in project folder
- [ ] Run:
  ```bash
  git init
  git add .
  git commit -m "Initial commit: 3D Multiplayer Car Game"
  git branch -M main
  git remote add origin https://github.com/YOUR_USERNAME/3d-car-game.git
  git push -u origin main
  ```
- [ ] ✅ Code is now on GitHub!

### Verify on GitHub
- [ ] Go to https://github.com/YOUR_USERNAME/3d-car-game
- [ ] You should see:
  - [ ] `index.html` (main game file)
  - [ ] `README.md` (documentation)
  - [ ] `FIREBASE_SETUP.md`
  - [ ] `NETLIFY_DEPLOYMENT.md`
  - [ ] `DEVELOPMENT_GUIDE.md`
  - [ ] `netlify.toml`
  - [ ] `.gitignore`

## Phase 4: Deploy to Netlify (5 minutes)

### Connect GitHub to Netlify
- [ ] Go to https://netlify.com
- [ ] Sign up or login (GitHub recommended)
- [ ] Click "New site from Git"
- [ ] Select "GitHub" as provider
- [ ] Authorize Netlify on GitHub
- [ ] Select your `3d-car-game` repository
- [ ] Build settings:
  - [ ] Build command: (leave empty)
  - [ ] Publish directory: `.` (or leave empty)
- [ ] Click "Deploy site"
- [ ] Wait for deployment to complete (should take < 1 minute)
- [ ] You'll get a URL like: `https://your-site-name.netlify.app`
- [ ] ✅ Your game is LIVE!

### Test Live Site
- [ ] Go to your Netlify URL
- [ ] You should see the login screen
- [ ] Test login/register
- [ ] Create a room
- [ ] Draw map
- [ ] Select car
- [ ] ✅ Live site works!

### Enable Auto-Deploy
- [ ] Back in Netlify Dashboard
- [ ] Go to **Deploys** tab
- [ ] You should see your recent deployment
- [ ] It's already set up for auto-deploy!
- [ ] Future pushes to GitHub = automatic deployment

## Phase 5: Custom Domain (Optional - 5 minutes)

### Buy Domain (Optional)
- [ ] Buy domain from:
  - [ ] GoDaddy
  - [ ] Namecheap
  - [ ] Google Domains
  - [ ] Or use your registrar
- [ ] Domain cost: $5-15/year

### Connect Domain to Netlify
- [ ] In Netlify Dashboard, go to your site
- [ ] Click "Domain settings"
- [ ] Click "Add custom domain"
- [ ] Enter your domain (e.g., `carrace.com`)
- [ ] Netlify shows DNS records to add
- [ ] Go to your domain registrar
- [ ] Update DNS settings with Netlify's records
- [ ] Wait 24-48 hours for propagation
- [ ] ✅ Your game is at your custom domain!

## Phase 6: Production Security (Important!)

### Update Firestore Security Rules
- [ ] Go to Firebase Console > Firestore > Rules
- [ ] Replace test rules with production rules
- [ ] Copy from `FIREBASE_SETUP.md` section "Production Security Rules"
- [ ] Click "Publish"
- [ ] ✅ Your database is now secure!

### Set Up Firestore Backups (Optional)
- [ ] Firebase Console > Firestore > Backups
- [ ] Enable daily automatic backups
- [ ] ✅ Your data is protected!

### Enable Billing (If using beyond free tier)
- [ ] Firebase Console > Upgrade to Blaze plan
- [ ] Link credit card
- [ ] Set up billing alerts
- [ ] ✅ You can scale beyond free tier limits!

## Phase 7: Monitor & Maintain

### Set Up Netlify Alerts
- [ ] Netlify Dashboard > Site settings > Notifications
- [ ] Add email or Slack notifications
- [ ] Choose: Build failures, Deploy success, etc.
- [ ] ✅ You'll know if something goes wrong!

### Monitor Firebase Usage
- [ ] Firebase Console > Dashboard
- [ ] Check daily active users
- [ ] Monitor Firestore reads/writes
- [ ] Monitor storage usage
- [ ] ✅ Stay under free tier limits!

### Regular Maintenance
- [ ] Monthly: Check Firebase Console for errors
- [ ] Monthly: Review player feedback
- [ ] Quarterly: Update dependencies (if applicable)
- [ ] Quarterly: Test on new browsers/devices

## Phase 8: Share & Market (Optional)

### Share with Friends
- [ ] Copy your game URL
- [ ] Share on:
  - [ ] Discord
  - [ ] Twitter/X
  - [ ] Reddit (r/webgames)
  - [ ] Facebook
  - [ ] Email
- [ ] ✅ Get players!

### Build a Community
- [ ] Create Discord server
- [ ] Share game updates
- [ ] Gather feedback
- [ ] Plan new features
- [ ] Build player base

### Content Marketing
- [ ] Create gameplay video
- [ ] Post on YouTube
- [ ] Submit to game websites:
  - [ ] itch.io
  - [ ] Kongregate
  - [ ] Armor Games
- [ ] Write blog post
- [ ] Share on social media

## Troubleshooting Checklist

### Can't Deploy to Netlify
- [ ] Check GitHub is connected
- [ ] Check repository is public
- [ ] Check all files are pushed to GitHub
- [ ] Check internet connection
- [ ] Try re-authenticating Netlify

### Live Site Shows Error
- [ ] Check Firebase config is correct
- [ ] Check Firestore database exists
- [ ] Check Firestore security rules allow reads
- [ ] Check browser console (F12) for errors
- [ ] Try clearing cache (Ctrl+Shift+Delete)

### Game Works Locally But Not Live
- [ ] Check Firebase config (must be public key)
- [ ] Verify all CDN links load (F12 > Network tab)
- [ ] Check Netlify logs for errors
- [ ] Clear browser cache

### Other Players Not Visible Live
- [ ] Check Firestore sync is working
- [ ] Try refreshing page
- [ ] Check internet is stable
- [ ] Verify Firebase security rules

## Final Checklist

- [ ] Firebase project created
- [ ] Firebase config updated in index.html
- [ ] Game tested locally (authentication, lobby, gameplay)
- [ ] Code pushed to GitHub
- [ ] Site deployed to Netlify
- [ ] Live site tested (login, create room, play)
- [ ] Firestore security rules updated for production
- [ ] Custom domain configured (optional)
- [ ] Netlify alerts set up
- [ ] Game shared with friends
- [ ] README.md links all working
- [ ] Documentation is clear
- [ ] All features tested
- [ ] Performance is acceptable
- [ ] Mobile testing completed
- [ ] ✅ READY FOR PRODUCTION!

## Next Steps

1. ✅ Complete all checklist items
2. 🎮 Play with friends!
3. 📊 Monitor Firebase usage
4. 🚀 Plan new features:
   - [ ] Leaderboard
   - [ ] Chat
   - [ ] Power-ups
   - [ ] Lap times
   - [ ] Custom skins
5. 📱 Build mobile app (React Native)
6. 💰 Monetize (ads, cosmetics, battle pass)

## Quick Reference

### Important URLs
- Firebase Console: https://console.firebase.google.com
- GitHub Repository: https://github.com/YOUR_USERNAME/3d-car-game
- Netlify Dashboard: https://app.netlify.com
- Your Game: https://your-site-name.netlify.app
- Custom Domain: https://yourdomain.com

### Key Files
- Main game: `index.html`
- Setup guide: `FIREBASE_SETUP.md`
- Deployment: `NETLIFY_DEPLOYMENT.md`
- Development: `DEVELOPMENT_GUIDE.md`

### Useful Commands
```bash
# Test locally
python -m http.server 8000

# Push to GitHub
git add .
git commit -m "Your message"
git push origin main

# Deploy with CLI
netlify deploy --prod
```

## Support Resources

- **Firebase Help**: https://firebase.google.com/support
- **Netlify Help**: https://support.netlify.com
- **Three.js Docs**: https://threejs.org/docs
- **GitHub Docs**: https://docs.github.com

## You're All Set! 🎉

Your 3D Multiplayer Car Game is now:
- ✅ Built
- ✅ Deployed
- ✅ Live
- ✅ Ready for players

**Share your game and have fun!**

Questions? Check the documentation files or open an issue on GitHub.

Happy racing! 🏎️
