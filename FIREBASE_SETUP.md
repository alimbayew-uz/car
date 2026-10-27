# Firebase Configuration Guide - 3D Multiplayer Car Game

## Step 1: Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Create a project" or "Add project"
3. Name it: `3d-car-game` (or your preferred name)
4. Enable Google Analytics (optional)
5. Create the project

## Step 2: Set Up Authentication

1. In Firebase Console, go to **Authentication**
2. Click "Get Started"
3. Enable **Email/Password** sign-in:
   - Click on "Email/Password"
   - Toggle "Enabled"
   - Save

## Step 3: Create Firestore Database

1. In Firebase Console, go to **Firestore Database**
2. Click "Create database"
3. Select **Start in test mode** (for development; switch to production rules before deploying)
4. Choose a location (select nearest to your users)
5. Click "Create"

## Step 4: Get Firebase Config

1. Go to **Project Settings** (gear icon)
2. Click on "Your apps" section
3. Click "Add app" and select "Web" (</> icon)
4. Register your app with a name like "Web Car Game"
5. You'll see your Firebase config:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyDemoKeyHereReplace",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef123456"
};
```

## Step 5: Update index.html

Replace the Firebase config at the top of the `<script>` section in `index.html`:

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

## Step 6: Configure Firestore Security Rules

1. Go to **Firestore Database > Rules**
2. Replace with these rules for development (test mode):

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Development: Allow all reads/writes
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

For production, use stricter rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    
    // Users collection
    match /users/{userId} {
      allow read, write: if request.auth.uid == userId;
    }
    
    // Rooms collection
    match /rooms/{roomId} {
      allow read: if request.auth != null;
      allow create: if request.auth != null;
      allow update: if request.auth != null;
      
      // Players subcollection
      match /players/{playerId} {
        allow read: if request.auth != null;
        allow write: if request.auth.uid == playerId;
      }
    }
  }
}
```

## Step 7: Update Firestore Rules

1. Click "Publish"

## Step 8: Configure CORS (if needed)

For Netlify hosting, CORS should be automatically handled by Firebase CDN. No additional configuration needed.

## Step 9: Test the Setup

1. Open `index.html` locally
2. Try to register a new account
3. You should see the account in Firebase Console > Authentication
4. Create a room and verify data in Firestore

## Database Schema

### Collections

```
/users/{userId}
  - email: string
  - username: string
  - createdAt: timestamp

/rooms/{roomId}
  - creatorId: string
  - creatorEmail: string
  - status: 'waiting' | 'playing' | 'finished'
  - mapData: string (compressed array)
  - createdAt: timestamp
  - maxPlayers: number
  - players: map
  
  /players/{userId}
    - email: string
    - car: number
    - ready: boolean
    - position: { x, y, z }
    - rotation: number
    - joinedAt: timestamp
    - updatedAt: timestamp
```

## Troubleshooting

### "Failed to get Firestore instance"
- Check Firebase config is correct
- Verify Firestore database is created
- Check browser console for detailed error

### "Permission denied" errors
- Check Firestore Security Rules
- Use test mode for development
- Ensure user is authenticated

### CORS errors
- Firebase CDN handles CORS automatically
- Check your domain is added to authorized domains in Firebase Console

### Map data not syncing
- Verify Firestore is enabled
- Check network tab in browser DevTools
- Ensure map data is being saved as a string

## Performance Tips

1. **Sync Rate**: Currently set to 100ms. Increase for lower bandwidth:
   ```javascript
   }, 100); // Change to 200 or 500 for slower updates
   ```

2. **Map Size**: Currently 32x32 cells. Adjust `initMapEditor()` for larger maps:
   ```javascript
   canvas.width = 1024; // Larger canvas
   canvas.height = 1024;
   // Adjust cellSize calculation accordingly
   ```

3. **Player Limit**: Modify `maxPlayers` in createRoom():
   ```javascript
   maxPlayers: 8, // Change as needed
   ```

4. **Firestore Indexes**: As you scale, Firebase may suggest creating indexes. Follow the prompts.

## Production Deployment

Before deploying to production:

1. Switch from test mode to production rules (see above)
2. Enable authentication providers needed
3. Set up proper security rules
4. Enable Firestore backups (optional)
5. Monitor usage in Firebase Console
6. Set up billing alerts if not on free tier

## Pricing Notes

- **Authentication**: Free for first 50,000 monthly active users
- **Firestore**: Free tier includes 1 GB storage and 50k reads/day
- **Bandwidth**: Firebase handles CDN at no extra cost
- Monitor usage to avoid unexpected charges

## Support

- [Firebase Documentation](https://firebase.google.com/docs)
- [Firestore Security Rules Guide](https://firebase.google.com/docs/firestore/security/get-started)
- [Authentication Best Practices](https://firebase.google.com/docs/auth/best-practices)
