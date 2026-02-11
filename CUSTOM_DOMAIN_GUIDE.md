# 🌐 Custom Domain Setup for GitHub Pages

## Quick Answer:

**YES!** You can use your own domain (like `toni.love` or `mycatsite.com`) with GitHub Pages. It's free and takes about 10-15 minutes to set up.

---

## 📋 Prerequisites:

- ✅ GitHub Pages site already set up
- ✅ Custom domain purchased (from Namecheap, Google Domains, GoDaddy, etc.)
- ✅ Access to your domain registrar's DNS settings

---

## 🚀 Setup Steps:

### Step 1: Add Domain to GitHub Pages

1. Go to your GitHub repository
2. Click **Settings** → **Pages**
3. Under **"Custom domain"**, enter your domain:
   - `toni.love` (apex domain)
   - OR `www.toni.love` (subdomain)
   - OR `gallery.yourdomain.com` (subdomain)
4. Click **"Save"**
5. Check **"Enforce HTTPS"** (wait 24 hours if not available yet)

---

### Step 2: Configure DNS at Your Registrar

You have two options: **Apex Domain** or **Subdomain**

---

## Option A: Apex Domain (toni.love)

**Use this if:** You want `toni.love` (no www)

### DNS Records to Add:

Add **4 A records** pointing to GitHub's IPs:

```
Type: A
Name: @ (or leave blank)
Value: 185.199.108.153

Type: A
Name: @ (or leave blank)
Value: 185.199.109.153

Type: A
Name: @ (or leave blank)
Value: 185.199.110.153

Type: A
Name: @ (or leave blank)
Value: 185.199.111.153
```

Add **1 CNAME record** for www:

```
Type: CNAME
Name: www
Value: YOUR_USERNAME.github.io
```

---

## Option B: Subdomain (www.toni.love or gallery.toni.love)

**Use this if:** You want `www.toni.love` or `gallery.toni.love`

### DNS Record to Add:

Add **1 CNAME record**:

```
Type: CNAME
Name: www (or gallery, or photos, or whatever you want)
Value: YOUR_USERNAME.github.io
```

**That's it!** Much simpler than apex domain.

---

## 🎯 Example: Namecheap

1. Log in to Namecheap
2. Go to **Dashboard** → **Domain List**
3. Click **"Manage"** next to your domain
4. Click **"Advanced DNS"** tab
5. Click **"Add New Record"**
6. Add the A or CNAME records (see above)
7. Click **"Save All Changes"**

---

## 🎯 Example: Google Domains

1. Log in to Google Domains
2. Click your domain
3. Click **"DNS"** in left sidebar
4. Scroll to **"Custom records"**
5. Click **"Manage custom records"**
6. Add the A or CNAME records (see above)
7. Click **"Save"**

---

## 🎯 Example: GoDaddy

1. Log in to GoDaddy
2. Go to **My Products** → **Domain**
3. Click **"DNS"** next to your domain
4. Click **"Add"** under Records
5. Add the A or CNAME records (see above)
6. Click **"Save"**

---

## ⏱️ How Long Does It Take?

### DNS Propagation:
- **Minimum:** 15 minutes
- **Typical:** 1-6 hours
- **Maximum:** 24-48 hours (rare)

**Check if it's working:**
```bash
# In terminal:
nslookup toni.love

# Should show GitHub's IPs:
# 185.199.108.153
# 185.199.109.153
# etc.
```

