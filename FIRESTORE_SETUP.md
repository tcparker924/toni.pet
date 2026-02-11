# 🔥 Firestore Setup Guide for Toni Gallery

## Why Firestore is Needed

**The Problem:** Cloudinary stores your photos, but there's no way for different users' browsers to know about newly uploaded photos without manually refreshing or checking Cloudinary's API repeatedly.

**The Solution:** Firestore acts as a **shared database** that:
1. ✅ Stores metadata about each photo (URL, moods, uploader, timestamp)
2. ✅ Syncs in **real-time** across all users' browsers
3. ✅ When anyone uploads a photo, ALL users see it instantly
4. ✅ Provides a single source of truth for the gallery

## How It Works

```
User uploads photo
    ↓
Photo → Cloudinary (stores actual image file)
    ↓ Returns URL
Metadata → Firestore (stores URL + moods + info)
    ↓
Firestore broadcasts to all connected browsers
    ↓
All users see the new photo instantly!
```

## Current Setup Steps

### Step 1: Create Firestore Database (If Not Already Done)

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Select your project: **toni-pet**
3. In the left sidebar, click **"Firestore Database"**
4. If you see "Get Started", click it
5. Choose **"Start in production mode"** (we'll update rules next)
6. Select a location (choose closest to your users, e.g., `us-central`)
7. Click **"Enable"**

### Step 2: Set Up Security Rules

This is **CRITICAL** - without proper security rules, your app can't read or write photos!

1. In Firestore Database, click the **"Rules"** tab
2. Replace the existing rules with:

```javascript
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    
    // Photos collection - Allow everyone to read and write
    // (Since this is a private family gallery)
    match /photos/{photoId} {
      allow read: if true;  // Anyone can view photos
      allow write: if true; // Anyone can upload photos
      allow delete: if true; // Anyone can delete photos (optional, can restrict)
    }
    
    // Ratings collection - Allow everyone to read and write ratings
    match /ratings/{ratingId} {
      allow read: if true;
      allow write: if true;
    }
    
    // Block all other collections by default
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

3. Click **"Publish"**

### Step 3: Verify Connection

1. Open your website in a browser
2. Open **Developer Console** (F12)
3. Look for these messages:
   ```
   ✅ Firebase initialized successfully!
   📡 Setting up real-time photo sync from Firestore...
   ✅ Firestore listener set up successfully!
   ```

### Step 4: Test Upload

1. Upload a photo through your website
2. Check the console for:
   ```
   ✅ Photo metadata saved to Firestore successfully! Doc ID: xxxxx
   ```
3. Open a **second browser window** (or incognito window)
4. The photo should appear in both windows!

### Step 5: Verify Firestore Data

1. Go back to Firebase Console → Firestore Database
2. You should now see a **"photos"** collection
3. Click on it to see all uploaded photos
4. Each document should have:
   - `path` (Cloudinary URL)
   - `cloudinaryId` (Cloudinary public ID)
   - `fileHash` (for duplicate detection)
   - `moods` (array of mood tags)
   - `uploadedBy` (username)
   - `uploadedAt` (timestamp)

## Troubleshooting

### Problem: "Permission Denied" errors

**Symptom:** Console shows:
```
❌ Error in Firestore snapshot listener: permission-denied
🚫 PERMISSION DENIED: Firestore security rules are blocking access!
```

**Solution:** 
1. Check that you published the security rules in Step 2
2. Rules might take 1-2 minutes to propagate
3. Hard refresh your browser (Ctrl+Shift+R)

### Problem: Photos upload but don't appear for other users

**Symptom:** Photos work in localStorage but not across browsers

**Solution:**
1. Check console for Firestore errors
2. Verify Firebase is initialized: Look for "Firebase initialized successfully!"
3. Check that the `photos` collection exists in Firestore console
4. Verify security rules are published

### Problem: No Firestore initialization

**Symptom:** Console shows:
```
⚠️ Firestore not available, loading from localStorage only
```

**Solution:**
1. Check that Firebase SDK is loaded (view page source, look for firebase scripts)
2. Verify `firebaseConfig` has correct credentials
3. Check browser console for any script loading errors

### Problem: Duplicate window.addEventListener('load')

**Fixed!** The code had two load event listeners that were conflicting. This has been resolved.

## Data Structure

### Photos Collection (`photos`)

Each document in the `photos` collection has this structure:

```javascript
{
  path: "https://res.cloudinary.com/dhjs7c8ix/image/upload/v1234567890/toni-gallery/photo.jpg",
  cloudinaryId: "toni-gallery/photo",
  fileHash: "abc123def456...",
  moods: ["unbridled_rage", "total_zen"],
  uploadedBy: "Tyler",
  uploadedAt: Timestamp(2024, 2, 11, 10, 30, 0)
}
```

### Ratings Collection (`ratings`)

Each document in the `ratings` collection has this structure:

```javascript
{
  photoUrl: "https://res.cloudinary.com/.../photo.jpg",
  ratings: {
    "Tyler": 5,
    "Sarah": 4,
    "Mom": 5
  }
}
```

## Real-Time Sync Explanation

The app uses Firestore's `onSnapshot()` listener:

```javascript
db.collection('photos')
  .orderBy('uploadedAt', 'desc')
  .onSnapshot((snapshot) => {
    // This function runs:
    // 1. On initial page load
    // 2. Whenever ANY document is added/modified/deleted
    // 3. In real-time across ALL connected browsers
    
    // Update the photo gallery
    catPhotos.length = 0;
    snapshot.forEach(doc => {
      catPhotos.push(doc.data());
    });
    
    // Refresh the display
    loadRandomPhoto();
  });
```

This means:
- **No polling** - Firestore pushes updates to browsers
- **Instant sync** - Sub-second latency typically
- **Automatic reconnection** - If internet drops, it catches up when reconnected

## Security Considerations

### Current Setup (Family Gallery)

The current rules allow **anyone** to read and write. This is fine for:
- ✅ Private family websites
- ✅ Sites behind authentication elsewhere
- ✅ Sites with access codes (like your secret code system)

### If You Need Stricter Security

If you want to add Firestore-level authentication:

```javascript
// Require authentication for uploads
match /photos/{photoId} {
  allow read: if true;  // Anyone can view
  allow create: if request.auth != null;  // Must be logged in to upload
  allow delete: if request.auth != null && request.auth.uid == resource.data.uploaderId;
}
```

Then you'd need to add Firebase Authentication (see Firebase docs).

## Cost Information

**Firestore Free Tier (Spark Plan):**
- ✅ 50,000 reads/day
- ✅ 20,000 writes/day
- ✅ 20,000 deletes/day
- ✅ 1GB storage

**Typical Usage for Your Gallery:**
- Each page load: 1 read per photo
- Each upload: 1 write
- Real-time listeners: Count as 1 read per document initially, then only changed documents

**Example:** 
- 100 photos in gallery
- 10 family members viewing daily
- 5 new photos uploaded daily
- **Daily usage:** ~1,000 reads + 5 writes = Well within free tier!

## Backup Strategy

The app uses **both** Firestore and localStorage:

1. **Primary:** Firestore (shared, real-time)
2. **Backup:** localStorage (local browser cache)

If Firestore is down:
- Users can still see photos from their browser's cache
- New uploads save to localStorage
- When Firestore comes back, photos sync

## Next Steps

1. ✅ Set up Firestore database
2. ✅ Publish security rules
3. ✅ Test upload from one browser
4. ✅ Verify it appears in a second browser
5. ✅ Check Firestore console to see the data

## Questions?

If you see any errors in the console, copy them and I can help diagnose!

Common logs to check:
- `Firebase initialized successfully!` - Firebase is working
- `Firestore listener set up successfully!` - Real-time sync is active
- `Photo metadata saved to Firestore successfully!` - Uploads are working
- `Firestore snapshot received: X photos` - Photos are loading
