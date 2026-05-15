# Rupix3D Ecommerce - Complete Setup Guide

## Quick Start (5 minutes)

This repository contains all code for the Rupix3D ecommerce platform. Follow these steps to get it deployed:

### Step 1: Clone and Prepare Local Environment

```bash
git clone https://github.com/yanaamity/rupix3d-ecommerce.git
cd rupix3d-ecommerce
npm install  # Install root dependencies
```

### Step 2: Set Up Environment Variables

Create `.env.local` file in root:

```
DATABASE_URL=your_postgresql_url
REDIS_URL=your_redis_url
JWT_SECRET=your_jwt_secret_key
NODE_ENV=production
PORT=3000
```

### Step 3: Deploy Backend to Railway

1. Go to https://railway.app
2. Click "New Project"
3. Select "GitHub Repo" and authorize
4. Select "yanaamity/rupix3d-ecommerce"
5. Railway detects `railway.json` and auto-configures
6. Add PostgreSQL service: click "+" → Add Postgres
7. Add Redis service: click "+" → Add Redis
8. Set environment variables from `railway.json`
9. Deploy!

**Note:** Railway will automatically read your Dockerfile and deploy the backend

### Step 4: Deploy Frontend to Vercel

1. Go to https://vercel.com
2. Click "New Project"
3. Import GitHub Repository → select "rupix3d-ecommerce"
4. Framework: Next.js
5. Environment Variables:
   - `REACT_APP_API_URL` = your Railway backend URL
   6. Deploy!

   ### Step 5: Configure API Connection

   Update `frontend_api_client.js` with your Railway backend URL:

   ```javascript
   const API_BASE_URL = process.env.REACT_APP_API_URL || 'https://your-railway-backend-url.railway.app';
   ```

   ## Deployment Architecture

   ```
   ┌─────────────────────┐
   │   Vercel Frontend   │ (React + Next.js)
   │   rupix3d-ui.com    │
   └──────────┬──────────┘
              │ API calls
                         ↓
                         ┌─────────────────────┐
                         │  Railway Backend    │ (Node.js Express)
                         │  Railway PostgreSQL │
                         │  Railway Redis      │
                         └─────────────────────┘
                         ```

                         ## Complete File Structure

                         ### Frontend Files (React/Next.js)
                         - `rupix3d_design_system.js` - Design system and styles
                         - `rupix3d_pages_*.jsx` - All page components
                         - `frontend_api_client.js` - API integration
                         - `frontend_useAuth.js` - Auth hook
                         - `frontend_package.json` - Frontend dependencies

                         ### Backend Files (Express.js)
                         - `backend_server.js` - Main Express server
                         - `backend_auth_routes.js` - Authentication endpoints
                         - `backend_products_routes.js` - Product CRUD
                         - `backend_cart_routes.js` - Shopping cart
                         - `backend_orders_routes.js` - Order management
                         - `backend_coupons_routes.js` - Discount system
                         - `backend_referrals_routes.js` - Referral system
                         - `database_schema.sql` - PostgreSQL schema
                         - `backend_package.json` - Backend dependencies

                         ### Configuration Files
                         - `railway.json` - Railway deployment config
                         - `vercel.json` - Vercel deployment config
                         - `docker-compose.yml` - Local Docker setup
                         - `Dockerfile.backend` - Backend containerization
                         - `Dockerfile.frontend` - Frontend containerization

                         ## Features Included

                         ✅ Phone OTP Authentication
                         ✅ Product Catalog with Material/Size/Color Variants  
                         ✅ Shopping Cart & Checkout
                         ✅ Coupon & Discount System
                         ✅ Referral System with Earning Codes
                         ✅ Order Tracking with Live Printer Telemetry
                         ✅ Custom 3D File Uploads with Auto-Pricing
                         ✅ Member Tier System (Bronze → Silver → Gold → Platinum)
                         ✅ Admin Dashboard
                         ✅ Email Notifications
                         ✅ Payment Gateway Integration (Razorpay Ready)

                         ## API Endpoints Reference

                         ### Authentication
                         - `POST /auth/send-otp` - Send OTP to phone
                         - `POST /auth/verify-otp` - Verify OTP and login
                         - `POST /auth/logout` - Logout user

                         ### Products  
                         - `GET /products` - List all products
                         - `GET /products/:id` - Get product details
                         - `GET /products/search?q=keyword` - Search products

                         ### Orders
                         - `POST /orders` - Create new order
                         - `GET /orders/:id` - Get order details
                         - `GET /orders/:id/tracking` - Get order tracking info

                         ### Custom 3D
                         - `POST /custom-3d/upload` - Upload STL/OBJ file
                         - `POST /custom-3d/quote` - Get price quote
                         - `POST /custom-3d/order` - Place custom order

                         ## Troubleshooting

                         **Railway deployment fails:**
                         - Check that railway.json exists
                         - Verify PostgreSQL and Redis are added as services
                         - Check logs in Railway dashboard

                         **Vercel frontend errors:**
                         - Set `REACT_APP_API_URL` environment variable
                         - Ensure backend is deployed and accessible
                         - Check network tab in browser dev tools

                         **API calls returning 404:**
                         - Verify backend is running: `curl https://your-backend-url/health`
                         - Check CORS settings in `backend_server.js`
                         - Ensure frontend URL is whitelisted

                         ## Local Development (Optional)

                         To run locally with Docker:

                         ```bash
                         docker-compose up --build
                         ```

                         This starts:
                         - PostgreSQL on localhost:5432
                         - Redis on localhost:6379
                         - Backend on localhost:3000
                         - Frontend on localhost:3001

                         ## Next Steps

                         1. Deploy backend to Railway
                         2. Deploy frontend to Vercel
                         3. Test live URLs
                         4. Configure payment gateway credentials
                         5. Set up email notifications
                         6. Monitor application performance

                         ## Support

                         For deployment issues, check:
                         - Railway Logs: Dashboard → Project → Logs
                         - Vercel Logs: Dashboard → Project → Logs
                         - GitHub Actions: Actions tab for CI/CD status

                         ---

                         **Status:** Production Ready
                         **Last Updated:** May 15, 2026
                         **Version:** 1.0.0
                         
