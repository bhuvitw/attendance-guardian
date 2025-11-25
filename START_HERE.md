# 🚀 START HERE - Complete Setup Guide

## Welcome! 👋

You now have a **complete full-stack attendance tracking application** with:
- ✅ Frontend (React + TypeScript)
- ✅ Backend (Node.js + Express)
- ✅ Database (PostgreSQL)
- ✅ Manual timetable entry
- ✅ Bulk attendance upload
- ✅ Day-by-day tracking
- ✅ Mid-semester support

## 📋 Quick Start (5 minutes)

### Option 1: Docker (Easiest) 🐳

```bash
# 1. Make sure Docker is installed
docker --version

# 2. Start everything
docker-compose up -d

# 3. Open your browser
open http://localhost:5173
```

That's it! Everything is running.

### Option 2: Manual Setup (More Control) 🛠️

#### Step 1: Database
```bash
# Install PostgreSQL (macOS)
brew install postgresql@14
brew services start postgresql@14

# Create database
createdb attendance_guardian
```

#### Step 2: Backend
```bash
# Go to server folder
cd server

# Install dependencies
npm install

# Setup environment
cp .env.example .env
# Edit .env with your database URL

# Run migrations
npm run prisma:migrate

# Start server
npm run dev
```

Backend runs on `http://localhost:3001`

#### Step 3: Frontend
```bash
# Go back to root
cd ..

# Install dependencies
npm install

# Setup environment
echo "VITE_API_URL=http://localhost:3001/api" > .env

# Start frontend
npm run dev
```

Frontend runs on `http://localhost:5173`

## 🎯 First Time Usage

### 1. Open the App
Navigate to `http://localhost:5173`

### 2. Setup Wizard
You'll see a 4-step wizard:

**Step 1: Timetable**
- Choose "Manual Entry" tab
- Add your subjects (name, code, teacher)
- Add weekly schedule (day, time, subject)
- Click "Save Timetable"
- Click "Continue"

**Step 2: Semester Info**
- Enter semester name (e.g., "Spring 2024")
- Set start date
- Set end date
- Set required attendance % (default: 75%)
- Click "Continue"

**Step 3: Past Attendance (Optional)**
- If starting mid-semester, upload past attendance
- Option A: Add records manually
- Option B: Import CSV
- Click "Continue"

**Step 4: Review**
- Check your setup
- Click "Finish Setup"

### 3. Dashboard
You'll be redirected to the dashboard showing:
- Average attendance
- Subjects at risk
- All your subjects
- Risk meter

### 4. Mark Attendance
- Click "Mark" button
- Select today's date
- Mark each class as Present/Absent
- Stats update automatically

## 📚 Key Features

### Manual Timetable Entry
- No need for image upload
- Add subjects manually
- Create weekly schedule
- Full control over data

### Bulk Attendance Upload
- Upload past attendance
- CSV import support
- Perfect for mid-semester start
- Automatic stats calculation

### Day-by-Day Tracking
- Each class has a specific date
- View attendance history
- Edit past records
- Calendar view

### Database Backend
- All data in PostgreSQL
- No data loss
- Real-time sync
- Scalable

## 🗂️ Project Structure

```
attendance-guardian/
├── server/              # Backend
│   ├── src/
│   │   ├── index.js    # Express server
│   │   └── routes/     # API endpoints
│   ├── prisma/
│   │   └── schema.prisma
│   └── package.json
│
├── src/                 # Frontend
│   ├── components/
│   │   ├── ManualTimetableEntry.tsx
│   │   ├── BulkAttendanceUpload.tsx
│   │   └── ...
│   ├── pages/
│   │   ├── SetupWizard.tsx
│   │   ├── Dashboard.tsx
│   │   └── ...
│   └── lib/
│       └── api.ts      # API client
│
└── docker-compose.yml   # Docker setup
```

## 📖 Documentation

- **[FULLSTACK_SETUP.md](./FULLSTACK_SETUP.md)** - Detailed setup instructions
- **[COMPLETE_FEATURES.md](./COMPLETE_FEATURES.md)** - All features explained
- **[DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md)** - Deploy to production
- **[FEATURES.md](./FEATURES.md)** - Original features
- **[INTEGRATION_GUIDE.md](./INTEGRATION_GUIDE.md)** - OCR integration

