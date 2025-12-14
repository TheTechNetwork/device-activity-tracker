# Railway Deployment Guide

This guide explains how to deploy the Device Activity Tracker to Railway.

## Prerequisites

- Railway account (sign up at [railway.app](https://railway.app))
- Git repository pushed to GitHub
- Railway CLI (optional but recommended): `npm i -g @railway/cli`

## Deployment Steps

### Option 1: Deploy via Railway Dashboard (Recommended)

1. **Create a new project on Railway**
   - Go to [railway.app](https://railway.app)
   - Click "New Project"
   - Select "Deploy from GitHub repo"
   - Choose your repository: `TheTechNetwork/device-activity-tracker`
   - Select the branch: `claude/deploy-cloudflare-workers-Wkmno`

2. **Railway will automatically detect and deploy**
   - Railway uses the `railway.toml` and `nixpacks.toml` configurations
   - Build process runs automatically
   - Your app will be deployed!

3. **Add a domain (optional)**
   - In your Railway project, go to Settings
   - Click "Generate Domain" to get a free `.railway.app` domain
   - Or add your custom domain

4. **Enable persistent storage (important!)**
   - In Railway dashboard, go to your service
   - Click "Volumes" tab
   - Add a new volume
   - Mount path: `/app/auth_info_baileys`
   - This ensures WhatsApp authentication persists across deployments

### Option 2: Deploy via Railway CLI

```bash
# Install Railway CLI
npm i -g @railway/cli

# Login to Railway
railway login

# Initialize project
railway init

# Deploy
railway up

# Add domain
railway domain
```

## Configuration

### Environment Variables

Railway automatically sets the `PORT` variable. You can add additional variables:

1. Go to your Railway project
2. Click on "Variables"
3. Add the following (optional):
   - `NODE_ENV`: `production` (auto-set by Railway)
   - `SIGNAL_API_URL`: If you're running Signal API in a separate service

### Signal Integration (Optional)

If you want Signal tracking:

1. Add a new service in Railway
2. Use the Docker image: `bbernhard/signal-cli-rest-api`
3. Add environment variable: `MODE=json-rpc`
4. Add a volume mounted to `/home/.local/share/signal-cli`
5. Update the main service's `SIGNAL_API_URL` to point to the Signal service

## Post-Deployment

1. **Access your app**: Open the generated Railway URL
2. **Scan WhatsApp QR code**: Use the web interface to link WhatsApp
3. **Start tracking**: Add phone numbers to track

## Important Notes

- **Persistent Storage**: Make sure to add a volume for `auth_info_baileys/` to persist WhatsApp sessions
- **Restarts**: Railway will automatically restart your app if it crashes
- **Logs**: View logs in the Railway dashboard under the "Deployments" tab
- **Signal**: Signal integration requires Docker and is optional

## Troubleshooting

### App crashes on startup
- Check logs in Railway dashboard
- Ensure all dependencies are installed
- Verify the build completed successfully

### WhatsApp disconnects after restart
- Ensure you've added a volume for `/app/auth_info_baileys`
- Volume must persist across deployments

### Cannot access the app
- Check if the deployment succeeded
- Verify the domain is configured correctly
- Check if the PORT variable is set correctly

## Costs

- Railway offers a free tier with limited resources
- For production use, consider upgrading to a paid plan
- Persistent volumes may incur additional costs

## Support

For issues:
- Railway Discord: [discord.gg/railway](https://discord.gg/railway)
- Railway Docs: [docs.railway.app](https://docs.railway.app)
- Project issues: [GitHub Issues](https://github.com/TheTechNetwork/device-activity-tracker/issues)
