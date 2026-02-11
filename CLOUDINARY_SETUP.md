# 🌥️ Cloudinary Setup Guide

## Quick Start (5 minutes)

Follow these steps to enable photo uploads with Cloudinary's free tier.

---

## Step 1: Create Cloudinary Account

1. Go to [https://cloudinary.com/users/register/free](https://cloudinary.com/users/register/free)
2. Sign up with:
   - Email
   - Or Google/GitHub account
3. **No credit card required!**
4. Verify your email

---

## Step 2: Get Your Credentials

After logging in, you'll see your dashboard:

1. Look for the **"Product Environment Credentials"** section
2. You'll see three important values:
   - **Cloud Name** (e.g., `dxyz123abc`)
   - **API Key** (we don't need this)
   - **API Secret** (we don't need this)

3. **Copy your Cloud Name** - you'll need it in Step 4

---

## Step 3: Create Upload Preset

This allows unsigned uploads (no API keys in your code):

1. In Cloudinary dashboard, go to **Settings** (gear icon top right)
2. Click **Upload** tab in the left sidebar
3. Scroll down to **Upload presets**
4. Click **Add upload preset**
5. Configure:
   ```
   Preset name: toni_gallery_upload
   Signing mode: Unsigned ✅ (IMPORTANT!)
   Folder: toni-gallery
   Access control: Public
   ```
6. Click **Save**
7. **Copy the preset name** (`toni_gallery_upload`)

---

## Step 4: Update Your Code

Open `index.html` and find this section (around line 665):

```javascript
// Cloudinary Configuration
// REPLACE WITH YOUR CLOUDINARY CREDENTIALS
const cloudinaryConfig = {
    cloudName: 'YOUR_CLOUD_NAME',
    uploadPreset: 'YOUR_UPLOAD_PRESET'
};
```

Replace with YOUR values:

```javascript
const cloudinaryConfig = {
    cloudName: 'dxyz123abc',  // Your Cloud Name from Step 2
    uploadPreset: 'toni_gallery_upload'  // Your preset name from Step 3
};
```

**Save the file!**

---

## Step 5: Test It!

1. Open your site (locally or on GitHub Pages)
2. Scroll to "📸 Upload New Photo"
3. Click or drag a photo
4. Select mood tags
5. Click "✅ Upload Photo"
6. Wait for progress...
7. ✅ Success! Photo should appear!

---

## Verify Upload in Cloudinary

1. Go to Cloudinary dashboard
2. Click **Media Library** in left sidebar
3. You should see your uploaded photo in the `toni-gallery` folder!

---

## 🎯 What Gets Uploaded:

### To Cloudinary:
- Original photo file
- Stored in `toni-gallery` folder
- Public URL generated
- Permanently stored (free tier: 25GB)

### To Firestore (if enabled):
- Photo URL
- Cloudinary ID
- Mood tags
- Uploader username
- Upload timestamp

### To localStorage (backup):
- Photo URL
- Mood tags
- Upload date

This triple storage ensures photos are never lost!

---

## 🆓 Free Tier Limits

**You get for FREE:**
- ✅ 25 GB storage
- ✅ 25 GB bandwidth/month
- ✅ 25,000 transformations/month
- ✅ Unlimited uploads
- ✅ No credit card required
- ✅ Never expires

**Your usage estimate:**
- 50-200 photos = 150-600 MB storage (2% of limit)
- 500 views/month = 1-2 GB bandwidth (8% of limit)

**You'll never hit the limits!** ✅

---

## 🔧 Advanced Configuration (Optional)

### Restrict File Types

In Upload Preset settings:
```
Allowed formats: jpg, png, jpeg
```

### Set Max File Size

In Upload Preset:
```
Max file size: 10 MB
```

### Auto-Optimize Images

In Upload Preset:
```
Quality: Auto
Format: Auto
```

This will automatically compress photos and save bandwidth!

---

## 🔐 Security Notes

**Unsigned uploads are safe because:**
- ✅ Limited to your preset settings
- ✅ Can only upload to designated folder
- ✅ No access to your account settings
- ✅ No ability to delete files
- ✅ Rate-limited automatically

**Best practices:**
- Keep upload preset unsigned (easier, secure enough)
- Only share the site URL (never your Cloudinary credentials)
- Monitor uploads in Cloudinary dashboard

---

## 📱 How Users Experience It

### On Desktop:
1. Click "Upload New Photo"
2. Select file from computer
3. Preview appears
4. Select moods
5. Upload → See progress bar
6. Success! Photo live instantly

### On Mobile:
1. Click "Upload New Photo"
2. Opens camera or photo library
3. Select/take photo
4. Preview appears
5. Select moods
6. Upload → Success!

Works perfectly on phones! 📱

---

## 🐛 Troubleshooting

### "Cloudinary is not configured yet"
- ❌ You forgot to update `cloudinaryConfig` in code
- ✅ Replace `YOUR_CLOUD_NAME` and `YOUR_UPLOAD_PRESET`

### "Upload failed: 400"
- ❌ Upload preset is set to "Signed" instead of "Unsigned"
- ✅ Go to Cloudinary → Settings → Upload presets → Change to Unsigned

### "Upload failed: Network error"
- ❌ Internet connection issue
- ✅ Check connection and try again

### Photos upload but don't appear:
- ✅ Refresh the page
- ✅ Check Cloudinary Media Library to confirm upload
- ✅ Check browser console for errors (F12)

### "Upload failed: Invalid preset"
- ❌ Preset name doesn't match
- ✅ Copy exact preset name from Cloudinary dashboard

---

## 🎨 Photo Management

### View All Uploads:
1. Go to Cloudinary dashboard
2. Click **Media Library**
3. Navigate to `toni-gallery` folder
4. See all uploaded photos!

### Delete Photos:
1. In Media Library, click photo
2. Click trash icon
3. Photo removed from Cloudinary (but URL might still be in Firestore)

### Download Originals:
1. Click photo in Media Library
2. Click download icon
3. Get original file

---

## 💡 Pro Tips

### Organize Photos:
Use folders in upload preset:
```
Folder: toni-gallery/2024
Folder: toni-gallery/favorites
```

### Auto-Transform:
Cloudinary can auto-resize, compress, and optimize:
```
Transformation: c_limit,w_1920,q_auto,f_auto
```

### Add Watermark:
In upload preset, add overlay:
```
Overlay: watermark
```

---

## 📊 Monitor Usage

Check your usage anytime:

1. Go to Cloudinary dashboard
2. Look at top bar:
   - Storage used
   - Bandwidth used
   - Transformations used

All shown as percentages of free tier!

---

## 🚀 You're Done!

Upload feature is now fully functional with:
- ✅ Free cloud storage (25GB)
- ✅ Fast uploads
- ✅ Works on all devices
- ✅ Photos persist forever
- ✅ No maintenance needed

Start uploading Toni photos! 📸🐱💕

---

## Need Help?

- Cloudinary Docs: [https://cloudinary.com/documentation](https://cloudinary.com/documentation)
- Support: [https://support.cloudinary.com](https://support.cloudinary.com)
- Status: [https://status.cloudinary.com](https://status.cloudinary.com)
