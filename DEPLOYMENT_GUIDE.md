# Calyra.ai Deployment Guide

This guide covers all deployment options for the Calyra.ai platform, from development to production.

## 🚀 Quick Deployment Options

### 1. Vercel (Recommended - Easiest)
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
npm run deploy
```

### 2. Netlify (Simple)
```bash
# Build the project
npm run build

# Deploy dist folder to Netlify
```

### 3. StackBlitz (No Installation Required)
- Visit [stackblitz.com](https://stackblitz.com)
- Import the GitHub repository
- Configure environment variables
- Deploy directly from browser

## 📋 Prerequisites

### Required Accounts
1. **Supabase** - [supabase.com](https://supabase.com)
2. **OpenAI** - [openai.com](https://openai.com)
3. **Paystack** - [paystack.com](https://paystack.com)
4. **Vercel/Netlify** - For deployment

### Required API Keys
- Supabase URL and Anon Key
- OpenAI API Key
- Paystack Secret and Public Keys
- Crunchbase API Key (optional)
- News API Key (optional)

## 🛠️ Step-by-Step Setup

### Step 1: Supabase Setup

1. **Create Supabase Project**
   ```bash
   # Go to supabase.com and create a new project
   ```

2. **Run Database Schema**
   ```sql
   -- Copy and paste the contents of supabase/schema.sql
   -- into your Supabase SQL editor
   ```

3. **Configure Authentication**
   - Go to Authentication > Settings
   - Add your domain to allowed redirect URLs
   - Configure email templates

4. **Get API Keys**
   - Go to Settings > API
   - Copy Project URL and anon public key

### Step 2: OpenAI Setup

1. **Create OpenAI Account**
   ```bash
   # Visit openai.com and create account
   ```

2. **Get API Key**
   - Go to API Keys section
   - Create new secret key
   - Copy the key

3. **Add Credits**
   - Add billing information
   - Purchase credits for API usage

### Step 3: Paystack Setup

1. **Create Paystack Account**
   ```bash
   # Visit paystack.com and create account
   ```

2. **Get API Keys**
   - Go to Settings > API Keys
   - Copy Secret Key and Public Key

3. **Configure Webhooks**
   - Add webhook URL: `https://your-domain.com/api/webhooks/paystack`
   - Select events: `charge.success`, `subscription.create`, `subscription.disable`

### Step 4: Environment Configuration

1. **Create Environment File**
   ```bash
   cp env.example .env
   ```

2. **Fill in Configuration**
   ```env
   # Supabase Configuration
   VITE_SUPABASE_URL=https://your-project.supabase.co
   VITE_SUPABASE_ANON_KEY=your-anon-key
   VITE_SUPABASE_SERVICE_ROLE_KEY=your-service-role-key

   # AI Services
   VITE_OPENAI_API_KEY=sk-your-openai-key
   VITE_ANTHROPIC_API_KEY=sk-ant-your-anthropic-key

   # Payment Gateway
   VITE_PAYSTACK_SECRET_KEY=sk_test_your-paystack-secret
   VITE_PAYSTACK_PUBLIC_KEY=pk_test_your-paystack-public

   # Market Intelligence APIs
   VITE_CRUNCHBASE_API_KEY=your-crunchbase-key
   VITE_NEWS_API_KEY=your-news-api-key

   # Development
   VITE_APP_ENV=production
   VITE_DEBUG_MODE=false
   ```

## 🚀 Deployment Methods

### Method 1: Vercel (Recommended)

#### Automatic Deployment
```bash
# Install Vercel CLI
npm i -g vercel

# Login to Vercel
vercel login

# Deploy
vercel --prod
```

#### Manual Deployment
1. **Push to GitHub**
   ```bash
   git add .
   git commit -m "Ready for deployment"
   git push origin main
   ```

