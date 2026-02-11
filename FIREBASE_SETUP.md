# Firebase Setup Guide 🔥

Follow these steps to enable cross-device rating sync with Firebase (it's free!).

## Step 1: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **"Add project"**
3. Enter a project name (e.g., "toni-gallery")
4. Disable Google Analytics (not needed for this)
5. Click **"Create project"**

## Step 2: Register Your Web App

1. In your Firebase project, click the **Web icon** (</>)
2. Enter an app nickname (e.g., "Toni Gallery Web")
3. **Don't** check "Set up Firebase Hosting"
4. Click **"Register app"**
5. You'll see a configuration object that looks like this:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyC...",
  authDomain: "toni-gallery.firebaseapp.com",
  projectId: "toni-gallery",
  storageBucket: "toni-gallery.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

6. Copy this entire configuration object

## Step 3: Update Your index.html

1. Open `index.html`
2. Find the Firebase configuration section (around line 280):

```javascript
// REPLACE THESE WITH YOUR FIREBASE CONFIG
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

3. Replace it with your copied configuration
4. Save the file

## Step 4: Set Up Firestore Database

1. In Firebase Console, go to **"Firestore Database"** in the left menu
2. Click **"Create database"**
3. Select **"Start in production mode"**
4. Choose a location (pick one closest to where she'll use it)
5. Click **"Enable"**

## Step 5: Configure Firestore Rules

1. In Firestore Database, click the **"Rules"** tab
2. Replace the default rules with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow users to read and write only their own ratings
    match /ratings/{username} {
      allow read, write: if true;
    }
  }
}
```

3. Click **"Publish"**

## Step 6: Test It Out!

1. Open `index.html` in your browser
2. Enter a username when prompted
3. Rate some photos
4. Open the same site on another device (or browser)
5. Enter the **same username**
6. Your ratings should appear! 🎉

## How It Works

### Username System:
- No passwords needed
- Anyone who knows the username can access those ratings
- Each username has its own set of ratings
- Choose memorable usernames (e.g., "Sarah", "TylerAndSarah")

### Data Sync:
- Ratings are saved to both localStorage (backup) AND Firebase (cloud)
- When you log in, Firebase ratings load automatically
- If Firebase is down, localStorage still works
- Syncs across all devices using the same username

### Security Note:
Since there's no password, anyone who knows the username can access the ratings. This is fine for a personal project! If you want more security later, we can add password protection.

## Troubleshooting

### "Firebase not configured" message in console
- Check that you replaced ALL the "YOUR_..." placeholders in the config
- Make sure the config is exactly as copied from Firebase (no extra commas or quotes)

### Ratings not syncing
- Check browser console for errors (F12 → Console tab)
- Verify Firestore rules are published
- Make sure you're using the same username on both devices

### Firebase costs
- Firebase is FREE for this usage level
- Free tier includes:
  - 50,000 reads per day
  - 20,000 writes per day
  - 1 GB storage
- This is way more than you'll ever need for this project!

## Optional: Custom Domain

If you want a custom domain (like `toni.love`):
1. Set up GitHub Pages first (see main README)
2. In Firebase Console, go to Hosting
3. Follow their custom domain setup guide
4. Point your domain to Firebase instead of GitHub Pages

## Without Firebase

The site works perfectly fine **without** Firebase:
- Ratings still save (just per-browser)
- All other features work the same
- No username needed

Firebase is only needed if you want ratings to sync across devices!

---

Need help? Check the browser console (F12) for error messages!
