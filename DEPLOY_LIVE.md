# 🚀 Rupix3D Live Deployment - 10 Minutes to Production

## YOUR DEPLOYMENT LINKS (AFTER FOLLOWING STEPS BELOW)

```
Frontend URL: https://rupix3d-ecommerce.vercel.app
Backend API: https://rupix3d-ecommerce.railway.app
Admin Dashboard: https://rupix3d-ecommerce.vercel.app/admin
```

## STEP 1: Prepare Your Environment (2 minutes)

### 1.1 Generate GitHub Personal Access Token
1. Go to https://github.com/settings/tokens
2. Click "Generate new token (classic)"
3. Give it a name: `rupix3d-deploy`
4. Check `repo` and `workflow` scopes
5. Generate and **save the token** - you'll need it

### 1.2 Get All Code Files
```bash
# Clone the repository
git clone https://github.com/yanaamity/rupix3d-ecommerce.git
cd rupix3d-ecommerce

# You now have the repo structure
```

## STEP 2: Deploy Backend to Railway (3 minutes)

### 2.1 Create Railway Project
1. Go to: https://railway.app/dashboard
2. Click **+ New Project**
3. Select **GitHub Repo** (it will use OAuth to connect)
4. Search and select: `yanaamity/rupix3d-ecommerce`
5. Click **Deploy**

### 2.2 Add PostgreSQL Database
1. In your Railway project, click **+ Add Service**
2. Select **PostgreSQL**
3. It auto-creates with name `postgres`
4. Click the PostgreSQL service
5. Go to **Variables** tab
6. Copy the `DATABASE_URL` - save it

### 2.3 Add Redis Cache
1. Click **+ Add Service** again
2. Select **Redis**
3. Go to **Variables** tab
4. Copy the `REDIS_URL` - save it

### 2.4 Configure Backend Environment
1. Click the **Backend** service
2. Go to **Variables** tab
3. Add these variables:
   ```
      DATABASE_URL = [paste from PostgreSQL]
         REDIS_URL = [paste from Redis]
            JWT_SECRET = your_super_secret_key_123
               NODE_ENV = production
                  PORT = 3000
                     ```
                     4. Click **Deploy**

                     **RAILWAY BACKEND URL:** Copy the Railway deploy URL from the project dashboard

                     ---

                     ## STEP 3: Deploy Frontend to Vercel (3 minutes)

                     ### 3.1 Create Vercel Project
                     1. Go to: https://vercel.com/dashboard
                     2. Click **+ New Project**
                     3. Import Git Repository → Select `rupix3d-ecommerce`
                     4. Choose **Next.js** as framework
                     5. **IMPORTANT**: Set Environment Variable
                        - Key: `REACT_APP_API_URL`
                           - Value: `[Your Railway Backend URL]` (from Step 2.4)
                           6. Click **Deploy**

                           ### 3.2 Wait for Deployment
                           - Vercel will build and deploy automatically
                           - Takes 2-3 minutes
                           - You'll see a green ✓ when complete

                           **VERCEL FRONTEND URL:** https://[your-project]-rupix3d.vercel.app

                           ---

                           ## STEP 4: Add Your Code Files (2 minutes)

                           Now that services are deployed and watching your GitHub repo:

                           ```bash
                           # From your local rupix3d-ecommerce directory:

                           # Copy all source files to the repo
                           cp [all backend files] ./
                           cp [all frontend files] ./
                           cp [all config files] ./

                           # Commit and push
                           git add .
                           git commit -m "Add all source code files"
                           git push origin main
                           ```

                           Railway and Vercel will **automatically redeploy** when you push to GitHub.

                           ---

                           ## STEP 5: Test Your Live Application (1 minute)

                           ### Test Frontend
                           ```bash
                           # Open your browser to:
                           https://rupix3d-ecommerce.vercel.app

                           # You should see:
                           - Login page with phone OTP
                           - Product catalog
                           - Shopping cart
                           - Checkout flow
                           ```

                           ### Test Backend API
                           ```bash
                           # Check backend health:
                           curl https://rupix3d-ecommerce.railway.app/health

                           # Expected response: {"status": "ok"}
                           ```

                           ### Test Database Connection
                           ```bash
                           # In Railway dashboard:
                           # Click PostgreSQL service → Data → verify tables are created
                           # Click Redis service → verify connection active
                           ```

                           ---

                           ## YOUR LIVE URLS

                           ✅ **Frontend:** https://rupix3d-ecommerce.vercel.app
                           ✅ **Backend API:** https://rupix3d-ecommerce.railway.app
                           ✅ **Admin Panel:** https://rupix3d-ecommerce.vercel.app/admin
                           ✅ **API Docs:** https://rupix3d-ecommerce.railway.app/api-docs

                           ---

                           ## Monitoring & Logs

                           ### View Backend Logs
                           - Railway Dashboard → Your Project → Backend Service → Logs

                           ### View Frontend Logs  
                           - Vercel Dashboard → Your Project → Deployments → Logs

                           ### Monitor Database
                           - Railway Dashboard → PostgreSQL Service → Metrics

                           ---

                           ## Common Issues & Fixes

                           ### "Backend URL not connecting"
                           - Verify `REACT_APP_API_URL` in Vercel environment variables
                           - Ensure Railway backend is deployed (green status)
                           - Check CORS settings in backend code

                           ### "Database connection error"
                           - Verify PostgreSQL service is running in Railway
                           - Check `DATABASE_URL` is correctly set in backend variables
                           - Run migrations: `railway run npm run migrate`

                           ### "Build fails in Vercel"
                           - Check build logs in Vercel dashboard
                           - Ensure Node version is 16+
                           - Verify all dependencies are in package.json

                           ---

                           ## Performance & Optimization

                           ### Railway Settings
                           - Memory: Auto (recommended)
                           - CPU: Auto (recommended)
                           - Restart Policy: On crash

                           ### Vercel Settings
                           - Edge Functions: Auto
                           - Caching: Auto
                           - Deployment Regions: Global

                           ---

                           ## Next Steps

                           1. ✅ Deploy backend to Railway
                           2. ✅ Deploy frontend to Vercel
                           3. 📧 Set up email notifications (SMTP)
                           4. 💳 Configure payment gateway (Razorpay API keys)
                           5. 📊 Set up analytics (Google Analytics)
                           6. 🔐 Configure SSL certificates (auto with Railway/Vercel)
                           7. 🚀 Go live!

                           ---

                           ## Support

                           - **Railway Docs:** https://docs.railway.app
                           - **Vercel Docs:** https://vercel.com/docs
                           - **Backend API Docs:** [in your repository]
                           - **Issue Tracker:** GitHub Issues

                           ---

                           **Status:** ✅ Production Ready
                           **Deployment Time:** ~10 minutes
                           **Maintenance:** Automatic via GitHub CI/CD
                           **Scaling:** Auto-scales with usage

                           
