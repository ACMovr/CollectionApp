# Collection Manager - Deployment Guide

## Quick Start (GitHub Pages - 10 Minutes)

This is the **easiest and recommended** way to deploy your Collection Manager.

### Prerequisites
- GitHub account (free at github.com)
- The files in this folder

### Step-by-Step Deployment

#### 1. Create GitHub Repository

1. Go to github.com and sign in
2. Click the "+" icon → "New repository"
3. Repository name: `collection-manager`
4. Public or Private: **Public** (required for free GitHub Pages)
5. **Do NOT** initialize with README
6. Click "Create repository"

#### 2. Upload Files

**Option A: Drag and Drop (Easiest)**

1. On the repository page, click "uploading an existing file"
2. Drag these files from this folder:
   ```
   index.html
   manifest.json
   sw.js
   ```
3. Click "Commit changes"

**Option B: Git Command Line**

```bash
# Navigate to this folder
cd /path/to/collection-manager

# Initialize git
git init

# Add files
git add .

# Commit
git commit -m "Initial deployment"

# Set remote (replace [username] with your GitHub username)
git remote add origin https://github.com/[username]/collection-manager.git

# Push
git branch -M main
git push -u origin main
```

#### 3. Create Icons Folder

1. In your repository, click "Add file" → "Create new file"
2. Type: `icons/.gitkeep`
3. Click "Commit new file"
4. Upload your icon files to this folder (see Icon Creation below)

#### 4. Enable GitHub Pages

1. Go to your repository Settings (⚙️ icon)
2. In the left sidebar, click "Pages"
3. Under "Source":
   - Branch: `main`
   - Folder: `/ (root)`
4. Click "Save"
5. Wait 1-2 minutes for deployment

#### 5. Get Your URL

Your app will be available at:
```
https://[username].github.io/collection-manager/
```

Example: `https://lars-dev.github.io/collection-manager/`

#### 6. Install on Android

1. Open the URL in Chrome on your Android phone
2. Chrome will show an "Install app" banner
3. Tap "Install"
4. The app appears on your home screen!
5. Open it - works like a native app!

---

## Icon Creation

You need to create app icons for the PWA to be installable.

### Quick Method: Use an Online Generator

1. Go to: https://favicon.io/favicon-generator/
2. Settings:
   - Text: Use emoji 📱 or initials "CM"
   - Background: #FF6B35 (orange)
   - Font: Bold
3. Click "Download"
4. Extract the ZIP file
5. You'll get multiple sizes

### Manual Method: Create One Icon

Create a single 512x512 PNG icon, then use a resizer:
1. Go to: https://www.iloveimg.com/resize-image
2. Upload your 512x512 icon
3. Create these sizes:
   - 72x72 → icon-72x72.png
   - 96x96 → icon-96x96.png
   - 128x128 → icon-128x128.png
   - 144x144 → icon-144x144.png
   - 152x152 → icon-152x152.png
   - 192x192 → icon-192x192.png
   - 384x384 → icon-384x384.png
   - 512x512 → icon-512x512.png

### Upload Icons

1. Go to your repository's `icons` folder
2. Click "Add file" → "Upload files"
3. Upload all the icon files
4. Commit changes

---

## Files Explained

### index.html
The main app - the complete UI and functionality.

### manifest.json
PWA configuration file that tells browsers:
- App name and description
- Theme colors
- Icons for home screen
- How to display the app (standalone/fullscreen)

### sw.js
Service Worker - enables:
- Offline functionality
- Fast loading (caching)
- App-like behavior

---

## Testing Your Deployment

### Test on Desktop
1. Open your GitHub Pages URL in Chrome
2. You should see the Collection Manager
3. Try clicking apps, importing
4. Press F12 → Application tab → Service Worker
5. Should show "activated and running"

### Test on Android
1. Open URL in Chrome
2. Look for install prompt
3. Install the app
4. Check home screen for icon
5. Open app - should be fullscreen
6. Turn off WiFi - should still work!

---

## Updating Your App

### To Update the App

**Method 1: GitHub Website**
1. Go to the file you want to edit
2. Click the pencil icon (✏️)
3. Make changes
4. Scroll down, click "Commit changes"
5. Changes go live in 1-2 minutes

**Method 2: Git Command Line**
```bash
# Make your changes to files

# Commit and push
git add .
git commit -m "Updated feature X"
git push

# Changes go live in 1-2 minutes
```

### Auto-Updates on User Devices

When users open your app, the service worker will:
1. Check for updates
2. Download new version in background
3. Show update prompt (optional)
4. Apply updates on next app launch

---

## Custom Domain (Optional)

Want your app at `apps.yourdomain.com` instead of GitHub's URL?

### Steps:

