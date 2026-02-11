# 🔄 Photo Migration Guide

You have **TWO OPTIONS** to migrate your existing Cloudinary photos to Firestore:

---

## ✅ OPTION 1: Use Migration Tool (Recommended)

### Step 1: Open the Migration Tool

1. Open `migrate-photos.html` in your browser
2. This is a visual tool that guides you through migration

### Step 2: Choose Your Method

**Method A: Load from localStorage (Easiest)**
- If you've uploaded photos through the website before
- Click the **"📦 Load from localStorage Instead"** button
- URLs will auto-populate!

**Method B: Manual Entry from Cloudinary**
1. Go to [Cloudinary Console](https://cloudinary.com/console)
2. Click "Media Library" → "toni-gallery" folder
3. For each photo:
   - Click on the photo
   - Copy the "Secure URL" (looks like: `https://res.cloudinary.com/dhjs7c8ix/image/upload/...`)
4. Paste all URLs into the textarea (one per line)

### Step 3: Select Mood Tags

- Choose default mood tags for ALL photos
- You can update individual photos later in the gallery

### Step 4: Enter Your Name

- Enter who is uploading (e.g., "Tyler")

### Step 5: Click "Start Migration"

- Tool will process all photos
- Shows progress bar
- Logs success/failures
- Skips duplicates automatically

### Step 6: Verify

- Go back to your gallery (`index.html`)
- All photos should now appear for everyone!

### Step 7: Clean Up

- Delete `migrate-photos.html` file (you won't need it again)

---

## ⚡ OPTION 2: Quick Console Script (Advanced)

If you prefer to migrate directly from localStorage:

### Step 1: Open Your Gallery

Open `index.html` in your browser

### Step 2: Open Developer Console

Press **F12**, then click the "Console" tab

### Step 3: Paste This Script

```javascript
async function migrateLocalStorageToFirestore() {
    console.log('🚀 Starting migration from localStorage to Firestore...');
    
    // Get photos from localStorage
    const savedPhotos = JSON.parse(localStorage.getItem('uploadedPhotos') || '[]');
    
    if (savedPhotos.length === 0) {
        console.log('❌ No photos found in localStorage');
        return;
    }
    
    console.log(`📊 Found ${savedPhotos.length} photos in localStorage`);
    
    if (!db || !firebase) {
        console.log('❌ Firebase not initialized. Make sure you are on index.html');
        return;
    }
    
    let successCount = 0;
    let skipCount = 0;
    let errorCount = 0;
    
    for (let i = 0; i < savedPhotos.length; i++) {
        const photo = savedPhotos[i];
        
        try {
            // Check if already exists in Firestore
            const existingQuery = await db.collection('photos')
                .where('path', '==', photo.path)
                .get();
            
            if (!existingQuery.empty) {
                console.log(`⚠️ Skipping duplicate: ${photo.path}`);
                skipCount++;
                continue;
            }
            
            // Add to Firestore
            await db.collection('photos').add({
                path: photo.path,
                cloudinaryId: photo.cloudinaryId || 'unknown',
                fileHash: photo.hash || photo.fileHash || 'unknown',
                moods: photo.moods || ['unbridled_rage'],
                uploadedBy: photo.uploadedBy || currentUser || 'Unknown',
                uploadedAt: photo.uploadedAt ? 
                    firebase.firestore.Timestamp.fromDate(new Date(photo.uploadedAt)) : 
                    firebase.firestore.FieldValue.serverTimestamp(),
                migratedAt: firebase.firestore.FieldValue.serverTimestamp()
            });
            
            console.log(`✅ Migrated ${i + 1}/${savedPhotos.length}: ${photo.path}`);
            successCount++;
            
        } catch (error) {
            console.error(`❌ Failed to migrate: ${photo.path}`, error);
            errorCount++;
        }
    }
    
    console.log('\n🎉 Migration Complete!');
    console.log(`✅ Successful: ${successCount}`);
    console.log(`⚠️ Skipped (duplicates): ${skipCount}`);
    console.log(`❌ Failed: ${errorCount}`);
    console.log('\n💡 Refresh the page to see all photos synced!');
}

// Run the migration
migrateLocalStorageToFirestore();
```

### Step 4: Press Enter

The script will run and show progress in the console

### Step 5: Refresh the Page

Your photos should now be synced to Firestore!

---

## 🔍 How to Get Cloudinary URLs Manually

If localStorage is empty or you want to add specific photos:

### Method 1: From Cloudinary Console

1. Go to https://cloudinary.com/console
2. Click **"Media Library"**
3. Navigate to **"toni-gallery"** folder
4. Click on each photo
5. Copy the **"Secure URL"** from the right panel

Example URL:
```
https://res.cloudinary.com/dhjs7c8ix/image/upload/v1707687654/toni-gallery/cat-photo-1.jpg
```

### Method 2: From Browser Network Tab

1. Open your gallery
2. Press **F12** → **Network** tab
3. Filter by "Img"
4. Refresh the page
5. Look for Cloudinary image URLs
6. Right-click → Copy URL

### Method 3: From localStorage

1. Open your gallery
2. Press **F12** → **Console** tab
3. Paste this:

```javascript
const photos = JSON.parse(localStorage.getItem('uploadedPhotos') || '[]');
console.log('All photo URLs:');
photos.forEach((photo, i) => {
    console.log(`${i + 1}. ${photo.path}`);
});
```

---

## ✅ Verification Steps

After migration, verify it worked:

### 1. Check Console Logs
Look for:
```
✅ Photo metadata saved to Firestore successfully!
```

### 2. Check Firebase Console
1. Go to Firebase Console → Firestore Database
2. Look for `photos` collection
3. Should see documents with your photos

### 3. Test Multi-Device Sync
1. Open gallery in Browser 1
2. Open gallery in Browser 2 (or incognito)
3. Both should show the same photos!

---

## 🆘 Troubleshooting

### "No photos found in localStorage"

**Solution:** Use Option 1 (Migration Tool) and manually enter Cloudinary URLs

### "Firebase not initialized"

**Solution:** Make sure you're running the script on `index.html`, not a blank page

### "permission-denied" error

**Solution:** You need to set up Firestore security rules first (see QUICK_START.md)

### Photos not appearing after migration

**Solutions:**
1. Hard refresh the page (Ctrl+Shift+R)
2. Check browser console for errors
3. Verify Firestore listener is running: Look for "Firestore listener set up successfully!"
4. Check Firebase Console to verify documents were created

---

## 💡 Pro Tips

### Tip 1: Batch Process by Mood
If you have lots of photos with different moods:
- Migrate photos in batches
- Set different default moods for each batch
- Use the migration tool multiple times

### Tip 2: Keep localStorage as Backup
Don't clear localStorage after migration - it acts as a backup!

### Tip 3: Verify Before Deleting Migration Tool
- Test that photos appear in gallery
- Open in multiple browsers to confirm sync
- Then delete `migrate-photos.html`

### Tip 4: Use Photo Preview
The migration tool shows preview thumbnails so you can verify you're migrating the right photos

---

## 📊 What Gets Migrated

For each photo, these fields are saved to Firestore:

```javascript
{
  path: "https://res.cloudinary.com/.../photo.jpg",  // Cloudinary URL
  cloudinaryId: "toni-gallery/photo",                // Cloudinary public ID
  fileHash: "abc123...",                             // For duplicate detection
  moods: ["unbridled_rage", "total_zen"],           // Mood tags array
  uploadedBy: "Tyler",                               // Your username
  uploadedAt: Timestamp,                             // Original upload time
  migratedAt: Timestamp                              // Migration time (NEW!)
}
```

---

## ⏱️ How Long Does It Take?

- **1-10 photos:** ~5 seconds
- **10-50 photos:** ~30 seconds
- **50-100 photos:** ~2 minutes

The tool processes photos one at a time to avoid rate limits.

---

## 🎉 After Migration

Once migration is complete:

1. ✅ All photos visible to all users
2. ✅ Real-time sync active
3. ✅ Upload new photos through regular gallery
4. ✅ Delete migration tool
5. ✅ Enjoy your synchronized gallery!

---

## 🗑️ Cleanup

After successful migration:

1. Delete `migrate-photos.html`
2. (Optional) Keep localStorage as backup
3. Use regular gallery upload for new photos

---

## ❓ Need Help?

If you get stuck:
1. Check browser console (F12) for error messages
2. Verify Firestore is set up (see QUICK_START.md)
3. Try the console script method if migration tool doesn't work
4. Copy any error messages and I can help debug!