2. **Connect to Vercel**
   - Go to [vercel.com](https://vercel.com)
   - Import your GitHub repository
   - Configure environment variables
   - Deploy

3. **Environment Variables in Vercel**
   - Go to Project Settings > Environment Variables
   - Add all variables from your `.env` file

### Method 2: Netlify

#### Automatic Deployment
```bash
# Install Netlify CLI
npm install -g netlify-cli

# Login to Netlify
netlify login

# Deploy
netlify deploy --prod
```

#### Manual Deployment
1. **Build the Project**
   ```bash
   npm run build
   ```

2. **Deploy to Netlify**
   - Go to [netlify.com](https://netlify.com)
   - Drag and drop the `dist` folder
   - Configure environment variables

3. **Environment Variables in Netlify**
   - Go to Site Settings > Environment Variables
   - Add all variables from your `.env` file

### Method 3: StackBlitz (No Installation)

1. **Open StackBlitz**
   - Visit [stackblitz.com](https://stackblitz.com)
   - Click "Start a new project"

2. **Import Repository**
   - Click "Import from GitHub"
   - Enter your repository URL
   - Wait for import to complete

3. **Configure Environment**
   - Open `.env` file
   - Add your API keys

4. **Deploy**
   - Click "Deploy" button
   - Choose deployment platform
   - Configure environment variables

### Method 4: Docker

#### Build Docker Image
```bash
# Create Dockerfile
cat > Dockerfile << EOF
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .
RUN npm run build

EXPOSE 3000

CMD ["npm", "start"]
EOF

# Build image
docker build -t calyra-ai .

# Run container
docker run -p 3000:3000 --env-file .env calyra-ai
```

#### Docker Compose
```yaml
# docker-compose.yml
version: '3.8'
services:
  calyra-ai:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
    env_file:
      - .env
```

### Method 5: Traditional Hosting

#### Build for Production
```bash
# Install dependencies
npm install

# Build the project
npm run build

# The dist folder contains your production build
```

#### Upload to Server
1. **Upload Files**
   - Upload contents of `dist` folder to your web server
   - Ensure `.htaccess` (Apache) or `nginx.conf` (Nginx) is configured

2. **Configure Server**
   ```nginx
   # nginx.conf example
   server {
       listen 80;
       server_name your-domain.com;
       root /var/www/calyra-ai;
       index index.html;

       location / {
           try_files $uri $uri/ /index.html;
       }
   }
   ```

## 🔧 Configuration

### Production Environment Variables

```env
# Required
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key
VITE_OPENAI_API_KEY=sk-your-openai-key
VITE_PAYSTACK_SECRET_KEY=sk_live_your-paystack-secret
VITE_PAYSTACK_PUBLIC_KEY=pk_live_your-paystack-public

# Optional but Recommended
VITE_CRUNCHBASE_API_KEY=your-crunchbase-key
VITE_NEWS_API_KEY=your-news-api-key
VITE_ANTHROPIC_API_KEY=sk-ant-your-anthropic-key
VITE_GOOGLE_ANALYTICS_ID=your-ga-id
VITE_MIXPANEL_TOKEN=your-mixpanel-token

# Development
VITE_APP_ENV=production
VITE_DEBUG_MODE=false
VITE_API_BASE_URL=https://your-domain.com
```

### Database Configuration

1. **Supabase RLS Policies**
   - Ensure all tables have proper RLS policies
   - Test user permissions

2. **Backup Strategy**
   - Enable automatic backups in Supabase
   - Set up manual backup schedule

3. **Performance Optimization**
   - Add database indexes
   - Monitor query performance

### Security Configuration

1. **CORS Settings**
   ```javascript
   // In your Supabase project
   // Go to Settings > API > CORS
   // Add your domain to allowed origins
   ```

2. **Rate Limiting**
   - Configure API rate limits
   - Set up monitoring

3. **SSL/TLS**
   - Ensure HTTPS is enabled
   - Configure SSL certificates

## 📊 Monitoring & Analytics

### Google Analytics Setup
```javascript
// Add to your main.tsx or App.tsx
import ReactGA from 'react-ga4';

ReactGA.initialize('GA_MEASUREMENT_ID');
```

### Error Tracking
```javascript
// Add error boundary and logging
window.addEventListener('error', (event) => {
  console.error('Global error:', event.error);
  // Send to your error tracking service
});
```

### Performance Monitoring
```javascript
// Monitor Core Web Vitals
import { getCLS, getFID, getFCP, getLCP, getTTFB } from 'web-vitals';

getCLS(console.log);
getFID(console.log);
getFCP(console.log);
getLCP(console.log);
getTTFB(console.log);
```

## 🔍 Troubleshooting

### Common Issues

#### 1. Build Errors
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install
npm run build
```

#### 2. Environment Variables Not Working
```bash
# Check variable names start with VITE_
# Ensure no spaces around =
# Restart development server
```

#### 3. Supabase Connection Issues
```bash
# Verify URL and key
# Check CORS settings
# Test connection in Supabase dashboard
```

#### 4. Payment Processing Issues
```bash
# Verify Paystack keys
# Check webhook configuration
# Test in sandbox mode first
```

#### 5. AI Service Errors
```bash
# Verify OpenAI API key
# Check API quota
# Test API calls manually
```

### Debug Mode

```env
# Enable debug mode
VITE_DEBUG_MODE=true
VITE_APP_ENV=development
```

### Logging

```javascript
// Add comprehensive logging
console.log('Environment:', import.meta.env.VITE_APP_ENV);
console.log('Supabase URL:', import.meta.env.VITE_SUPABASE_URL);
console.log('OpenAI Key:', import.meta.env.VITE_OPENAI_API_KEY ? 'Set' : 'Not Set');
```

## 🚀 Performance Optimization

### Build Optimization
```javascript
// vite.config.ts
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
          ai: ['openai', 'anthropic'],
          ui: ['lucide-react', 'framer-motion']
        }
      }
    }
  }
});
```

### Code Splitting
```javascript
// Lazy load components
const Dashboard = lazy(() => import('./pages/Dashboard'));
const AdvancedTools = lazy(() => import('./pages/AdvancedTools'));
```

### Image Optimization
```javascript
// Use optimized images
import { Image } from '@vitejs/plugin-react';

// Configure image optimization
export default defineConfig({
  plugins: [
    Image({
      include: ['**/*.{png,jpg,jpeg,gif,svg,webp}']
    })
  ]
});
```

## 🔒 Security Checklist

- [ ] Environment variables are secure
- [ ] API keys are not exposed in client code
- [ ] CORS is properly configured
- [ ] HTTPS is enabled
- [ ] Database RLS policies are active
- [ ] Payment processing is PCI compliant
- [ ] Error messages don't expose sensitive data
- [ ] Rate limiting is implemented
- [ ] Input validation is in place
- [ ] XSS protection is enabled

## 📈 Scaling Considerations

### Database Scaling
- Monitor Supabase usage
- Consider dedicated database for enterprise
- Implement caching strategies

### API Scaling
- Monitor OpenAI API usage
- Implement request queuing
- Consider API key rotation

### Infrastructure Scaling
- Use CDN for static assets
- Implement caching layers
- Monitor performance metrics

## 🆘 Support

### Getting Help
- **Documentation:** [docs.calyra.ai](https://docs.calyra.ai)
- **Community:** [community.calyra.ai](https://community.calyra.ai)
- **Email:** support@calyra.ai
- **Status:** [status.calyra.ai](https://status.calyra.ai)

### Emergency Contacts
- **Technical Issues:** tech@calyra.ai
- **Billing Issues:** billing@calyra.ai
- **Security Issues:** security@calyra.ai

---

**Happy Deploying! 🚀**
