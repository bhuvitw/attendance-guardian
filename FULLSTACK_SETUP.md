# Full-Stack Setup Guide

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     Frontend (React)                     │
│  - React + TypeScript + Vite                            │
│  - Tailwind CSS + shadcn/ui                             │
│  - React Router + React Query                           │
└──────────────────┬──────────────────────────────────────┘
                   │ HTTP/REST API
┌──────────────────▼──────────────────────────────────────┐
│                  Backend (Node.js)                       │
│  - Express.js                                           │
│  - Prisma ORM                                           │
│  - RESTful API                                          │
└──────────────────┬──────────────────────────────────────┘
                   │ SQL
┌──────────────────▼──────────────────────────────────────┐
│                Database (PostgreSQL)                     │
│  - User data                                            │
│  - Semesters, Subjects, Classes                         │
│  - Attendance records                                   │
└─────────────────────────────────────────────────────────┘
```

## 📋 Prerequisites

- Node.js 18+ and npm
- PostgreSQL 14+
- Git

## 🚀 Quick Start

### 1. Database Setup

#### Option A: Local PostgreSQL

```bash
# Install PostgreSQL (macOS)
brew install postgresql@14
brew services start postgresql@14

# Create database
createdb attendance_guardian

# Create user (optional)
psql postgres
CREATE USER attendance_user WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE attendance_guardian TO attendance_user;
\q
```

#### Option B: Docker PostgreSQL

```bash
docker run --name attendance-db \
  -e POSTGRES_DB=attendance_guardian \
  -e POSTGRES_USER=attendance_user \
  -e POSTGRES_PASSWORD=your_password \
  -p 5432:5432 \
  -d postgres:14
```

### 2. Backend Setup

```bash
# Navigate to server directory
cd server

# Install dependencies
npm install

# Create .env file
cp .env.example .env

# Edit .env with your database credentials
# DATABASE_URL="postgresql://attendance_user:your_password@localhost:5432/attendance_guardian?schema=public"

# Generate Prisma client
npm run prisma:generate

# Run migrations
npm run prisma:migrate

# Start development server
npm run dev
```

Server will run on `http://localhost:3001`

### 3. Frontend Setup

```bash
# Navigate to project root
cd ..

# Install dependencies (if not already done)
npm install

# Create .env file
echo "VITE_API_URL=http://localhost:3001/api" > .env

# Start development server
npm run dev
```

Frontend will run on `http://localhost:5173`

## 📁 Project Structure

```
attendance-guardian/
├── server/                    # Backend
│   ├── src/
│   │   ├── index.js          # Express server
│   │   └── routes/           # API routes
│   │       ├── semester.js
│   │       ├── subject.js
│   │       ├── class.js
│   │       ├── holiday.js
│   │       └── stats.js
│   ├── prisma/
│   │   └── schema.prisma     # Database schema
│   ├── package.json
│   └── .env
│
├── src/                       # Frontend
│   ├── components/           # React components
│   │   ├── ManualTimetableEntry.tsx
│   │   ├── BulkAttendanceUpload.tsx
│   │   ├── TimetableUpload.tsx
│   │   └── ThemeToggle.tsx
│   ├── pages/               # Page components
│   │   ├── SetupWizard.tsx
│   │   ├── Dashboard.tsx
│   │   └── ...
│   ├── lib/
│   │   └── api.ts           # API client
│   └── ...
│
├── package.json
└── .env
```

## 🗄️ Database Schema

### Tables

**User**
- id (UUID, PK)
- email (String, unique)
- name (String)
- createdAt, updatedAt

**Semester**
- id (UUID, PK)
- name (String)
- startDate, endDate (DateTime)
- requiredPercentage (Float)
- userId (FK → User)

**Subject**
- id (UUID, PK)
- name, code, teacher (String)
- requiredPercentage (Float)
- semesterId (FK → Semester)

**Class**
- id (UUID, PK)
- subjectId (FK → Subject)
- date (DateTime)
- dayOfWeek, startTime, endTime (String)
- status (Enum: SCHEDULED, PRESENT, ABSENT, CANCELLED, DUTY_LEAVE, MEDICAL_LEAVE)
- notes (String, optional)

**Holiday**
- id (UUID, PK)
- date (DateTime)
- name (String)
- type (Enum: HOLIDAY, WEEKLY_OFF, DUTY_LEAVE, MEDICAL_LEAVE)
- semesterId (FK → Semester)

## 🔌 API Endpoints

### Semesters
- `GET /api/semesters` - Get all semesters
- `GET /api/semesters/current` - Get current semester
- `POST /api/semesters` - Create semester
- `PUT /api/semesters/:id` - Update semester
- `DELETE /api/semesters/:id` - Delete semester

