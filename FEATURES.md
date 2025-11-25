# New Features Added

## 1. Timetable Upload Functionality

### Overview
Users can now upload their weekly timetable as an image (PNG, JPG) or PDF file. The system will automatically parse and extract:
- Subject names
- Subject codes
- Teacher names
- Class schedules

### How It Works

#### During Onboarding
1. On the first step of onboarding, users can drag & drop or click to upload their timetable
2. The system processes the file and extracts subject information
3. Detected subjects are displayed with their details (name, code, teacher)
4. Users can proceed through the setup with their custom subjects

#### In Settings
1. Navigate to Settings page
2. Find the "Timetable" section
3. Click "Upload New Timetable" button
4. Upload your timetable file
5. The system will replace existing subjects with newly detected ones

### Technical Implementation
- **Component**: `TimetableUpload.tsx` - Reusable upload component with drag & drop
- **Parser**: `timetableParser.ts` - Handles file validation and parsing
- **Storage**: Subjects stored in localStorage under "attendance-data"
- **Schedule**: Class schedule stored under "timetable-schedule"

### File Requirements
- **Formats**: PNG, JPG, JPEG, PDF
- **Max Size**: 10MB
- **Content**: Should contain clear text with subject names, codes, and teacher names

### Current Implementation
The parser currently uses mock data for demonstration. To integrate real OCR:
1. Install an OCR library (e.g., `tesseract.js`)
2. Update `parseTimetableImage()` in `src/lib/timetableParser.ts`
3. Process the uploaded image and extract text
4. Parse the text to structure subject data

## 2. Dark/Light Theme Toggle

### Overview
Users can now switch between dark and light themes throughout the application.

### Features
- **System Default**: Automatically detects user's system preference
- **Manual Toggle**: Click the sun/moon icon to switch themes
- **Persistent**: Theme preference is saved and persists across sessions
- **Smooth Transitions**: Animated transitions between themes

### Where to Find It
The theme toggle button (sun/moon icon) is available in:
- Dashboard header (top right)
- Settings page header (top right)
- Attendance page header (top right)

### Technical Implementation
- **Library**: Uses `next-themes` (already installed)
- **Component**: `ThemeToggle.tsx` - Reusable theme toggle button
- **Provider**: `ThemeProvider` wraps the entire app in `App.tsx`
- **CSS**: Theme variables defined in `src/index.css`

### Theme Variables
All colors are defined using CSS custom properties in `src/index.css`:
- Light theme: Default colors
- Dark theme: `.dark` class overrides

## 3. Dynamic Subject Management

### Overview
The application now fully supports dynamic subject management based on uploaded timetables.

### Features
- **Auto-Import**: Subjects automatically imported from timetable
- **Flexible Count**: Support for any number of subjects
- **Data Persistence**: All subject data saved to localStorage
- **Reset Functionality**: Option to reset all data and start fresh

### API Updates
The `useAttendanceData` hook now includes:
- `setSubjects(subjects)` - Replace all subjects
- `resetAllData()` - Clear all data and reset to defaults

## Usage Examples

### Uploading a Timetable
```typescript
import { TimetableUpload } from "@/components/TimetableUpload";
import { ParsedTimetable } from "@/lib/timetableParser";

function MyComponent() {
  const handleUpload = (data: ParsedTimetable) => {
    console.log("Subjects:", data.subjects);
    console.log("Schedule:", data.schedule);
  };

  return <TimetableUpload onUploadComplete={handleUpload} />;
}
```

### Using Theme Toggle
```typescript
import { ThemeToggle } from "@/components/ThemeToggle";

function MyHeader() {
  return (
    <header>
      <h1>My App</h1>
      <ThemeToggle />
    </header>
  );
}
```

### Managing Subjects
```typescript
import { useAttendanceData } from "@/hooks/useAttendanceData";

function MyComponent() {
  const { subjects, setSubjects, resetAllData } = useAttendanceData();

  const addNewSubject = () => {
    const newSubject = {
      id: Date.now(),
      name: "New Subject",
      code: "NS101",
      teacher: "Dr. Smith",
      totalClasses: 0,
      attendedClasses: 0,
      requiredPercentage: 75,
    };
    setSubjects([...subjects, newSubject]);
  };

  return (
    <div>
      <button onClick={addNewSubject}>Add Subject</button>
      <button onClick={resetAllData}>Reset All</button>
    </div>
  );
}
```

## Future Enhancements

### Timetable Upload
- [ ] Integrate real OCR service (Tesseract.js, Google Vision API, etc.)
- [ ] Support for more file formats
- [ ] Manual editing of detected subjects
- [ ] Bulk import from CSV/Excel
- [ ] Schedule visualization

### Theme System
- [ ] Multiple theme options (not just dark/light)
- [ ] Custom color schemes
- [ ] Per-page theme preferences
- [ ] Theme preview before applying

### Subject Management
- [ ] Manual subject addition/editing
- [ ] Subject archiving
- [ ] Import/export functionality
- [ ] Subject categories/groups
- [ ] Custom required percentages per subject