## 🔧 Common Commands

### Backend
```bash
cd server
npm run dev          # Start development server
npm run prisma:studio # Open database GUI
npm run prisma:migrate # Run migrations
```

### Frontend
```bash
npm run dev          # Start development server
npm run build        # Build for production
npm run preview      # Preview production build
```

### Docker
```bash
docker-compose up -d     # Start all services
docker-compose down      # Stop all services
docker-compose logs -f   # View logs
docker-compose ps        # Check status
```

## 🐛 Troubleshooting

### Database Connection Error
```bash
# Check PostgreSQL is running
pg_isready

# Check connection
psql -U attendance_user -d attendance_guardian
```

### Port Already in Use
```bash
# Kill process on port 3001
lsof -ti:3001 | xargs kill -9

# Kill process on port 5173
lsof -ti:5173 | xargs kill -9
```

### Prisma Issues
```bash
cd server
npm run prisma:generate
npm run prisma:migrate reset
```

## 🎓 Example Workflows

### Workflow 1: New Semester, Start from Beginning
1. Open app → Setup Wizard
2. Add 5 subjects manually
3. Add 20 weekly class slots
4. Set semester: Jan 15 - May 31
5. Skip past attendance
6. Finish setup
7. Start marking attendance daily

### Workflow 2: Mid-Semester Start
1. Open app → Setup Wizard
2. Add subjects
3. Add schedule
4. Set semester dates (including past)
5. Upload 50 past attendance records
6. Finish setup
7. Dashboard shows current stats
8. Continue marking attendance

### Workflow 3: CSV Import
1. Download CSV template
2. Fill in your data:
   ```csv
   SubjectCode,Date,Status
   CS201,2024-01-15,PRESENT
   CS202,2024-01-15,ABSENT
   ```
3. Upload CSV in Step 3
4. System imports all records
5. Stats calculated automatically

## 🎯 What's Different from Before?

### Before (LocalStorage Version)
- ❌ Static subject list
- ❌ No database
- ❌ Counter-based attendance
- ❌ No date tracking
- ❌ Data loss on clear
- ❌ No mid-semester support

### Now (Full-Stack Version)
- ✅ Dynamic subjects
- ✅ PostgreSQL database
- ✅ Day-by-day attendance
- ✅ Date-specific tracking
- ✅ Persistent data
- ✅ Mid-semester support
- ✅ Bulk operations
- ✅ Manual entry
- ✅ CSV import/export
- ✅ RESTful API

## 🚀 Next Steps

1. **Test the Setup**
   - Add a few subjects
   - Create a schedule
   - Mark some attendance
   - Check the dashboard

2. **Customize**
   - Adjust required percentages
   - Add holidays
   - Set weekly offs

3. **Deploy** (Optional)
   - See [DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md)
   - Deploy to Heroku, Railway, or Vercel

4. **Enhance** (Optional)
   - Add user authentication
   - Integrate real OCR
   - Add email notifications

## 💡 Tips

- **Use Manual Entry**: More reliable than image upload
- **Import CSV**: Fastest way to add past attendance
- **Mark Daily**: Don't let it pile up
- **Check Dashboard**: Monitor your risk levels
- **Backup Data**: Export from Prisma Studio

## 🎉 You're Ready!

Everything is set up and ready to use. Start by:
1. Opening `http://localhost:5173`
2. Going through the Setup Wizard
3. Adding your subjects and schedule
4. Marking your first attendance

**Happy tracking!** 📊

---

## 📞 Need Help?

- Check [FULLSTACK_SETUP.md](./FULLSTACK_SETUP.md) for detailed setup
- See [COMPLETE_FEATURES.md](./COMPLETE_FEATURES.md) for feature docs
- Review [DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md) for deployment
- Check server logs: `docker-compose logs -f backend`
- Check database: `npm run prisma:studio` (in server/)

## 🔗 Quick Links

- Frontend: http://localhost:5173
- Backend API: http://localhost:3001
- API Health: http://localhost:3001/health
- Database GUI: http://localhost:5555 (run `npm run prisma:studio`)

---

**Everything you need is here. Let's go!** 🚀