Or use online tools:
- [whatsmydns.net](https://www.whatsmydns.net)
- [dnschecker.org](https://dnschecker.org)

---

## 🔒 HTTPS (SSL Certificate)

### Automatic HTTPS:
1. After DNS propagates (24 hours max)
2. Go back to GitHub Pages settings
3. Check **"Enforce HTTPS"**
4. GitHub provides free SSL certificate
5. Your site is now: `https://toni.love` ✅

**Why this matters:**
- Secure connection
- No browser warnings
- Required for modern web
- Completely free!

---

## 🎯 Which Domain Structure to Choose?

### For Your Project (Recommendations):

**Option 1: Short & Sweet (Best for Gift)**
```
toni.love
→ Super memorable
→ Easy to type
→ Personal and cute
```

**Option 2: Subdomain (If You Have Other Uses for Domain)**
```
gallery.yourdomain.com
photos.yourdomain.com
toni.yourdomain.com
→ Good if main domain is for something else
```

**Option 3: www Subdomain (Traditional)**
```
www.toni.love
→ Classic approach
→ Slightly easier DNS setup
```

---

## 📝 Summary Table:

| Domain Type | Example | DNS Records | Setup Time |
|-------------|---------|-------------|------------|
| Apex | `toni.love` | 4 A + 1 CNAME | 10 min |
| Subdomain | `gallery.toni.love` | 1 CNAME | 5 min |
| WWW | `www.toni.love` | 1 CNAME | 5 min |

**All work perfectly with GitHub Pages!**

---

## 🔄 Testing Your Setup:

### Before DNS Propagates:
```
https://YOUR_USERNAME.github.io/toni-gallery/
→ ✅ Works immediately
```

### After DNS Propagates:
```
https://toni.love
→ ✅ Works (redirects to your site)

https://YOUR_USERNAME.github.io/toni-gallery/
→ ✅ Still works (redirects to custom domain)
```

---

## 💡 Pro Tips:

### 1. Keep GitHub URL Working:
Both URLs work:
- `https://toni.love` (custom domain)
- `https://username.github.io/toni-gallery/` (GitHub URL)

Both go to the same site!

### 2. Redirect www to Non-www (or vice versa):
Add both in DNS, GitHub handles redirect automatically.

### 3. Email Forwarding:
Some registrars let you do:
- `hello@toni.love` forwards to your email
- Free with domain purchase

### 4. Subdomain Ideas:
If you bought `toni.love`, you could do:
- `toni.love` - Main gallery
- `admin.toni.love` - Admin panel (future)
- `upload.toni.love` - Upload-only page (future)

---

## 🎁 Cool Domain Ideas:

If you haven't bought a domain yet:

**Cute & Personal:**
- `toni.love` ❤️
- `ourtoni.com`
- `tonithecat.com`
- `meettoni.com`

**Fun & Playful:**
- `tonigallery.com`
- `tonisphotos.com`
- `tonipics.com`
- `randomtoni.com`

**Inside Joke:**
- `tonibalogna.com` (based on your secret code!)
- `lordtoni.com`
- `toniverse.com`

---

## 📊 Cost Breakdown:

### With Custom Domain:
- Domain: **~$12-15/year** (one-time annual)
- GitHub Pages: **$0**
- Cloudinary: **$0** (free tier)
- Firebase: **$0** (free tier)
- SSL Certificate: **$0** (GitHub provides)

**Total: ~$12-15/year** (just the domain!)

### Without Custom Domain:
- Everything: **$0**
- URL: `username.github.io/toni-gallery`
- Still fully functional!

---

## 🤔 Should You Use Custom Domain?

### YES, if:
✅ You want it to feel more "professional"
✅ You want an easy-to-remember URL
✅ It's a special gift (makes it feel more permanent)
✅ You're okay spending $12/year

### NO, if:
❌ You want to keep it 100% free
❌ GitHub URL is fine for you
❌ Only she will use it (URL doesn't matter)

**For a gift:** Custom domain adds a nice touch! `toni.love` would be adorable 💕

---

## 🚀 Quick Start:

### If You Already Have a Domain:

```bash
# 1. Add domain in GitHub Pages settings
#    Settings → Pages → Custom domain: yourdomain.com

# 2. Add DNS records at your registrar
#    (see Option A or B above)

# 3. Wait 1-24 hours

# 4. Check if working:
#    Visit yourdomain.com

# 5. Enable HTTPS in GitHub Pages settings

# Done!
```

---

## 🎯 Recommendation:

If you bought a domain like `toni.love`:

1. **Use apex domain** (`toni.love` without www)
2. **Add the 4 A records** (10 minutes)
3. **Wait 2-6 hours** for DNS
4. **Enable HTTPS** after 24 hours
5. **Share:** `https://toni.love` 💕

Super clean and memorable!

---

Need help setting up DNS records? Let me know which domain registrar you're using (Namecheap, Google Domains, GoDaddy, etc.) and I can give you specific instructions! 🎯
