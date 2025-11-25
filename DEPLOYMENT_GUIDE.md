# Deployment Guide

## 🚀 Quick Deploy with Docker

### Prerequisites
- Docker and Docker Compose installed
- Git

### Steps

```bash
# Clone repository
git clone <your-repo-url>
cd attendance-guardian

# Start all services
docker-compose up -d

# Check status
docker-compose ps

# View logs
docker-compose logs -f
```

Access the app at `http://localhost:5173`

### Stop Services
```bash
docker-compose down

# Stop and remove volumes (deletes data)
docker-compose down -v
```

## 🌐 Manual Deployment

### 1. Deploy Database

#### Heroku Postgres
```bash
heroku addons:create heroku-postgresql:mini
heroku config:get DATABASE_URL
```

#### Railway
1. Create new project
2. Add PostgreSQL service
3. Copy connection string

#### Supabase
1. Create new project
2. Get connection string from Settings → Database

### 2. Deploy Backend

#### Heroku
```bash
cd server

# Create Heroku app
heroku create attendance-guardian-api

# Set environment variables
heroku config:set DATABASE_URL="your-database-url"
heroku config:set NODE_ENV=production

# Deploy
git subtree push --prefix server heroku main

# Run migrations
heroku run npm run prisma:migrate deploy
```

#### Railway
```bash
cd server

# Install Railway CLI
npm install -g @railway/cli

# Login and init
railway login
railway init

# Deploy
railway up

# Set environment variables in Railway dashboard
```

#### Render
1. Connect GitHub repository
2. Select `server` directory as root
3. Set build command: `npm install && npx prisma generate`
4. Set start command: `npm start`
5. Add environment variables

### 3. Deploy Frontend

#### Vercel
```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel

# Set environment variable
vercel env add VITE_API_URL production
# Enter your backend URL
```

#### Netlify
```bash
# Install Netlify CLI
npm install -g netlify-cli

# Build
npm run build

# Deploy
netlify deploy --prod --dir=dist

# Set environment variable in Netlify dashboard
```

#### GitHub Pages
```bash
# Build
npm run build

# Deploy to gh-pages branch
npm install -g gh-pages
gh-pages -d dist
```

## 🔧 Environment Variables

### Backend (.env)
```env
DATABASE_URL="postgresql://user:pass@host:5432/db"
PORT=3001
NODE_ENV=production
```

### Frontend (.env.production)
```env
VITE_API_URL=https://your-backend-url.com/api
```

## 📊 Database Migration

### Initial Setup
```bash
cd server
npm run prisma:migrate deploy
```

### Seed Data (Optional)
```bash
npm run prisma:seed
```

## 🔒 Security Checklist

- [ ] Use strong database passwords
- [ ] Enable SSL for database connections
- [ ] Set NODE_ENV=production
- [ ] Use environment variables for secrets
- [ ] Enable CORS only for your frontend domain
- [ ] Add rate limiting
- [ ] Implement authentication
- [ ] Use HTTPS for all connections

## 📈 Monitoring

### Health Checks
```bash
# Backend health
curl https://your-backend-url.com/health

# Database connection
curl https://your-backend-url.com/api/semesters/current
```

### Logs
```bash
# Heroku
heroku logs --tail

# Railway
railway logs

# Docker
docker-compose logs -f backend
```

## 🔄 Updates

### Backend Updates
```bash
cd server
git pull
npm install
npm run prisma:migrate deploy
npm start
```

### Frontend Updates
```bash
git pull
npm install
npm run build
# Deploy dist/ folder
```

## 💾 Backup

### Database Backup
```bash
# PostgreSQL dump
pg_dump -h host -U user -d database > backup.sql

# Restore
psql -h host -U user -d database < backup.sql
```

### Automated Backups
- Heroku: Automatic with paid plans
- Railway: Configure in dashboard
- Supabase: Automatic daily backups

## 🎯 Performance Optimization

### Backend
- Enable gzip compression
- Add Redis caching
- Use connection pooling
- Optimize database queries
- Add indexes

### Frontend
- Enable CDN
- Compress assets
- Lazy load routes
- Use service workers
- Enable caching

## 🐛 Troubleshooting

### Database Connection Failed
```bash
# Check connection string
echo $DATABASE_URL

# Test connection
psql $DATABASE_URL

# Check Prisma client
cd server
npm run prisma:generate
```

### API Not Responding
```bash
# Check server logs
docker-compose logs backend

# Check port
lsof -i :3001

# Restart service
docker-compose restart backend
```

### Frontend Build Failed
```bash
# Clear cache
rm -rf node_modules dist
npm install
npm run build

# Check environment variables
cat .env
```

## 📱 Mobile Deployment

### Progressive Web App (PWA)
1. Add manifest.json
2. Add service worker
3. Enable HTTPS
4. Test with Lighthouse

### React Native (Future)
- Use same API
- Reuse business logic
- Native UI components

## 🌍 Multi-Region Deployment

### Database Replication
- Primary in one region
- Read replicas in others
- Use connection pooling

### CDN for Frontend
- Cloudflare
- AWS CloudFront
- Vercel Edge Network

## 📊 Scaling

### Horizontal Scaling
- Multiple backend instances
- Load balancer
- Database connection pooling

### Vertical Scaling
- Increase server resources
- Optimize queries
- Add caching layer

## 🎉 Post-Deployment

1. Test all features
2. Monitor error rates
3. Check performance
4. Set up alerts
5. Document API
6. Create user guide

---

**Your app is now live!** 🚀

Access it at your deployed URL and start tracking attendance!
