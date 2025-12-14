# Quick Setup Guide for Railway Deployment

## 🚀 Fastest Way to Deploy (GitHub Actions)

### Step 1: Fork & Clone
```bash
# Fork the repository on GitHub first, then:
git clone https://github.com/YOUR_USERNAME/device-activity-tracker.git
cd device-activity-tracker
```

### Step 2: Create Railway Project
1. Go to [railway.app](https://railway.app)
2. Sign up/login with GitHub
3. Click "New Project" → "Empty Project"
4. Name it: `device-activity-tracker`

### Step 3: Get Railway Token
```bash
# Install Railway CLI
npm i -g @railway/cli

# Login (opens browser)
railway login

# Get your token
railway whoami --token
```
**Copy the token!** You'll need it in the next step.

### Step 4: Add Token to GitHub
1. Go to your GitHub repo: `https://github.com/YOUR_USERNAME/device-activity-tracker`
2. Click **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**
4. Name: `RAILWAY_TOKEN`
5. Value: Paste the token from Step 3
6. Click **Add secret**

### Step 5: Link Your Local Repo to Railway
```bash
# In your local repo directory
railway link
```
Select the project you created in Step 2.

### Step 6: Deploy!
```bash
git push origin main
# or
git push origin your-branch-name
```

**That's it!** 🎉 GitHub Actions will automatically:
- Build your app
- Deploy to Railway
- Give you a live URL

### Step 7: Add Persistent Storage (IMPORTANT!)
1. Go to Railway dashboard → Your project
2. Click your service
3. Click **"Volumes"** tab
4. Click **"New Volume"**
5. Mount path: `/app/auth_info_baileys`
6. Size: `1GB`
7. Click **"Add"**

This ensures WhatsApp stays connected across deployments!

### Step 8: Get Your App URL
1. In Railway dashboard → Your service
2. Click **"Settings"**
3. Scroll to **"Domains"**
4. Click **"Generate Domain"**
5. Copy the URL: `https://your-app.railway.app`

### Step 9: Use Your App
1. Visit your Railway URL
2. Scan WhatsApp QR code
3. Add phone numbers to track
4. See real-time activity! 📊

---

## 📝 Updating Your App

Just push to GitHub:
```bash
git add .
git commit -m "Update feature"
git push
```
GitHub Actions deploys automatically! ✨

---

## 🔍 Troubleshooting

**GitHub Actions failing?**
- Check if `RAILWAY_TOKEN` secret is set correctly
- Make sure you ran `railway link` in your local repo

**App crashes after deployment?**
- Check Railway logs in dashboard
- Make sure volume is mounted at `/app/auth_info_baileys`

**WhatsApp disconnects?**
- Add persistent volume (Step 7)
- Volume must persist across deployments

---

## 💡 Pro Tips

- **View logs:** Railway dashboard → Your service → "Deployments" tab
- **Environment variables:** Railway dashboard → "Variables" tab
- **Manual deployment:** GitHub → "Actions" → "Deploy to Railway" → "Run workflow"
- **Local testing:** Run `npm run dev` before pushing

---

## 🆘 Need Help?

- Railway Discord: [discord.gg/railway](https://discord.gg/railway)
- GitHub Issues: [Create an issue](https://github.com/TheTechNetwork/device-activity-tracker/issues)
- Railway Docs: [docs.railway.app](https://docs.railway.app)