1. **Buy a Domain** (if you don't have one)
   - Namecheap.com: ~$12/year
   - Google Domains: ~$12/year

2. **Configure DNS**
   Add a CNAME record:
   ```
   Type: CNAME
   Host: apps (or whatever subdomain)
   Value: [username].github.io
   ```

3. **Configure GitHub Pages**
   - Settings → Pages
   - Custom domain: `apps.yourdomain.com`
   - Check "Enforce HTTPS"
   - Save

4. **Wait 24 Hours**
   DNS changes take time to propagate

---

## Troubleshooting

### GitHub Pages Not Loading?

**Problem**: 404 error on GitHub Pages URL

**Solutions**:
- Wait 5 minutes (initial deployment takes time)
- Check Settings → Pages for error messages
- Ensure repository is Public
- Verify `index.html` is in root (not in subfolder)
- Check file names are exactly: `index.html` (lowercase)

### PWA Not Installing?

**Problem**: No install prompt on Android

**Solutions**:
- Clear Chrome cache: Settings → Site settings → Clear data
- Ensure all required files are present:
  - ✓ index.html
  - ✓ manifest.json
  - ✓ sw.js
  - ✓ At least one icon (192x192 minimum)
- Check browser console (F12) for errors
- Use Chrome (not Firefox initially)
- Ensure site is HTTPS (GitHub Pages is automatic)

### Service Worker Not Activating?

**Problem**: App doesn't work offline

**Solutions**:
- Open DevTools (F12)
- Go to Application → Service Workers
- Click "Update" or "Unregister"
- Reload page
- Check console for errors

### Icons Not Showing?

**Problem**: Default icon instead of custom icon

**Solutions**:
- Verify icon files are in `/icons/` folder
- Check file names match manifest.json
- Ensure icons are PNG format
- Minimum size: 192x192 pixels
- Hard refresh: Ctrl+Shift+R (desktop) or clear cache (mobile)

---

## Advanced: Alternative Hosting

### Vercel Deployment

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel --prod

# Follow prompts
# Result: https://collection-manager.vercel.app
```

### Netlify Deployment

1. Go to netlify.com
2. Drag and drop this folder
3. Get instant URL
4. Optional: Connect GitHub for auto-deploy

---

## Project Structure

```
collection-manager/
│
├── index.html              # Main app
├── manifest.json           # PWA manifest
├── sw.js                   # Service worker
│
├── icons/                  # App icons
│   ├── icon-72x72.png
│   ├── icon-96x96.png
│   ├── icon-128x128.png
│   ├── icon-144x144.png
│   ├── icon-152x152.png
│   ├── icon-192x192.png
│   ├── icon-384x384.png
│   └── icon-512x512.png
│
└── README.md              # This file
```

---

## Security Notes

### HTTPS Required
- GitHub Pages provides free HTTPS ✓
- PWAs require HTTPS for security
- Service workers won't work over HTTP

### Data Privacy
- All data stays on user's device
- No server-side storage
- IndexedDB is local only
- Apps run in sandboxed iframes

### Content Security
- Apps are sandboxed
- Cannot access parent app data
- Cannot access other apps
- Limited to their own storage

---

## Next Steps

After deployment:

1. **Test Thoroughly**
   - Install on your Android device
   - Try all features
   - Test offline mode

2. **Add IndexedDB**
   - Currently apps are demo only
   - Add real storage implementation
   - Enable actual app import/launch

3. **Enhance Features**
   - Search functionality
   - Collections/folders
   - Export/backup
   - Analytics

4. **Optional: Play Store**
   - Package as TWA
   - Submit to Google Play
   - Get wider distribution

---

## Support & Resources

### Documentation
- PWA Guide: https://web.dev/progressive-web-apps/
- GitHub Pages: https://docs.github.com/pages
- Service Workers: https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API

### Tools
- PWA Builder: https://www.pwabuilder.com/
- Icon Generator: https://favicon.io/
- Manifest Generator: https://app-manifest.firebaseapp.com/

### Testing
- Lighthouse: Chrome DevTools → Lighthouse tab
- PWA Test: https://www.pwabuilder.com/
- Mobile Test: Chrome DevTools → Toggle device toolbar

---

## Cost Summary

### GitHub Pages (This Setup)
```
Setup:           $0
Hosting:         $0/month
SSL/HTTPS:       $0 (included)
Custom Domain:   $12/year (optional)

TOTAL: Free forever (or $12/year with custom domain)
```

### No Hidden Costs
- No storage limits for code
- Unlimited bandwidth
- Unlimited visitors
- No credit card required

---

## Quick Reference Commands

```bash
# Clone your deployed app
git clone https://github.com/[username]/collection-manager.git

# Make changes
# ... edit files ...

# Deploy updates
git add .
git commit -m "Your update message"
git push

# Changes live in 1-2 minutes!
```

---

## Success Checklist

After deployment, verify:

- [ ] App loads at GitHub Pages URL
- [ ] Icons appear correctly
- [ ] Install prompt appears on Android Chrome
- [ ] App installs to home screen
- [ ] Opens fullscreen (no browser UI)
- [ ] Service worker activates (check DevTools)
- [ ] Works offline after first load
- [ ] All demo apps launch
- [ ] Import modal opens

If all checked ✓ → **Deployment successful!** 🎉

---

**Ready to deploy? Start at Step 1 above!**

Need help? The deployment guide in `deployment-options-guide.md` has more detailed alternatives.
