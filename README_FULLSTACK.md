# 🎓 Attendance Guardian - Full-Stack Edition

> A complete attendance tracking system with manual entry, bulk upload, and database backend

[![React](https://img.shields.io/badge/React-18-blue)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-blue)](https://www.typescriptlang.org/)
[![Node.js](https://img.shields.io/badge/Node.js-18-green)](https://nodejs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-14-blue)](https://www.postgresql.org/)
[![Prisma](https://img.shields.io/badge/Prisma-5-2D3748)](https://www.prisma.io/)

## ✨ What's New in Full-Stack Version

### 🎯 Core Features
- ✅ **Manual Timetable Entry** - Add subjects and schedule without image upload
- ✅ **Bulk Attendance Upload** - Import past attendance via CSV or manual entry
- ✅ **Day-by-Day Tracking** - Track attendance for specific dates, not just counters
- ✅ **PostgreSQL Database** - Persistent storage, no data loss
- ✅ **RESTful API** - Complete backend with Express.js
- ✅ **Mid-Semester Support** - Start using the app anytime during semester

### 🚀 Technical Stack

**Frontend**
- React 18 + TypeScript
- Vite for blazing fast builds
- Tailwind CSS + shadcn/ui
- React Router + React Query
- Dark/Light theme support

**Backend**
- Node.js 18 + Express.js
- Prisma ORM for type-safe database access
- PostgreSQL for reliable data storage
- RESTful API design
- CORS enabled

**DevOps**
- Docker & Docker Compose
- Nginx for production
- Environment-based configuration
- Health check endpoints

## 📸 Screenshots

### Setup Wizard
![Setup Wizard](docs/setup-wizard.png)

### Manual Entry
![Manual Entry](docs/manual-entry.png)

### Bulk Upload
![Bulk Upload](docs/bulk-upload.png)

### Dashboard
![Dashboard](docs/dashboard.png)

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- PostgreSQL 14+ (or Docker)
- npm or yarn

### Option 1: Docker (Recommended)

```bash
# Clone repository
git clone <your-repo-url>
cd attendance-guardian

# Start all services
docker-compose up -d

# Open browser
open http://localhost:5173
```

### Option 2: Manual Setup

```bash
# 1. Setup Database
createdb attendance_guardian

# 2. Setup Backend
cd server
npm install
cp .env.example .env
# Edit .env with your database URL
npm run prisma:migrate
npm run dev

# 3. Setup Frontend (in new terminal)
cd ..
npm install
echo "VITE_API_URL=http://localhost:3001/api" > .env
npm run dev
```

## 📖 Documentation

| Document | Description |
|----------|-------------|
| **[START_HERE.md](./START_HERE.md)** | 👈 **Begin here!** Quick start guide |
| [FULLSTACK_SETUP.md](./FULLSTACK_SETUP.md) | Detailed setup instructions |
| [COMPLETE_FEATURES.md](./COMPLETE_FEATURES.md) | All features explained |
| [DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md) | Production deployment |
| [INTEGRATION_GUIDE.md](./INTEGRATION_GUIDE.md) | OCR integration guide |

## 🎯 Key Features Explained

### 1. Manual Timetable Entry
No need to upload images - add everything manually:
- Add subjects with name, code, teacher
- Create weekly schedule with time slots
- Assign subjects to specific days/times
- Full validation and error handling

### 2. Bulk Attendance Upload
Perfect for mid-semester start:
- Upload past attendance records
- CSV import with template
- Manual entry for individual records
- Automatic stats calculation

### 3. Day-by-Day Tracking
Track attendance for specific dates:
- Each class has a date and time
- View attendance history
- Edit past records
- Calendar view of classes

### 4. Database Backend
Reliable data storage:
- PostgreSQL database
- Prisma ORM for type safety
- RESTful API
- No data loss on refresh

## 🗂️ Project Structure

```
attendance-guardian/
├── server/                      # Backend
│   ├── src/
│   │   ├── index.js            # Express server
│   │   └── routes/             # API endpoints
│   │       ├── semester.js
│   │       ├── subject.js
│   │       ├── class.js
│   │       ├── holiday.js
│   │       └── stats.js
│   ├── prisma/
│   │   └── schema.prisma       # Database schema
│   └── package.json
│
├── src/                         # Frontend
│   ├── components/
│   │   ├── ManualTimetableEntry.tsx
│   │   ├── BulkAttendanceUpload.tsx
│   │   ├── TimetableUpload.tsx
│   │   └── ThemeToggle.tsx
│   ├── pages/
│   │   ├── SetupWizard.tsx     # New setup flow
│   │   ├── Dashboard.tsx
│   │   ├── Attendance.tsx
│   │   └── Settings.tsx
│   ├── lib/
│   │   └── api.ts              # API client
│   └── hooks/
│       └── useAttendanceData.ts
│
├── docker-compose.yml           # Docker setup
├── Dockerfile                   # Frontend container
└── server/Dockerfile            # Backend container
```

## 🔌 API Endpoints

### Semesters
- `GET /api/semesters` - List all semesters
- `GET /api/semesters/current` - Get current semester
- `POST /api/semesters` - Create semester
- `PUT /api/semesters/:id` - Update semester
- `DELETE /api/semesters/:id` - Delete semester

### Subjects
- `GET /api/subjects?semesterId=xxx` - List subjects
- `POST /api/subjects` - Create subject
- `POST /api/subjects/bulk` - Bulk create subjects
- `PUT /api/subjects/:id` - Update subject
- `DELETE /api/subjects/:id` - Delete subject

### Classes (Attendance)
- `GET /api/classes?subjectId=xxx` - List classes
- `GET /api/classes/date/:date` - Classes by date
- `PATCH /api/classes/:id/attendance` - Mark attendance
- `POST /api/classes/bulk` - Bulk create classes
- `POST /api/classes/bulk-attendance` - Bulk mark attendance

### Stats
- `GET /api/stats/semester/:id` - Semester statistics
- `GET /api/stats/subject/:id/trend` - Attendance trend

## 🎓 Usage Examples

### Example 1: New Semester
```bash
# 1. Open app
open http://localhost:5173

# 2. Setup Wizard
- Add 5 subjects manually
- Create weekly schedule (20 slots)
- Set semester dates
- Skip past attendance
- Finish setup

# 3. Start marking attendance
```

### Example 2: Mid-Semester Start
```bash
# 1. Setup Wizard
- Add subjects
- Create schedule
- Set semester dates (including past)

# 2. Upload past attendance
- Download CSV template
- Fill in 50 records
- Upload CSV

# 3. Dashboard shows current stats
```

### Example 3: CSV Import
```csv
SubjectCode,Date,Status
CS201,2024-01-15,PRESENT
CS202,2024-01-15,ABSENT
CS201,2024-01-16,PRESENT
CS203,2024-01-16,DUTY_LEAVE
```

## 🔧 Development

### Backend Development
```bash
cd server
npm run dev              # Start with nodemon
npm run prisma:studio    # Open database GUI
npm run prisma:migrate   # Run migrations
```

### Frontend Development
```bash
npm run dev              # Start Vite dev server
npm run build            # Build for production
npm run preview          # Preview production build
```

### Database Management
```bash
cd server
npm run prisma:studio    # GUI at http://localhost:5555
npm run prisma:migrate   # Create migration
npx prisma migrate reset # Reset database
```

## 🐛 Troubleshooting

### Database Connection Error
```bash
# Check PostgreSQL
pg_isready

# Test connection
psql -U attendance_user -d attendance_guardian

# Reset database
cd server && npm run prisma:migrate reset
```

### Port Already in Use
```bash
# Backend (3001)
lsof -ti:3001 | xargs kill -9

# Frontend (5173)
lsof -ti:5173 | xargs kill -9
```

### Prisma Issues
```bash
cd server
rm -rf node_modules
npm install
npm run prisma:generate
npm run prisma:migrate
```

## 🚀 Deployment

### Quick Deploy with Docker
```bash
docker-compose up -d
```

### Deploy to Cloud
See [DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md) for:
- Heroku
- Railway
- Vercel
- Netlify
- AWS
- Digital Ocean

## 📊 Database Schema

```prisma
model Semester {
  id                  String
  name                String
  startDate           DateTime
  endDate             DateTime
  requiredPercentage  Float
  subjects            Subject[]
  holidays            Holiday[]
}

model Subject {
  id                  String
  name                String
  code                String
  teacher             String
  requiredPercentage  Float
  classes             Class[]
}

model Class {
  id          String
  date        DateTime
  dayOfWeek   String
  startTime   String
  endTime     String
  status      ClassStatus
  notes       String?
}
```

## 🎯 Roadmap

- [ ] User authentication
- [ ] Multi-user support
- [ ] Real-time sync
- [ ] Mobile app (React Native)
- [ ] Push notifications
- [ ] Email reports
- [ ] Advanced analytics
- [ ] AI predictions
- [ ] LMS integration
- [ ] Attendance certificates

## 🤝 Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📄 License

MIT License - see LICENSE file

## 🙏 Acknowledgments

- shadcn/ui for beautiful components
- Prisma for amazing ORM
- Vercel for hosting
- All contributors

## 📞 Support

- 📧 Email: support@example.com
- 💬 Discord: [Join our server](#)
- 🐛 Issues: [GitHub Issues](#)
- 📖 Docs: [Full Documentation](#)

## ⭐ Star History

If you find this project useful, please consider giving it a star!

---

**Built with ❤️ for students who want to track their attendance effectively**

[Get Started](./START_HERE.md) | [Documentation](./FULLSTACK_SETUP.md) | [Deploy](./DEPLOYMENT_GUIDE.md)
