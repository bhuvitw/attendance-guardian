# Testing Checklist

Use this checklist to verify all new features are working correctly.

## 🚀 Initial Setup

- [ ] Clone/pull latest code
- [ ] Run `npm install`
- [ ] Run `npm run dev`
- [ ] App opens at `http://localhost:5173`
- [ ] No console errors on load

## 📤 Timetable Upload - Onboarding

### Step 1: Upload Timetable
- [ ] Onboarding screen appears on first visit
- [ ] Upload area is visible
- [ ] Can click to select file
- [ ] File picker opens with correct filters (PNG, JPG, PDF)
- [ ] Can drag and drop a file
- [ ] Border highlights on drag over
- [ ] File validation works (try invalid file type)
- [ ] File size validation works (try > 10MB file)
- [ ] Upload shows progress indicator
- [ ] Success state shows checkmark
- [ ] Detected subjects appear below upload
- [ ] Subject details show (name, code, teacher)
- [ ] Continue button is disabled until upload completes
- [ ] Continue button enables after successful upload
- [ ] Can proceed to Step 2

### Complete Onboarding
- [ ] Can complete all 4 steps
- [ ] Finish button works
- [ ] Redirects to Dashboard
- [ ] Subjects from upload appear on Dashboard

## 📤 Timetable Upload - Settings

### Access Settings
- [ ] Navigate to Settings page
- [ ] Timetable section is visible
- [ ] Shows current subject count
- [ ] "Upload New Timetable" button present

### Upload New Timetable
- [ ] Click "Upload New Timetable"
- [ ] Dialog opens
- [ ] Upload component works same as onboarding
- [ ] Can upload file
- [ ] Success message appears
- [ ] Dialog closes after upload
- [ ] Subject count updates
- [ ] Navigate to Dashboard
- [ ] New subjects appear on Dashboard
- [ ] Old attendance data preserved (if applicable)

### Error Handling
- [ ] Try uploading wrong file type → Error message
- [ ] Try uploading too large file → Error message
- [ ] Cancel upload → Dialog closes properly

## 🌓 Theme Toggle - Dashboard

### Initial State
- [ ] Theme toggle button visible in header
- [ ] Shows sun icon (light mode) or moon icon (dark mode)
- [ ] Matches system preference on first load

### Toggle Theme
- [ ] Click theme toggle
- [ ] Theme changes instantly
- [ ] Icon animates (rotates/fades)
- [ ] All colors update
- [ ] Cards update
- [ ] Text updates
- [ ] Borders update
- [ ] No flash or flicker

### Persistence
- [ ] Refresh page
- [ ] Theme persists
- [ ] Toggle again
- [ ] Refresh again
- [ ] New theme persists

## 🌓 Theme Toggle - Other Pages

### Settings Page
- [ ] Navigate to Settings
- [ ] Theme toggle visible
- [ ] Click toggle
- [ ] Theme changes
- [ ] All elements update correctly

### Attendance Page
- [ ] Navigate to Attendance
- [ ] Theme toggle visible
- [ ] Click toggle
- [ ] Theme changes
- [ ] Calendar updates correctly
- [ ] Class cards update correctly

### Subjects Page
- [ ] Navigate to Subjects (if applicable)
- [ ] Theme toggle visible
- [ ] Click toggle
- [ ] Theme changes

## 📊 Dynamic Subjects

### Subject Display
- [ ] Dashboard shows all uploaded subjects
- [ ] Subject cards display correctly
- [ ] Can click on subject cards
- [ ] Subject detail page works

### Subject Count
- [ ] Upload timetable with 5 subjects → Shows 5
- [ ] Upload timetable with 3 subjects → Shows 3
- [ ] Upload timetable with 10 subjects → Shows 10
- [ ] All subjects display properly

### Data Persistence
- [ ] Mark attendance for a subject
- [ ] Upload new timetable
- [ ] Check if attendance data handled correctly
- [ ] Navigate away and back
- [ ] Data persists

## 🗑️ Reset Functionality

### Reset All Data
- [ ] Navigate to Settings
- [ ] Scroll to Danger Zone
- [ ] Click "Reset All Data"
- [ ] Confirmation dialog appears
- [ ] Cancel → Nothing happens
- [ ] Confirm → Data resets
- [ ] Success message appears
- [ ] Subjects reset to defaults
- [ ] Attendance data cleared
- [ ] Onboarding status reset (optional test)

## 📱 Responsive Design

### Desktop (> 1024px)
- [ ] All features visible
- [ ] Theme toggle in header
- [ ] Upload dialog centered
- [ ] Subject cards in grid
- [ ] No layout issues

### Tablet (768px - 1024px)
- [ ] Layout adjusts properly
- [ ] Theme toggle accessible
- [ ] Upload dialog responsive
- [ ] Subject cards stack appropriately

### Mobile (< 768px)
- [ ] All features accessible
- [ ] Theme toggle visible
- [ ] Upload dialog full width
- [ ] Subject cards stack vertically
- [ ] Touch targets large enough
- [ ] No horizontal scroll

## 🎨 Visual Quality

