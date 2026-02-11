# 📦 Batch Upload & Tag Editing - Quick Reference

## 🚀 Quick Start

### Batch Upload Multiple Photos

1. **Click or drag** multiple photos onto the "📸 Upload New Photo" area
2. **Preview** all selected photos in the grid
3. **Tag each photo**:
   - Click the 🏷️ **Tag** button under each photo
   - Select moods (you can pick multiple!)
   - Click **💾 Save**
4. **Remove** any unwanted photos (click the ✕ in top-right corner)
5. **Click "⬆️ Upload All"** when ready
6. **Wait** for progress: "Uploading 1/5", "Uploading 2/5", etc.
7. **Done!** Photos appear in gallery immediately

### Edit Tags on Existing Photos

1. **Scroll to "⭐ Your Favorites"** section
2. **Find the photo** you want to edit
3. **Click "✏️ Edit"** button on the photo
4. **Select/deselect moods** (click to toggle)
5. **Click "💾 Save Changes"**
6. **Done!** Tags updated everywhere

---

## 🎯 Keyboard Shortcuts (Same as Before)

- **Spacebar** or **→**: Next random photo
- **1-5**: Rate photo with that many hearts
- **↓**: Download current photo

---

## 🏷️ Available Mood Tags

- 😤 **Unbridled Rage** - Angry, frustrated, annoyed moments
- 😴 **Lazy Boy** - Calm, relaxed, sleeping, lounging
- 😇 **Sweet Perfect Angel Cat** - Cute, sweet, adorable moments
- 🤪 **Weirdo** - Funny, bizarre, quirky behaviors

**Note:** You can select multiple moods per photo!

---

## ✅ What Gets Validated During Upload

- ✅ **File Type**: Only JPG, JPEG, PNG allowed
- ✅ **File Size**: Must be under 10MB per photo
- ✅ **Duplicates**: Automatically detected and skipped (using SHA-256 hash)

---

## 💡 Pro Tips

### For Uploading
- Select 5-10 photos at a time to start
- Tag consistently (makes filtering easier later)
- Preview before uploading to catch mistakes
- Don't forget to add moods! (At least one per photo)

### For Editing
- Review favorites regularly
- Fix tagging mistakes immediately
- Add moods you initially forgot
- Remove incorrect tags

### For Organization
- Use multiple tags when appropriate
- "Lazy Boy" + "Sweet Angel" = sleepy cuteness
- "Weirdo" + "Unbridled Rage" = hilariously angry
- Be consistent with your tagging logic

---

## 🐛 Common Issues & Fixes

| Problem | Solution |
|---------|----------|
| "No valid files to upload" | Check file types (JPG/PNG only) and sizes (under 10MB) |
| Some photos skipped | Read alert messages - they explain why each was skipped |
| Upload fails partway | Check internet connection, note which succeeded, retry failed ones |
| Changes don't save | Check Firestore connection, refresh page, try again |
| Can't find Edit button | Only appears in Favorites section, not on main photo |

---

## 📊 What Happens Behind the Scenes

### Batch Upload
```
Select files → Validate → Preview → Tag → Upload to Cloudinary → Save to Firestore → Add to gallery
```

### Tag Editing
```
Click Edit → Load current tags → Modify → Save to Firestore → Update display
```

### Data Storage
- **Cloudinary**: Photo files (free tier: 25 GB storage, 25 GB bandwidth/month)
- **Firestore**: Photo metadata and tags (free tier: 1 GB storage, 50K reads, 20K writes per day)
- **LocalStorage**: Backup data and duplicate detection hashes

---

## 📱 Works On

- ✅ Desktop (Chrome, Firefox, Safari, Edge)
- ✅ Mobile phones (iOS Safari, Android Chrome)
- ✅ Tablets (iPad, Android tablets)
- ✅ Touch and mouse supported

---

## 🎁 Perfect For

- 📸 **After a photoshoot** - Upload all at once
- 🌅 **End of the day** - Add today's photos quickly
- 🎉 **Special occasions** - Batch upload event photos
- 🧹 **Organization** - Re-tag and organize existing collection
- 💕 **Gifting** - Easy for both of you to contribute

---

## 📚 More Information

- **Complete Guide**: `BATCH_UPLOAD_GUIDE.md`
- **Implementation Details**: `BATCH_TAG_IMPLEMENTATION.md`
- **Main README**: `README.md`
- **Cloudinary Setup**: `CLOUDINARY_SETUP.md`
- **Firebase Setup**: `FIREBASE_SETUP.md`

---

## 🆘 Need Help?

1. Check the relevant .md guide file
2. Check browser console for error messages
3. Try refreshing the page
4. Verify Cloudinary and Firebase are configured correctly
5. Check your internet connection

---

**Made with 💜 for your girlfriend and Toni the cat!** 🐱✨
