# Toni's Photo Gallery 🐱💕

An interactive website that displays random cat photos with fun features like rating, mood selection, slideshow mode, username system, and cloud sync!

## ✨ Features

- 👤 **Username System** - Simple username + secret code protection
- ☁️ **Cloud Sync** - Ratings sync across all devices (optional Firebase setup)
- 📦 **Batch Upload** - Upload multiple photos at once! (NEW!)
- ✏️ **Edit Tags** - Change mood tags on already uploaded photos! (NEW!)
- 🎲 **Random Photos** - Get a new cat photo with each refresh or button click
- 💕 **Photo Rating** - Rate each photo with 1-5 hearts (saves per username!)
- ⭐ **Favorites Gallery** - View and download all your rated photos
- 🎭 **Mood Selection** - Filter photos by custom moods
- 📸 **Photo Upload** - Upload new photos with mood tagging
- 📊 **Visit Counter** - Tracks how many times each user has visited
- 🔊 **Sound Effects** - Cute sound when changing photos (toggle on/off)
- 🐱 **Purr Feature** - Hidden easter egg - pet the photo and hear purring!
- 🎨 **Mosaic Background** - Beautiful subtle mosaic of cat photos in the background
- 🎬 **Slideshow Mode** - Auto-play photos with live countdown
- 💾 **Download Button** - Save your favorite photos instantly
- ⌨️ **Keyboard Shortcuts** - Spacebar for next photo, 1-5 for ratings, Arrow Down to download
- 🔒 **Duplicate Detection** - Automatically prevents uploading the same photo twice

## 🚀 Quick Start

### Option 1: View Locally (Immediate - Works Offline)
1. Add your cat photos to the `cats` folder
2. Open `index.html` in your web browser
3. Enter a username when prompted
4. Enjoy! (Ratings save locally per-browser)

### Option 2: Host on GitHub Pages + Firebase (Ratings Sync Everywhere!)
1. **Set up GitHub Pages** (free hosting):
   - Create a GitHub account
   - Create a new repository called `toni-gallery`
   - Upload `index.html` and `cats` folder
   - Go to Settings → Pages → Enable Pages

2. **Set up Firebase** (optional - for cross-device sync):
   - Follow the step-by-step guide in `FIREBASE_SETUP.md`
   - Takes about 5 minutes
   - Completely free for this usage level
   - Once set up, ratings sync across all devices!

Your site will be live at: `https://yourusername.github.io/toni-gallery/`

## 📸 Adding More Photos

### Easy Method: Use the Built-In Uploader! (RECOMMENDED)

The easiest way to add photos is through the website itself:

1. **Open the website** and log in with your username
2. **Scroll to "📸 Upload New Photo"** section
3. **Select photos**:
   - Click to browse and select multiple photos (hold Ctrl/Cmd)
   - Or drag & drop multiple photos onto the upload area
4. **Tag each photo** with moods (click the 🏷️ Tag button):
   - 😤 Unbridled Rage
   - 😴 Lazy Boy
   - 😇 Sweet Perfect Angel Cat
   - 🤪 Weirdo
5. **Click "⬆️ Upload All"** and wait for completion
6. Done! Photos are live immediately

**📦 Batch Upload Features:**
- Upload 5, 10, 20+ photos at once
- Preview all photos before uploading
- Tag each individually with custom moods
- Remove any photo from batch before uploading
- Automatic duplicate detection
- Progress tracking

**See `BATCH_UPLOAD_GUIDE.md` for detailed instructions!**

### Advanced Method: Manual Code Updates

If you want to manually add photos (not using Cloudinary upload):

1. Add photos to the `cats` folder
2. Update the `catPhotos` array in `index.html`:

```javascript
const catPhotos = [
    { url: 'cats/cat1.jpg', moods: ['lazy_boy'] },
    { url: 'cats/cat2.jpg', moods: ['weirdo'] },
    // Or use Cloudinary URLs:
    { url: 'https://res.cloudinary.com/...', moods: ['sweet_perfect_angel_cat'] },
];
```

### Custom Mood Tags

- `'unbridled_rage'` - Angry, frustrated, annoyed cat moments
- `'lazy_boy'` - Calm, relaxed, sleeping, lounging
- `'sweet_perfect_angel_cat'` - Cute, sweet, adorable moments
- `'weirdo'` - Funny, bizarre, quirky behaviors

You can assign multiple moods to each photo!

## 🎮 How to Use Features

### 🔐 Secret Code Access
- First time: Enter username AND secret code: `toni_balogna`
- Only people with the code can access the site
- Protects your photos from random visitors

### 📦 Batch Upload (NEW!)
- Upload multiple photos at once (5, 10, 20+)
- Tag each photo individually with moods
- Remove photos from batch before uploading
- Auto-duplicate detection
- **See `BATCH_UPLOAD_GUIDE.md` for complete guide!**

### ✏️ Edit Tags (NEW!)
- Change mood tags on already uploaded photos
- Go to Favorites → Click "✏️ Edit" on any photo
- Select/deselect moods and save
- Updates everywhere (Firestore + local)
- **See `BATCH_UPLOAD_GUIDE.md` for details!**

### 💕 Photo Rating & Favorites
- Click the hearts below the photo to rate it (1-5 hearts)
- Click the ✖ button next to hearts to clear rating
- Ratings are saved per username
- With Firebase: Ratings sync across all devices
- Scroll to "⭐ Your Favorites" to see all rated photos
- Filter favorites by rating (All, 5⭐, 4⭐, etc.)
- Download or view any favorite