### Light Theme
- [ ] Colors look good
- [ ] Contrast is sufficient
- [ ] Text is readable
- [ ] Cards have proper shadows
- [ ] Borders are visible

### Dark Theme
- [ ] Colors look good
- [ ] Contrast is sufficient
- [ ] Text is readable
- [ ] Cards stand out
- [ ] No harsh whites

### Transitions
- [ ] Theme switch is smooth
- [ ] No jarring changes
- [ ] Icons animate nicely
- [ ] Upload states transition well

## 🔧 Edge Cases

### Upload Edge Cases
- [ ] Upload same file twice → Works
- [ ] Upload different file → Replaces subjects
- [ ] Upload during onboarding, skip, then upload in settings → Works
- [ ] Upload with no subjects detected → Handles gracefully

### Theme Edge Cases
- [ ] Toggle rapidly → No issues
- [ ] Toggle while page loading → Works
- [ ] Toggle on different pages → Consistent
- [ ] System theme changes → App responds (if applicable)

### Data Edge Cases
- [ ] No subjects → Shows empty state
- [ ] Many subjects (10+) → Scrolls properly
- [ ] Reset with no data → Works
- [ ] Reset then upload → Works

## 🚨 Error Scenarios

### Upload Errors
- [ ] Network error (if using real OCR) → Shows error
- [ ] Invalid file → Shows error message
- [ ] Corrupted file → Handles gracefully
- [ ] Cancel during upload → Cleans up properly

### Theme Errors
- [ ] localStorage disabled → Falls back to default
- [ ] Invalid theme value → Uses default
- [ ] Theme provider missing → Graceful degradation

### Data Errors
- [ ] Corrupted localStorage → Resets to defaults
- [ ] Invalid subject data → Validates and fixes
- [ ] Missing required fields → Uses defaults

## 🔍 Browser Compatibility

### Chrome
- [ ] All features work
- [ ] Theme toggle works
- [ ] Upload works
- [ ] No console errors

### Firefox
- [ ] All features work
- [ ] Theme toggle works
- [ ] Upload works
- [ ] No console errors

### Safari
- [ ] All features work
- [ ] Theme toggle works
- [ ] Upload works
- [ ] No console errors

### Edge
- [ ] All features work
- [ ] Theme toggle works
- [ ] Upload works
- [ ] No console errors

## 📊 Performance

### Load Time
- [ ] Initial load < 3 seconds
- [ ] Theme switch instant
- [ ] Upload feedback immediate
- [ ] Page transitions smooth

### Memory
- [ ] No memory leaks
- [ ] Upload cleans up properly
- [ ] Theme switch doesn't leak
- [ ] Navigation doesn't accumulate memory

### Bundle Size
- [ ] Build completes successfully
- [ ] Bundle size reasonable (~850KB)
- [ ] Gzipped size acceptable (~250KB)
- [ ] No unnecessary dependencies

## 🎯 User Experience

### Onboarding Flow
- [ ] Clear instructions
- [ ] Progress indicator works
- [ ] Can go back/forward
- [ ] Can complete successfully
- [ ] Feels smooth and intuitive

### Daily Usage
- [ ] Easy to mark attendance
- [ ] Easy to toggle theme
- [ ] Easy to view subjects
- [ ] Easy to navigate

### Settings
- [ ] Easy to find upload
- [ ] Easy to reset data
- [ ] Clear what each setting does
- [ ] Changes take effect immediately

## 📝 Documentation

### Code Documentation
- [ ] Components have comments
- [ ] Functions are documented
- [ ] Types are clear
- [ ] No TODO comments left

### User Documentation
- [ ] README is updated
- [ ] FEATURES.md is complete
- [ ] QUICK_START.md is helpful
- [ ] INTEGRATION_GUIDE.md is clear

## ✅ Final Checks

### Build
- [ ] `npm run build` succeeds
- [ ] No TypeScript errors
- [ ] No linting errors
- [ ] Build output looks correct

### Production
- [ ] `npm run preview` works
- [ ] Production build functions correctly
- [ ] All features work in production
- [ ] No console errors in production

### Git
- [ ] All files committed
- [ ] Commit messages clear
- [ ] No sensitive data in commits
- [ ] Branch is clean

## 🎉 Sign Off

- [ ] All critical features tested
- [ ] All major browsers tested
- [ ] Documentation reviewed
- [ ] Ready for production

---

## 📋 Test Results

**Date Tested**: _______________

**Tested By**: _______________

**Browser**: _______________

**Device**: _______________

**Issues Found**: 
- 
- 
- 

**Overall Status**: ⬜ Pass  ⬜ Fail  ⬜ Needs Review

**Notes**:
_______________________________________________
_______________________________________________
_______________________________________________

---

## 🐛 Bug Report Template

If you find issues, use this template:

**Bug Title**: 

**Steps to Reproduce**:
1. 
2. 
3. 

**Expected Behavior**:

**Actual Behavior**:

**Screenshots**: (if applicable)

**Browser/Device**:

**Console Errors**: (if any)

---

## ✨ Feature Request Template

For improvements:

**Feature**: 

**Use Case**:

**Proposed Solution**:

**Priority**: ⬜ High  ⬜ Medium  ⬜ Low
