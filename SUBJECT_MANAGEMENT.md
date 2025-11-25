# Subject Management Guide

## ✨ New Feature: Manage Subjects

You can now **add, edit, and remove subjects** directly from the Settings page!

## 🎯 Features

### 1. View All Subjects
- See all your subjects in one place
- View attendance stats for each subject
- See subject code, teacher, and attendance percentage

### 2. Add New Subject
- Click "Add New Subject" button
- Fill in:
  - Subject Name (e.g., "Data Structures")
  - Subject Code (e.g., "CS201")
  - Teacher Name (e.g., "Dr. Smith")
  - Required Percentage (default: 75%)
- Click "Add Subject"

### 3. Edit Subject
- Click the edit icon (pencil) on any subject
- Modify any field:
  - Name
  - Code
  - Teacher
  - Required percentage
- Click "Save" to confirm or "Cancel" to discard

### 4. Remove Subject
- Click the delete icon (trash) on any subject
- Confirm deletion in the dialog
- **Warning**: This will delete all attendance data for that subject!

### 5. Upload Timetable
- Click "Upload Timetable" button
- Upload image or use manual entry
- This will **replace all existing subjects**

## 📍 How to Access

1. Open the app: http://localhost:8080
2. Click the Settings icon (gear) in the top right
3. Scroll to "Manage Subjects" section

## 🎨 UI Features

### Subject Card Shows:
- ✅ Subject name (bold)
- ✅ Subject code and teacher
- ✅ Attendance stats (X/Y classes attended)
- ✅ Attendance percentage
- ✅ Edit button
- ✅ Delete button

### Add/Edit Form:
- Clean, organized layout
- Validation for required fields
- Cancel option
- Success notifications

### Delete Confirmation:
- Alert dialog to prevent accidents
- Shows subject name
- Warns about data loss
- Cancel or confirm options

## 💡 Use Cases

### Use Case 1: Add a New Subject Mid-Semester
```
1. Go to Settings → Manage Subjects
2. Click "Add New Subject"
3. Fill in details
4. Click "Add Subject"
5. Subject appears in dashboard
```

### Use Case 2: Fix a Typo in Subject Name
```
1. Go to Settings → Manage Subjects
2. Click edit icon on the subject
3. Fix the name
4. Click "Save"
5. Updated everywhere
```

### Use Case 3: Remove a Dropped Subject
```
1. Go to Settings → Manage Subjects
2. Click delete icon on the subject
3. Confirm deletion
4. Subject removed from dashboard
```

### Use Case 4: Change Teacher Name
```
1. Go to Settings → Manage Subjects
2. Click edit icon
3. Update teacher name
4. Click "Save"
```

## ⚠️ Important Notes

### Data Persistence
- All changes are saved to localStorage immediately
- If using the backend, changes sync to database
- No manual save needed

### Deleting Subjects
- **Permanent action** - cannot be undone
- Deletes all attendance records for that subject
- Confirmation dialog prevents accidents

### Editing Subjects
- Changes apply immediately
- Attendance data is preserved
- Only metadata (name, code, teacher) changes

### Adding Subjects
- Starts with 0 attendance
- Can mark attendance from today onwards
- Appears in dashboard immediately

## 🔄 Integration with Backend

If using the full-stack version:

### Add Subject
```typescript
POST /api/subjects
{
  "name": "New Subject",
  "code": "CS301",
  "teacher": "Dr. Jones",
  "requiredPercentage": 75,
  "semesterId": "xxx"
}
```

### Update Subject
```typescript
PUT /api/subjects/:id
{
  "name": "Updated Name",
  "teacher": "New Teacher"
}
```

### Delete Subject
```typescript
DELETE /api/subjects/:id
```

## 🎓 Tips

1. **Regular Review**: Check your subjects list regularly
2. **Fix Typos Early**: Edit subjects as soon as you notice errors
3. **Be Careful Deleting**: Double-check before removing subjects
4. **Use Descriptive Names**: Make subjects easy to identify
5. **Keep Teacher Names Updated**: Helps with organization

## 🐛 Troubleshooting

### Subject Not Appearing?
- Refresh the page
- Check if it was added successfully (toast notification)
- Check browser console for errors

### Can't Delete Subject?
- Make sure you're clicking the correct delete button
- Check if confirmation dialog appears
- Try refreshing and deleting again

### Changes Not Saving?
- Check localStorage is enabled
- Check browser console for errors
- Try clearing cache and reloading

## 📊 Example Workflow

**Scenario**: Starting a new semester with 6 subjects

1. **Setup**:
   - Go to Settings → Manage Subjects
   - Click "Add New Subject" 6 times
   - Fill in each subject's details

2. **Mid-Semester**:
   - One subject dropped → Delete it
   - Teacher changed → Edit subject
   - New subject added → Add new subject

3. **End of Semester**:
   - Review all subjects
   - Export attendance data
   - Prepare for next semester

## 🎉 Benefits

✅ **Flexibility**: Add/remove subjects anytime
✅ **Control**: Edit any subject detail
✅ **Safety**: Confirmation dialogs prevent mistakes
✅ **Convenience**: All in one place
✅ **Real-time**: Changes apply immediately
✅ **User-friendly**: Clean, intuitive interface

---

**Now you have complete control over your subjects!** 🎓

Go to Settings → Manage Subjects to try it out!