### 🎭 Mood Selection
- Click mood buttons at the top to filter photos:
  - 😤 **Unbridled Rage**
  - 😴 **Lazy Boy**
  - 😇 **Sweet Perfect Angel Cat**
  - 🤪 **Weirdo**
- "All Moods" shows everything
- Other buttons show only photos with that mood tag

### 🐱 Purr Feature (Hidden Easter Egg!)
- **Desktop**: Move mouse around photo (like petting)
- **Mobile**: Touch and move finger on photo
- Keep "petting" for a few seconds and Toni will purr!
- Sound plays softly and stops when you stop petting
- 10 second auto-stop if you hold still

### 🎨 Mosaic Background
- Subtle background shows a beautiful mosaic of cat photos
- Automatically uses photos from your collection
- Adds depth and visual interest without being distracting

### 🎬 Slideshow Mode
- Toggle the "Slideshow" switch to auto-advance every 5 seconds
- Live countdown shows time until next photo
- Perfect for showing off Toni to friends!

### 💾 Download Photos
- Click "💾 Download" to save the current photo
- Great for setting as wallpaper or sharing!

### ⌨️ Keyboard Shortcuts
- **Spacebar** or **→** (Right Arrow): Next photo
- **1-5**: Rate current photo with that many hearts
- **↓** (Down Arrow): Download current photo

## 🎨 Customization

### Change the Title
Edit line 6 in `index.html`:
```html
<title>Toni's Photo Gallery 💕</title>
```

### Change the Heading
Edit line 245 in `index.html`:
```html
<h1>🐱 Toni's Photo Gallery 🐱</h1>
```

### Change Colors
The gradient colors are on line 16. You can use a gradient generator like [cssgradient.io](https://cssgradient.io/) to create new ones.

### Add Real Meow Sound
1. Get or record a meow sound file (meow.mp3)
2. Put it in the same folder as index.html
3. Replace the audio initialization code (around line 335) with:
```javascript
function playMeow() {
    const audio = new Audio('meow.mp3');
    audio.volume = 0.3;
    audio.play().catch(e => console.log('Sound play failed:', e));
}
```

## 📁 Folder Structure
```
toni-gallery/
├── index.html          # Main website file with all features
├── README.md           # This file (instructions)
└── cats/               # Folder for cat photos
    ├── cat1.jpg
    ├── cat2.jpg
    ├── cat3.jpg
    └── ...
```

## 🆓 Cost Breakdown
- **Hosting**: FREE (GitHub Pages)
- **Domain**: FREE (uses github.io subdomain)
- **Storage**: FREE (GitHub gives you plenty of space)
- **All Features**: FREE (no external dependencies!)
- **Custom Domain** (optional): ~$10-15/year if you want something like `toni.love`

## 💾 Data Storage

### Without Firebase (Default):
- **Username**: Saved in browser localStorage
- **Ratings**: Saved per-browser (won't sync across devices)
- **Visit Counter**: Per-browser
- ✅ Completely private
- ✅ Works offline
- ⚠️ Ratings don't sync between devices

### With Firebase (Optional):
- **Username**: Saved in browser localStorage
- **Ratings**: Synced to cloud (works everywhere!)
- **Visit Counter**: Still per-browser
- ✅ Ratings sync across all devices
- ✅ Access ratings from phone, tablet, computer
- ✅ Still works offline (syncs when back online)
- ✅ Free forever for this usage level

**Setup Firebase**: See `FIREBASE_SETUP.md` for a 5-minute guide!

## 🔐 Security Note

The username system is simple and doesn't use passwords. Anyone who knows the username can access those ratings. This is perfect for a personal gift! 

If you want password protection later, let me know and I can add it.

## 🤝 Tips
- Keep photo file sizes reasonable (under 2MB each) for fast loading
- Use common formats: JPG, PNG, or WEBP
- Tag photos with moods that match their vibe
- Photos can have multiple mood tags!
- Works on all devices (mobile, tablet, desktop)
- Ratings persist forever (until browser data is cleared)

## 🐛 Troubleshooting
- **Photos don't show**: Check that file names in the code match exactly (including capitalization)
- **Sound doesn't work**: Some browsers block autoplay. User interaction (button click) enables it.
- **Ratings not saving**: Make sure your browser allows localStorage
- **Firebase not working**: Check console for errors. See `FIREBASE_SETUP.md`
- **Ratings not syncing**: Make sure you're using the same username on all devices
- **Visit counter keeps resetting**: Don't clear browser data / use the same browser
- **Username modal won't close**: Enter a valid username (2+ characters, letters/numbers only)

## 🎁 Special Touch Ideas
- Record a real meow sound and add it!
- Take photos specifically for each mood category
- Write the date/location in the filename (e.g., `cats/2024-06-15-beach.jpg`)
- Set up Firebase so her ratings sync between phone and computer!
- Share a special username together (e.g., "Tyler&Sarah")
- Add a secret photo that only shows up on special dates (requires custom code)

## 📚 Files Included

- `index.html` - Main website with all features
- `README.md` - This file (general instructions)
- `FIREBASE_SETUP.md` - Step-by-step Firebase setup guide
- `cats/` - Folder for your cat photos

Enjoy your interactive cat gallery! 🎉💕
