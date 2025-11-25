# Attendance Guardian

A smart attendance tracking application that helps students monitor their attendance, predict risks, and manage their academic schedule.

## ✨ Features

### 📊 Attendance Tracking
- Track attendance for multiple subjects
- Real-time attendance percentage calculation
- Visual risk indicators (Safe, Warning, High, Critical)
- Calculate how many classes you can bunk or must attend

### 📅 Timetable Upload
- Upload your weekly timetable as an image (PNG, JPG) or PDF
- Automatic subject extraction with OCR (ready for integration)
- Dynamic subject management based on your timetable
- Store and manage class schedules

### 🌓 Dark/Light Theme
- Toggle between dark and light themes
- System preference detection
- Smooth theme transitions
- Persistent theme selection

### 📈 Smart Analytics
- Average attendance across all subjects
- Risk meter visualization
- Subject-wise detailed statistics
- Attendance predictions

## Project info

**URL**: https://lovable.dev/projects/f17b8f73-ac3a-48ff-8b82-eb4c36a541c1

## How can I edit this code?

There are several ways of editing your application.

**Use Lovable**

Simply visit the [Lovable Project](https://lovable.dev/projects/f17b8f73-ac3a-48ff-8b82-eb4c36a541c1) and start prompting.

Changes made via Lovable will be committed automatically to this repo.

**Use your preferred IDE**

If you want to work locally using your own IDE, you can clone this repo and push changes. Pushed changes will also be reflected in Lovable.

The only requirement is having Node.js & npm installed - [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating)

Follow these steps:

```sh
# Step 1: Clone the repository using the project's Git URL.
git clone <YOUR_GIT_URL>

# Step 2: Navigate to the project directory.
cd <YOUR_PROJECT_NAME>

# Step 3: Install the necessary dependencies.
npm i

# Step 4: Start the development server with auto-reloading and an instant preview.
npm run dev
```

**Edit a file directly in GitHub**

- Navigate to the desired file(s).
- Click the "Edit" button (pencil icon) at the top right of the file view.
- Make your changes and commit the changes.

**Use GitHub Codespaces**

- Navigate to the main page of your repository.
- Click on the "Code" button (green button) near the top right.
- Select the "Codespaces" tab.
- Click on "New codespace" to launch a new Codespace environment.
- Edit files directly within the Codespace and commit and push your changes once you're done.

## What technologies are used for this project?

This project is built with:

- **Vite** - Fast build tool and dev server
- **TypeScript** - Type-safe JavaScript
- **React** - UI library
- **shadcn-ui** - Beautiful component library
- **Tailwind CSS** - Utility-first CSS framework
- **next-themes** - Theme management
- **React Router** - Client-side routing
- **date-fns** - Date manipulation
- **Sonner** - Toast notifications
- **Lucide React** - Icon library

## 📚 Documentation

- **[FEATURES.md](./FEATURES.md)** - Detailed feature documentation
- **[INTEGRATION_GUIDE.md](./INTEGRATION_GUIDE.md)** - Guide for integrating real OCR

## 🚀 Quick Start

### Prerequisites
- Node.js (v16 or higher)
- npm or yarn

### Installation

```sh
# Clone the repository
git clone <YOUR_GIT_URL>

# Navigate to project directory
cd <YOUR_PROJECT_NAME>

# Install dependencies
npm install

# Start development server
npm run dev
```

### Build for Production

```sh
npm run build
```

### Preview Production Build

```sh
npm run preview
```

## 📱 Usage

### First Time Setup
1. Launch the app and complete the onboarding process
2. Upload your timetable (or skip to use default subjects)
3. Set your semester dates and holidays
4. Configure leave rules

### Daily Use
1. Mark attendance for each class
2. View your dashboard for attendance overview
3. Check individual subject details
4. Monitor risk levels and take action

### Settings
- Upload new timetable to update subjects
- Adjust semester settings
- Manage holidays and leave dates
- Toggle between dark/light theme
- Export attendance reports
- Reset all data if needed

## 🎨 Theme Customization

The app supports full theme customization. Edit `src/index.css` to modify:
- Color schemes
- Gradients
- Shadows
- Border radius
- Typography

## 🔧 Configuration

### Environment Variables
Create a `.env` file for API keys (when integrating OCR):

```env
VITE_GOOGLE_VISION_API_KEY=your_key_here
VITE_AZURE_VISION_ENDPOINT=your_endpoint_here
```

### Local Storage Keys
- `attendance-data` - Subject and attendance data
- `timetable-schedule` - Class schedule information
- `onboarded` - Onboarding completion status
- `theme` - User's theme preference

## How can I deploy this project?

Simply open [Lovable](https://lovable.dev/projects/f17b8f73-ac3a-48ff-8b82-eb4c36a541c1) and click on Share -> Publish.

## Can I connect a custom domain to my Lovable project?

Yes, you can!

To connect a domain, navigate to Project > Settings > Domains and click Connect Domain.

Read more here: [Setting up a custom domain](https://docs.lovable.dev/features/custom-domain#custom-domain)
