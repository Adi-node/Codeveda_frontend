# Vercel Deployment Guide

This guide will help you deploy your frontend to Vercel.

## Prerequisites

1. **Vercel Account**: Sign up at [vercel.com](https://vercel.com)
2. **Backend Deployed**: Your backend API must be deployed and accessible
3. **Supabase Project**: Your Supabase project should be configured

## Environment Variables Setup

Before deploying, you need to set up environment variables in Vercel:

### 1. In Vercel Dashboard:
- Go to your project settings
- Navigate to "Environment Variables"
- Add the following variables:

```bash
VITE_SUPABASE_URL=https://your-project-id.supabase.co
VITE_SUPABASE_ANON_KEY=your-actual-supabase-anon-key
VITE_API_URL=https://your-deployed-backend.com/api
```

### 2. Important Notes:
- Replace `https://your-deployed-backend.com/api` with your actual backend URL
- Get Supabase credentials from your Supabase project dashboard
- All environment variables for Vite must start with `VITE_`

## Deployment Methods

### Method 1: GitHub Integration (Recommended)
1. Push your code to GitHub
2. Connect your Vercel account to GitHub
3. Import your repository in Vercel
4. Vercel will automatically detect it as a Vite project
5. Set environment variables in Vercel dashboard
6. Deploy!

### Method 2: Vercel CLI
```bash
# Install Vercel CLI
npm install -g vercel

# Login to Vercel
vercel login

# Deploy
vercel

# Set environment variables
vercel env add VITE_SUPABASE_URL
vercel env add VITE_SUPABASE_ANON_KEY
vercel env add VITE_API_URL

# Redeploy to apply environment variables
vercel --prod
```

## Build Settings (Auto-detected)

Vercel will automatically detect these settings from `vercel.json`:
- **Framework**: Vite
- **Build Command**: `npm run build`
- **Output Directory**: `dist`
- **Install Command**: `npm install`

## Post-Deployment Checklist

### 1. Test Your Deployment
- [ ] Visit your deployed URL
- [ ] Test user authentication (login/signup)
- [ ] Verify API calls are working
- [ ] Check browser console for errors

### 2. Configure Your Backend
- [ ] Update CORS settings to allow your Vercel domain
- [ ] Ensure your backend accepts requests from `https://your-app.vercel.app`

### 3. Custom Domain (Optional)
- [ ] Add custom domain in Vercel dashboard
- [ ] Update DNS records as instructed
- [ ] Update CORS settings for custom domain

## Common Issues & Solutions

### Issue: API calls failing
**Solution**: Check that `VITE_API_URL` is set correctly and your backend allows CORS from your Vercel domain.

### Issue: Authentication not working
**Solution**: Verify Supabase environment variables are set correctly in Vercel dashboard.

### Issue: 404 on page refresh
**Solution**: The `vercel.json` rewrites configuration should handle this. Make sure it's in your repository.

### Issue: Environment variables not working
**Solution**: 
- Ensure they start with `VITE_`
- Redeploy after adding environment variables
- Check they're set in Vercel dashboard

## Performance Optimization

Your `vite.config.js` includes:
- Code splitting for better loading
- Asset optimization
- Chunk size optimization

## Security Headers

Your deployment includes security headers:
- `X-Content-Type-Options: nosniff`
- `X-Frame-Options: DENY`
- `X-XSS-Protection: 1; mode=block`
- `Referrer-Policy: strict-origin-when-cross-origin`

## Monitoring

- Monitor your deployment in Vercel dashboard
- Check function logs for any errors
- Set up analytics if needed

## Need Help?

1. Check Vercel documentation: [vercel.com/docs](https://vercel.com/docs)
2. Check build logs in Vercel dashboard
3. Test locally first with `npm run build && npm run preview`