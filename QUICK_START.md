# Quick Start Guide

## 🎯 Getting Your App Running

### 1. Install Dependencies
```bash
npm install
```

### 2. Start Development Server
```bash
npm run dev
```

The app will open at `http://localhost:5173`

## 🎓 First Time User Flow

### Step 1: Onboarding - Upload Timetable
1. When you first open the app, you'll see the onboarding screen
2. **Upload your timetable**:
   - Click the upload area or drag & drop your timetable image
   - Supported formats: PNG, JPG, PDF (max 10MB)
   - Wait for the system to process and extract subjects
3. Review the detected subjects
4. Click "Continue"

> **Note**: Currently uses mock data. See [INTEGRATION_GUIDE.md](./INTEGRATION_GUIDE.md) to integrate real OCR.

### Step 2: Set Semester Dates
1. Enter your semester start date
2. Enter your semester end date
3. Select weekly holidays (e.g., Sunday)
4. Add any additional holiday dates
5. Click "Continue"

### Step 3: Configure Leave Rules
1. Enable/disable Duty Leave tracking
2. Add duty leave dates if applicable
3. Enable/disable Medical Leave tracking
4. Add medical leave dates if applicable
5. Click "Continue"

### Step 4: Review & Complete
1. Review your configuration summary
2. Click "Finish Setup"
3. You'll be redirected to the Dashboard

## 📊 Using the Dashboard

### Main Dashboard
- **Stats Overview**: See your average attendance, subjects at risk, and overall status
- **Risk Meter**: Visual representation of your attendance health
- **Subject Cards**: Click any subject to view detailed information

### Quick Actions
- **Mark Attendance**: Click the calendar icon to mark today's attendance
- **Theme Toggle**: Click sun/moon icon to switch between light/dark mode
- **Settings**: Click gear icon to access settings

## ✅ Marking Attendance

### Daily Attendance
1. Click "Mark" button on Dashboard or navigate to Attendance page
2. Select the date (defaults to today)
3. For each class:
   - Click "Present" if you attended
   - Click "Absent" if you missed it
4. Your attendance is automatically saved and calculations updated

### Tips
- Mark attendance daily for accurate tracking
- Use the calendar to mark past dates if you forgot
- Check the dashboard regularly to monitor your status

## ⚙️ Settings & Configuration

### Upload New Timetable
1. Go to Settings
2. Find "Timetable" section
3. Click "Upload New Timetable"
4. Upload your new timetable
5. Subjects will be automatically updated

### Adjust Semester Settings
- Modify semester start/end dates
- Change required attendance percentage
- Update holiday schedules

### Manage Leave
- Add duty leave dates
- Add medical leave dates
- These dates won't negatively impact your attendance

### Export Data
- Click "Export Attendance Report" to download your records
- Useful for sharing with advisors or keeping personal records

### Reset Data
- Use "Reset All Data" to clear everything and start fresh
- **Warning**: This action cannot be undone!

## 🌓 Theme Switching

### Toggle Theme
- Click the sun/moon icon in the header
- Theme preference is automatically saved
- Works across all pages

### Theme Options
- **Light Mode**: Clean, bright interface
- **Dark Mode**: Easy on the eyes, great for night use
- **System**: Automatically matches your device preference

## 📱 Understanding Risk Levels

### Safe (Green)
- Attendance is well above required percentage
- You can afford to miss some classes
- "Can Bunk" shows how many classes you can skip

### Warning (Yellow)
- Attendance is close to required percentage
- Be cautious about missing classes
- Monitor closely

### High (Orange)
- Attendance is below required percentage
- Need to attend more classes
- "Must Attend" shows minimum classes needed

### Critical (Red)
- Attendance is significantly below required
- Urgent action needed
- Attend all upcoming classes

## 🎯 Pro Tips

### Stay on Track
1. Mark attendance daily - don't let it pile up
2. Check dashboard weekly to monitor trends
3. Plan ahead using "Can Bunk" / "Must Attend" indicators
4. Set reminders for classes you tend to miss

### Maximize the App
1. Upload accurate timetable for best results
2. Keep semester dates updated
3. Mark duty/medical leave properly
4. Use dark mode to save battery on mobile

### Troubleshooting
- **Subjects not showing?** Upload timetable again or check Settings
- **Wrong attendance?** You can manually adjust in subject details
- **Theme not changing?** Clear browser cache and try again
- **Data lost?** Check if you accidentally reset data

## 🔄 Updating Your Timetable

### Mid-Semester Changes
If your timetable changes mid-semester:

1. Go to Settings
2. Upload new timetable
3. Your existing attendance data will be preserved
4. New subjects will be added with 0 attendance
5. Removed subjects will be archived (data preserved in localStorage)

### Manual Subject Management
Currently, subjects are managed via timetable upload. For manual management:
- Edit `src/hooks/useAttendanceData.ts`
- Add functions for adding/editing/deleting individual subjects
- Update UI to include subject management interface

## 📊 Understanding Calculations

### Attendance Percentage
```
Attendance % = (Attended Classes / Total Classes) × 100
```

### Can Bunk
```
Maximum classes you can miss while staying above required %
```

### Must Attend
```
Minimum classes you must attend to reach required %
```

### Risk Status
- **Safe**: Attendance ≥ 80%
- **Warning**: 75% ≤ Attendance < 80%
- **High**: 70% ≤ Attendance < 75%
- **Critical**: Attendance < 70%

## 🚀 Next Steps

1. **Integrate Real OCR**: Follow [INTEGRATION_GUIDE.md](./INTEGRATION_GUIDE.md)
2. **Customize Theme**: Edit colors in `src/index.css`
3. **Add Features**: Check [FEATURES.md](./FEATURES.md) for enhancement ideas
4. **Deploy**: Use `npm run build` and deploy to your preferred platform

## 💡 Need Help?

- Check [FEATURES.md](./FEATURES.md) for detailed feature documentation
- See [INTEGRATION_GUIDE.md](./INTEGRATION_GUIDE.md) for OCR integration
- Review [README.md](./README.md) for technical details

## 🎉 You're All Set!

Start tracking your attendance and never worry about falling below the required percentage again!
