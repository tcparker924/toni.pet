# Toni's Photo Gallery 🐱💕

An interactive website that displays random cat photos with fun features like rating, mood selection, slideshow mode, username system, and cloud sync!

## ✨ Features

- 👤 **Username System** - Simple username login (no password needed!)
- ☁️ **Cloud Sync** - Ratings sync across all devices (optional Firebase setup)
- 🎲 **Random Photos** - Get a new cat photo with each refresh or button click
- 💕 **Photo Rating** - Rate each photo with 1-5 hearts (saves per username!)
- 🎭 **Mood Selection** - Filter photos by mood: Happy, Silly, Sleepy, or Majestic
- 📊 **Visit Counter** - Tracks how many times each user has visited
- 🔊 **Sound Effects** - Cute sound when changing photos (toggle on/off)
- 🐱 **Purr Feature** - Pet the photo with your mouse and Toni will purr!
- 🎨 **Mosaic Background** - Beautiful subtle mosaic of cat photos in the background
- 🎬 **Slideshow Mode** - Auto-play photos every 5 seconds
- 💾 **Download Button** - Save your favorite photos instantly
- ⌨️ **Keyboard Shortcuts** - Spacebar for next photo, 1-5 for ratings, Arrow Down to download

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

### Update the Photo Array
When adding photos, you need to update the `catPhotos` array in `index.html` (around line 273):

```javascript
const catPhotos = [
    { path: 'cats/cat1.jpg', moods: ['happy'] },
    { path: 'cats/cat2.jpg', moods: ['silly'] },
    { path: 'cats/cat3.jpg', moods: ['sleepy'] },
    { path: 'cats/cat4.jpg', moods: ['majestic'] },
    { path: 'cats/cat5.jpg', moods: ['happy', 'silly'] },
    { path: 'cats/cat6.jpg', moods: ['sleepy', 'majestic'] }, // New photo!
    // Add more here
];
```

### Mood Tags
Assign one or more moods to each photo:
- `'happy'` - Energetic, playful, cheerful photos
- `'silly'` - Funny, goofy, entertaining photos
- `'sleepy'` - Calm, relaxed, resting photos
- `'majestic'` - Elegant, regal, proud photos

### Method 2: Let Others Add Photos
If you're using GitHub:
1. Others can fork your repository
2. They add photos to the `cats` folder
3. They update the `catPhotos` array with mood tags
4. They create a Pull Request
5. You review and merge it

## 🎮 How to Use Features

### Username System
- First time: Enter any username (no password!)
- Choose something memorable (e.g., "Sarah" or "Sarah&Tyler")
- That's it! Your ratings are now saved to that username
- Use the same username on any device to sync ratings (requires Firebase)
- Click "Change User" to switch users

### Photo Rating
- Click the hearts below the photo to rate it (1-5 hearts)
- Ratings are saved per username
- With Firebase: Ratings sync across all devices
- Without Firebase: Ratings save per-browser only

### Mood Selection
- Click mood buttons at the top to filter photos
- "All Moods" shows everything
- Other buttons show only photos with that mood tag

### Purr Feature (NEW! 🐱)
- **Desktop**: Hover over the photo and move your mouse around (like petting)
- **Mobile**: Press and hold the photo for 2 seconds
- Keep "petting" for ~1.5 seconds and Toni will purr!
- A cute indicator shows your progress
- The purr sound is generated with realistic low-frequency rumbling

### Mosaic Background (NEW! 🎨)
- Subtle background shows a beautiful mosaic of cat photos
- Automatically uses the first 5 photos in your collection
- Adds depth and visual interest without being distracting
- Looks professional and polished!

### Slideshow Mode
- Toggle the "Slideshow" switch to auto-advance every 5 seconds
- Perfect for showing off Toni to friends!

### Sound Effects
- Toggle the "Sound" switch to enable/disable the cute beep
- **Pro tip**: You can add a real meow sound by:
  1. Get a `meow.mp3` file
  2. Put it in the same folder as `index.html`
  3. Update the audio element in the HTML (instructions in code comments)

### Download Photos
- Click "💾 Download" to save the current photo
- Great for setting as wallpaper or sharing!

### Keyboard Shortcuts
- **Spacebar** or **→** (Right Arrow): Next photo
- **1-5**: Rate current photo with that many hearts
- **↓** (Down Arrow): Download current photo

### Easter Eggs
- Try petting the photo - Toni might purr! 🐱💕

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
