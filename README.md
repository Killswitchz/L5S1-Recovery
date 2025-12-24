# L5-S1 Recovery Program

A 12-week rehabilitation app for L5-S1 disc bulge with sciatica. Features exercise timers with audio notifications, progress tracking, and illustrated exercises.

## Features

- 📅 12-week progressive program (4 phases)
- ⏱️ Timers with audio countdown alerts (10, 5, 4, 3, 2, 1 sec)
- 🔊 Completion chimes - no need to watch the screen
- 📊 Progress tracking (saves to browser storage)
- 🎨 Illustrated exercises with instructions
- 📱 Mobile-friendly, installable as PWA

---

## Deployment Options

### Option 1: Azure Static Web Apps (Recommended - Free Tier Available)

**Using Azure Portal:**

1. Go to [Azure Portal](https://portal.azure.com)
2. Create a new **Static Web App**
3. Choose your subscription and resource group
4. Name: `l5s1-recovery`
5. Plan type: **Free**
6. Region: Choose closest to you
7. Deployment source: **Other** (we'll upload manually)
8. Click **Review + Create** → **Create**

**Upload files using Azure CLI:**

```bash
# Install Azure CLI if needed
# https://docs.microsoft.com/en-us/cli/azure/install-azure-cli

# Login
az login

# Deploy (replace with your resource group and app name)
az staticwebapp upload \
  --app-name l5s1-recovery \
  --resource-group your-resource-group \
  --source ./
```

**Or use VS Code Azure Extension:**
1. Install "Azure Static Web Apps" extension
2. Right-click the folder → Deploy to Static Web App

---

### Option 2: Azure Blob Storage (Static Website)

```bash
# Create storage account
az storage account create \
  --name l5s1recovery \
  --resource-group your-resource-group \
  --location westeurope \
  --sku Standard_LRS

# Enable static website
az storage blob service-properties update \
  --account-name l5s1recovery \
  --static-website \
  --index-document index.html

# Upload files
az storage blob upload-batch \
  --account-name l5s1recovery \
  --source ./ \
  --destination '$web'

# Get URL
az storage account show \
  --name l5s1recovery \
  --query "primaryEndpoints.web" \
  --output tsv
```

---

### Option 3: GitHub Pages (Free)

1. Create a GitHub repository
2. Upload `index.html` and `manifest.json`
3. Go to Settings → Pages
4. Source: Deploy from branch → `main` → `/ (root)`
5. Your site will be at: `https://yourusername.github.io/repo-name`

---

### Option 4: Netlify (Free, Easiest)

1. Go to [netlify.com](https://netlify.com)
2. Drag and drop the folder containing `index.html`
3. Done! You get a URL like `random-name.netlify.app`
4. Optionally set a custom domain

---

### Option 5: Vercel (Free)

1. Go to [vercel.com](https://vercel.com)
2. Import from Git or drag & drop
3. Auto-deploys on every push

---

## Installing on Your Phone

Once deployed, you can install it as a native app:

**iPhone:**
1. Open the URL in Safari
2. Tap Share button → "Add to Home Screen"

**Android:**
1. Open the URL in Chrome
2. Tap menu → "Add to Home Screen" or "Install App"

---

## Local Development

Just open `index.html` in a browser. No build step required!

For testing with a local server:
```bash
# Python 3
python -m http.server 8080

# Node.js
npx serve .
```

---

## Customization

Edit `index.html` to:
- Adjust exercise durations in `exerciseData`
- Modify weekly programs in `weeklyPrograms`
- Change colors in the style section
- Add new exercises

---

## Tech Stack

- React 18 (via CDN)
- Web Audio API for sounds
- LocalStorage for progress persistence
- No build tools required

---

## License

Free for personal use. Created for L5-S1 disc bulge rehabilitation.
