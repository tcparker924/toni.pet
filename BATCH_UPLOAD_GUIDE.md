# 📦 Batch Upload & Tag Editing Guide

## Overview

The Toni Cat Gallery now supports **batch uploading** multiple photos at once and **editing tags** for already uploaded photos! These features make managing your cat photo collection much easier.

---

## ✨ New Features

### 1. 📸 Batch Photo Upload

Upload multiple photos at once instead of one at a time!

**Benefits:**
- ⚡ Upload 5, 10, or even 20+ photos in one go
- 🏷️ Tag each photo individually with custom moods
- 👁️ Preview all photos before uploading
- ❌ Remove photos from the batch if needed
- 🔍 Automatic duplicate detection for each photo

### 2. ✏️ Edit Photo Tags

Change the mood tags on photos that are already uploaded!

**Benefits:**
- 🔄 Update moods without re-uploading
- 🎯 Fix tagging mistakes
- 📝 Add moods you forgot initially
- 🗑️ Remove incorrect mood tags

---

## 🚀 How to Use Batch Upload

### Step 1: Select Multiple Photos

You can select multiple photos in two ways:

**Option A: Click to Browse**
1. Click the **"📸 Upload New Photo"** area
2. In the file picker, select multiple photos:
   - **Windows**: Hold `Ctrl` and click each photo
   - **Mac**: Hold `Cmd` and click each photo
   - Or select a range: Click first photo, hold `Shift`, click last photo
3. Click **Open**

**Option B: Drag & Drop**
1. Open your file explorer
2. Select multiple photos
3. Drag and drop them onto the upload area

### Step 2: Preview Your Photos

After selecting photos, you'll see a grid preview showing:
- ✅ All photos that passed validation (file type, size, not duplicates)
- ⚠️ Alert messages for any skipped photos (wrong format, too large, duplicates)
- 🏷️ Current mood tags (initially "No moods selected")

**What Gets Validated:**
- ✅ File type: Only JPG, JPEG, PNG
- ✅ File size: Must be under 10MB
- ✅ Duplicates: Automatically detected and skipped

### Step 3: Tag Each Photo

For each photo in the batch:

1. Click the **"🏷️ Tag"** button under the photo
2. A modal will appear showing:
   - Preview of the photo
   - All available mood tags
3. Click mood tags to select/deselect:
   - 😤 **Unbridled Rage**
   - 😴 **Lazy Boy**
   - 😇 **Sweet Perfect Angel Cat**
   - 🤪 **Weirdo**
4. Click **"💾 Save"** to apply the tags

**Pro Tips:**
- You can select multiple moods per photo!
- Photos without mood tags will still show "No moods selected"
- You can skip tagging and add tags later using the Edit feature

### Step 4: Remove Photos (Optional)

Don't want to upload a photo after all?

1. Click the **✕** button in the top-right corner of any photo preview
2. The photo will be removed from the batch
3. The upload count will update automatically

### Step 5: Upload All Photos

When you're ready:

1. Click the **"⬆️ Upload All (X photos)"** button at the bottom
2. You'll see progress: **"⏳ Uploading 1/5..."**, **"⏳ Uploading 2/5..."**, etc.
3. Each photo uploads to Cloudinary with its selected mood tags
4. After completion, you'll see a summary:
   ```
   ✅ Upload complete!
   
   5 photos uploaded successfully
   ```

**What Happens Behind the Scenes:**
- Each photo uploads to Cloudinary
- Photo URLs and mood tags are saved to Firestore (if connected)
- Photo hashes are saved to prevent future duplicates
- Photos are added to the gallery immediately

---

## ✏️ How to Edit Photo Tags

You can edit tags for any photo that's already uploaded and in your favorites:

### Step 1: Go to Favorites

1. Scroll down to the **"⭐ Your Favorites"** section
2. You'll see all photos you've rated

### Step 2: Click Edit Tags

1. Find the photo you want to edit
2. Click the **"✏️ Edit"** button on the photo card

### Step 3: Update Moods

A modal will appear showing:
- Preview of the photo
- Current mood tags (highlighted in purple)
- All available mood tags