### Subjects
- `GET /api/subjects?semesterId=xxx` - Get all subjects
- `GET /api/subjects/:id` - Get subject with stats
- `POST /api/subjects` - Create subject
- `POST /api/subjects/bulk` - Bulk create subjects
- `PUT /api/subjects/:id` - Update subject
- `DELETE /api/subjects/:id` - Delete subject

### Classes
- `GET /api/classes?subjectId=xxx` - Get classes
- `GET /api/classes/date/:date?semesterId=xxx` - Get classes by date
- `PATCH /api/classes/:id/attendance` - Mark attendance
- `POST /api/classes/bulk-attendance` - Bulk mark attendance
- `POST /api/classes` - Create class
- `POST /api/classes/bulk` - Bulk create classes
- `PUT /api/classes/:id` - Update class
- `DELETE /api/classes/:id` - Delete class

### Holidays
- `GET /api/holidays?semesterId=xxx` - Get holidays
- `POST /api/holidays` - Create holiday
- `POST /api/holidays/bulk` - Bulk create holidays
- `DELETE /api/holidays/:id` - Delete holiday

### Stats
- `GET /api/stats/semester/:semesterId` - Get semester stats
- `GET /api/stats/subject/:subjectId/trend` - Get attendance trend

## 🎯 Key Features

### 1. Manual Timetable Entry
- Add subjects one by one
- Define weekly schedule
- Assign subjects to time slots

### 2. Bulk Attendance Upload
- Upload past attendance via UI
- Import from CSV
- Support for mid-semester start

### 3. Day-by-Day Attendance
- Mark attendance for specific dates
- View attendance history
- Edit past records

### 4. Database Persistence
- All data stored in PostgreSQL
- Real-time sync
- No data loss

## 🧪 Testing the API

### Using curl

```bash
# Health check
curl http://localhost:3001/health

# Create semester
curl -X POST http://localhost:3001/api/semesters \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Spring 2024",
    "startDate": "2024-01-15",
    "endDate": "2024-05-31",
    "requiredPercentage": 75,
    "userId": "default-user"
  }'

# Get current semester
curl http://localhost:3001/api/semesters/current?userId=default-user

# Create subject
curl -X POST http://localhost:3001/api/subjects \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Data Structures",
    "code": "CS201",
    "teacher": "Dr. Smith",
    "requiredPercentage": 75,
    "semesterId": "your-semester-id"
  }'
```

### Using Prisma Studio

```bash
cd server
npm run prisma:studio
```

Opens a GUI at `http://localhost:5555` to view/edit database.

## 🐛 Troubleshooting

### Database Connection Issues

```bash
# Check PostgreSQL is running
pg_isready

# Check connection
psql -U attendance_user -d attendance_guardian

# Reset database
cd server
npx prisma migrate reset
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
# Regenerate client
cd server
npm run prisma:generate

# Reset and reseed
npm run prisma:migrate reset
```

## 🔒 Environment Variables

### Backend (.env in server/)
```env
DATABASE_URL="postgresql://user:password@localhost:5432/attendance_guardian?schema=public"
PORT=3001
NODE_ENV=development
```

### Frontend (.env in root)
```env
VITE_API_URL=http://localhost:3001/api
```

## 📦 Production Deployment

### Backend

```bash
cd server
npm install --production
npm run prisma:generate
npm run prisma:migrate deploy
npm start
```

### Frontend

```bash
npm run build
# Serve dist/ folder with nginx or similar
```

### Docker Compose (Full Stack)

See `docker-compose.yml` for complete setup.

## 🎓 Usage Flow

1. **Setup Wizard**
   - Choose manual entry or image upload
   - Add subjects and schedule
   - Set semester dates
   - Upload past attendance (optional)

2. **Daily Use**
   - View dashboard
   - Mark today's attendance
   - Check subject details
   - Monitor risk levels

3. **Mid-Semester Start**
   - Use bulk upload feature
   - Import CSV with past records
   - System calculates current stats

## 📊 Data Flow

```
User Input → Frontend → API → Prisma → PostgreSQL
                ↓
         localStorage (cache)
```

## 🔄 Migration from LocalStorage

If you have existing data in localStorage:

1. Export data from browser console:
```javascript
const data = localStorage.getItem('attendance-data');
console.log(JSON.parse(data));
```

2. Use bulk upload feature to import into database

## 🚀 Next Steps

- [ ] Add user authentication
- [ ] Implement real OCR for timetable upload
- [ ] Add email notifications
- [ ] Create mobile app
- [ ] Add data export features
- [ ] Implement analytics dashboard

## 📞 Support

For issues or questions:
- Check the API health: `http://localhost:3001/health`
- View Prisma Studio: `npm run prisma:studio`
- Check server logs
- Review browser console

---

**You're all set!** 🎉 Start the backend and frontend servers, then navigate to `http://localhost:5173` to begin.
