# 🚀 Vercel Deployment Guide for Calyra.ai

## Prerequisites
- GitHub account
- Vercel account (free at vercel.com)

## Method 1: Deploy via Vercel Dashboard (Recommended)

### Step 1: Prepare Your Project
1. **Create a GitHub Repository**
   - Go to [GitHub.com](https://github.com)
   - Click "New repository"
   - Name it `calyra-ai`
   - Make it public or private (your choice)
   - Don't initialize with README (we already have one)

### Step 2: Upload to GitHub
1. **Download the project files**
   - The `calyra-ai-final` folder contains all necessary files
   - You can zip it and upload via GitHub web interface

2. **Upload via GitHub Web Interface**
   - Go to your new repository
   - Click "uploading an existing file"
   - Drag and drop all files from `calyra-ai-final` folder
   - Commit the changes

### Step 3: Deploy to Vercel
1. **Connect to Vercel**
   - Go to [vercel.com](https://vercel.com)
   - Sign up/login with your GitHub account
   - Click "New Project"

2. **Import Repository**
   - Select your `calyra-ai` repository
   - Vercel will automatically detect it's a Vite project

3. **Configure Environment Variables**
   - In the deployment settings, add these environment variables:
   ```
   VITE_SUPABASE_URL=your_supabase_url
   VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
   VITE_OPENAI_API_KEY=your_openai_api_key
   VITE_ANTHROPIC_API_KEY=your_anthropic_api_key
   VITE_PAYSTACK_PUBLIC_KEY=your_paystack_public_key
   VITE_PAYSTACK_SECRET_KEY=your_paystack_secret_key
   VITE_APP_ENV=production
   ```

4. **Deploy**
   - Click "Deploy"
   - Vercel will build and deploy your app automatically

## Method 2: Deploy via Vercel CLI (Alternative)

If you prefer command line:

```bash
# Install Vercel CLI globally
npm install -g vercel

# Navigate to project directory
cd calyra-ai-final

# Deploy
vercel --prod
```

## Post-Deployment Configuration

### 1. Set Up Supabase
1. Go to [supabase.com](https://supabase.com)
2. Create a new project
3. Run the SQL schema from `supabase/schema.sql`
4. Get your project URL and anon key
5. Add them to Vercel environment variables

### 2. Configure APIs
1. **OpenAI**: Get API key from [platform.openai.com](https://platform.openai.com)
2. **Anthropic**: Get API key from [console.anthropic.com](https://console.anthropic.com)
3. **Paystack**: Get keys from [paystack.com](https://paystack.com)

### 3. Update Environment Variables in Vercel
1. Go to your Vercel project dashboard
2. Navigate to Settings > Environment Variables
3. Add all required variables from `env.example`

## Custom Domain Setup

1. **Add Custom Domain**
   - In Vercel dashboard, go to Settings > Domains
   - Add your domain (e.g., calyra.ai)
   - Follow DNS configuration instructions

2. **SSL Certificate**
   - Vercel automatically provides SSL certificates
   - No additional configuration needed

## Monitoring & Analytics

### 1. Vercel Analytics
- Automatically enabled
- View in Vercel dashboard

### 2. Custom Analytics
- Google Analytics 4
- Mixpanel
- Segment
- All configured in the app

## Troubleshooting

### Common Issues:

1. **Build Failures**
   - Check environment variables are set correctly
   - Verify all dependencies are in package.json

2. **API Errors**
   - Ensure API keys are valid
   - Check CORS settings in Supabase

3. **Routing Issues**
   - Vercel.json handles SPA routing
   - All routes redirect to index.html

### Performance Optimization:
- Vercel automatically optimizes builds
- CDN distribution worldwide
- Automatic caching configured

## Security Checklist

✅ Environment variables secured
✅ CORS configured in Supabase
✅ Security headers set in vercel.json
✅ HTTPS enforced
✅ XSS protection enabled

## Support

If you encounter issues:
1. Check Vercel deployment logs
2. Verify environment variables
3. Test locally first (if possible)
4. Contact Vercel support

## Next Steps After Deployment

1. **Test All Features**
   - User registration/login
   - Idea generation
   - AI analysis
   - Payment processing

2. **Monitor Performance**
   - Check Vercel analytics
   - Monitor API usage
   - Track user engagement

3. **Scale as Needed**
   - Vercel automatically scales
   - Upgrade plan if needed

---

🎉 **Your Calyra.ai platform is now live and ready for users!**