**To Edit:**
1. Click tags to **add** them (they'll turn purple)
2. Click selected tags to **remove** them
3. You can select any combination of moods

### Step 4: Save Changes

1. Click **"💾 Save Changes"**
2. Tags are updated in:
   - Local memory
   - Firestore database (if connected)
3. You'll see: **"✅ Tags updated successfully!"**
4. The favorites section refreshes to show updated tags

**Use Cases for Editing:**
- 🐱 "This photo is actually more 'Weirdo' than 'Lazy Boy'"
- 📝 "I forgot to add 'Sweet Perfect Angel Cat' tag"
- 🎯 "Let me organize photos better by mood"
- 🧹 "Clean up my tagging to be more consistent"

---

## 💡 Pro Tips & Best Practices

### For Batch Uploading

1. **Organize First**
   - Sort photos into folders by mood before uploading
   - Makes batch tagging faster and easier

2. **Start Small**
   - Try uploading 5-10 photos first
   - Get comfortable with the workflow
   - Then do larger batches

3. **Preview Before Upload**
   - Double-check each photo's tags
   - Remove any accidental selections
   - Ensure quality is good

4. **Tag Consistently**
   - Use the same tagging logic for similar photos
   - Makes mood filtering more effective later

### For Tag Editing

1. **Regular Reviews**
   - Periodically review your favorites
   - Update tags as you get better at categorizing

2. **Fix Mistakes Immediately**
   - If you notice a wrong tag, fix it right away
   - Keeps your collection organized

3. **Seasonal Cleanup**
   - Every few months, review all photos
   - Update tags to match your current system

---

## 🔧 Technical Details

### Batch Upload Workflow

```
User selects files
    ↓
Validate each file (type, size, duplicates)
    ↓
Create preview grid
    ↓
User tags each photo
    ↓
Click "Upload All"
    ↓
Upload photos one-by-one
    ↓
Save metadata to Firestore
    ↓
Add to local catPhotos array
    ↓
Show success message
```

### Tag Editing Workflow

```
User clicks "Edit" on favorite
    ↓
Load current photo tags
    ↓
Display modal with mood options
    ↓
User selects/deselects moods
    ↓
Click "Save Changes"
    ↓
Update local catPhotos array
    ↓
Update Firestore document
    ↓
Refresh favorites display
```

### Data Stored for Each Photo

```javascript
{
  url: "https://res.cloudinary.com/...",
  moods: ["lazy_boy", "weirdo"],
  uploadedAt: "2026-02-10T...",
  hash: "abc123...", // SHA-256 hash for duplicate detection
  updatedAt: "2026-02-10T..." // Only if tags were edited
}
```

---

## 🐛 Troubleshooting

### Batch Upload Issues

**Problem: "No valid files to upload" alert**
- **Cause**: All selected files failed validation
- **Fix**: 
  - Check file formats (must be JPG, JPEG, or PNG)
  - Check file sizes (must be under 10MB each)
  - Check for duplicates (photos already uploaded)

**Problem: Some photos were skipped**
- **Cause**: Individual files failed validation
- **Fix**: Read the alert messages - they tell you exactly why each photo was skipped

**Problem: Upload fails partway through**
- **Cause**: Network connection issue or Cloudinary error
- **Fix**: 
  - Check your internet connection
  - The error message will show how many succeeded vs. failed
  - Re-upload only the failed photos

**Problem: Photos uploaded but not showing in gallery**
- **Cause**: Page needs refresh or localStorage issue
- **Fix**: Refresh the page - photos are saved in Cloudinary and Firestore

### Tag Editing Issues

**Problem: "Photo not found" alert**
- **Cause**: Photo isn't in the loaded catPhotos array
- **Fix**: 
  - Refresh the page to reload all photos
  - Make sure the photo was uploaded successfully

**Problem: Changes not saving**
- **Cause**: Firestore connection issue
- **Fix**: 
  - Check browser console for errors
  - Changes are saved locally even if Firestore fails
  - Re-edit the photo to try saving to Firestore again

**Problem: Changes don't appear immediately**
- **Cause**: Display needs refresh
- **Fix**: The favorites section should auto-refresh, but you can scroll to another section and back

---

## 🎉 Examples

### Example 1: Uploading a Day's Worth of Photos

```
1. Open phone/camera folder
2. Select all 15 photos from today
3. Drag onto upload area
4. Tag breakfast photos as "Lazy Boy"
5. Tag playful photos as "Weirdo"
6. Tag sweet moment photos as "Sweet Perfect Angel Cat"
7. Tag the one where she knocked over your coffee as "Unbridled Rage"
8. Click "Upload All (15 photos)"
9. Wait 2-3 minutes for upload
10. Success! All photos in gallery
```

### Example 2: Re-organizing Old Photos

```
1. Go to Favorites section
2. Find photo tagged "Lazy Boy"
3. Click "✏️ Edit"
4. Add "Sweet Perfect Angel Cat" (she's both!)
5. Click "💾 Save Changes"
6. Repeat for other photos that need multiple tags
7. Now your mood filters work better!
```

### Example 3: Bulk Upload with Consistent Tagging

```
Scenario: You have 30 photos to upload, all from a lazy Sunday

1. Select all 30 photos
2. Batch preview appears
3. For each photo: Click "🏷️ Tag" → Select "😴 Lazy Boy" → Save
4. Takes 2 minutes to tag all 30
5. Click "Upload All (30 photos)"
6. Go make coffee while they upload
7. Come back to 30 new lazy cat photos!
```

---

## 🔮 Future Enhancements (Potential)

Ideas for making this even better:

- 🏷️ **Bulk tagging**: Apply the same tags to all selected photos at once
- 📁 **Tag presets**: Save common tag combinations ("Lazy Sunday" = Lazy Boy + Sweet Angel)
- 🔍 **Search by tag**: Find photos by specific tag combinations
- 📊 **Tag statistics**: See which moods are most common
- 🎨 **Custom tags**: Create your own mood tags beyond the 4 defaults

---

## 🤝 Support

If you have questions or issues:

1. Check this guide first
2. Check `README.md` for general setup
3. Check `CLOUDINARY_SETUP.md` for upload issues
4. Check browser console for error messages
5. Try refreshing the page

---

## 🎁 For Your Girlfriend

This feature makes it super easy for both of you to add photos!

**For you:**
- Dump a whole camera roll at once
- Tag photos quickly
- Keep the gallery fresh with new content

**For her:**
- Upload multiple photos from her phone
- Edit tags if she changes her mind
- Organize the collection her way

**Perfect for:**
- 📸 After a photoshoot
- 🌅 End of the day
- 🎉 Special occasions
- 🐱 When Toni does something particularly cute (which is always)

Enjoy your batch uploading! 🐱📷✨
