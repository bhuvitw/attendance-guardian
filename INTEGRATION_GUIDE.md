# Integration Guide for Real OCR

## Current State
The timetable upload feature currently uses mock data for demonstration. To integrate real OCR functionality, follow this guide.

## Option 1: Tesseract.js (Client-Side OCR)

### Installation
```bash
npm install tesseract.js
```

### Implementation
Update `src/lib/timetableParser.ts`:

```typescript
import Tesseract from 'tesseract.js';

export async function parseTimetableImage(file: File): Promise<ParsedTimetable> {
  try {
    // Convert file to image URL
    const imageUrl = URL.createObjectURL(file);
    
    // Perform OCR
    const { data: { text } } = await Tesseract.recognize(
      imageUrl,
      'eng',
      {
        logger: (m) => console.log(m), // Optional: progress logging
      }
    );
    
    // Clean up
    URL.revokeObjectURL(imageUrl);
    
    // Parse the extracted text
    const subjects = parseTextToSubjects(text);
    const schedule = parseTextToSchedule(text);
    
    return { subjects, schedule };
  } catch (error) {
    console.error('OCR Error:', error);
    throw new Error('Failed to parse timetable');
  }
}

function parseTextToSubjects(text: string): Omit<Subject, "id" | "totalClasses" | "attendedClasses">[] {
  // Implement your parsing logic based on your timetable format
  // Example: Look for patterns like "CS201 - Data Structures - Dr. Smith"
  
  const subjects: Omit<Subject, "id" | "totalClasses" | "attendedClasses">[] = [];
  const lines = text.split('\n');
  
  for (const line of lines) {
    // Example regex pattern - adjust based on your format
    const match = line.match(/([A-Z]{2}\d{3})\s*-\s*([^-]+)\s*-\s*(.+)/);
    if (match) {
      subjects.push({
        code: match[1].trim(),
        name: match[2].trim(),
        teacher: match[3].trim(),
        requiredPercentage: 75,
      });
    }
  }
  
  return subjects;
}

function parseTextToSchedule(text: string): TimetableSlot[] {
  // Implement schedule parsing logic
  // Look for day names, time slots, and subject codes
  
  const schedule: TimetableSlot[] = [];
  // Your parsing logic here
  
  return schedule;
}
```

### Pros
- No backend required
- Works offline
- Free and open source

### Cons
- Slower processing
- Less accurate than cloud services
- Larger bundle size

## Option 2: Google Cloud Vision API (Cloud-Based OCR)

### Setup
1. Create a Google Cloud project
2. Enable Cloud Vision API
3. Create API credentials
4. Install the client library:

```bash
npm install @google-cloud/vision
```

### Backend Implementation (Node.js/Express)
Create an API endpoint:

```javascript
// server.js
const vision = require('@google-cloud/vision');
const express = require('express');
const multer = require('multer');

const app = express();
const upload = multer({ storage: multer.memoryStorage() });
const client = new vision.ImageAnnotatorClient();

app.post('/api/parse-timetable', upload.single('timetable'), async (req, res) => {
  try {
    const [result] = await client.textDetection(req.file.buffer);
    const text = result.fullTextAnnotation.text;
    
    // Parse the text and return structured data
    const parsedData = parseTextToTimetable(text);
    res.json(parsedData);
  } catch (error) {
    res.status(500).json({ error: 'Failed to parse timetable' });
  }
});
```

### Frontend Implementation
Update `src/lib/timetableParser.ts`:

```typescript
export async function parseTimetableImage(file: File): Promise<ParsedTimetable> {
  const formData = new FormData();
  formData.append('timetable', file);
  
  const response = await fetch('/api/parse-timetable', {
    method: 'POST',
    body: formData,
  });
  
  if (!response.ok) {
    throw new Error('Failed to parse timetable');
  }
  
  return await response.json();
}
```

### Pros
- High accuracy
- Fast processing
- Handles complex layouts

### Cons
- Requires backend
- Costs money (free tier available)
- Needs internet connection

## Option 3: Azure Computer Vision

### Setup
1. Create Azure account
2. Create Computer Vision resource
3. Get API key and endpoint

```bash
npm install @azure/cognitiveservices-computervision
```

### Implementation
Similar to Google Cloud Vision, but using Azure SDK.

## Option 4: AWS Textract

### Setup
1. Create AWS account
2. Set up Textract service
3. Configure credentials

```bash
npm install @aws-sdk/client-textract
```

### Implementation
Use AWS SDK to send images and receive structured text.

## Recommended Approach

For a production app, I recommend:

1. **Start with Tesseract.js** for MVP/testing
2. **Upgrade to Cloud Vision** for production if accuracy is critical
3. **Add manual editing** as a fallback for incorrect detections

## Testing Your OCR Integration

Create test cases with various timetable formats:

```typescript
// src/lib/__tests__/timetableParser.test.ts
import { parseTimetableImage } from '../timetableParser';

describe('Timetable Parser', () => {
  it('should parse a standard timetable', async () => {
    const file = new File(['test'], 'timetable.png', { type: 'image/png' });
    const result = await parseTimetableImage(file);
    
    expect(result.subjects).toHaveLength(5);
    expect(result.subjects[0]).toHaveProperty('name');
    expect(result.subjects[0]).toHaveProperty('code');
    expect(result.subjects[0]).toHaveProperty('teacher');
  });
});
```

## Fallback Strategy

Always provide a way for users to manually edit detected subjects:

```typescript
// Add to TimetableUpload component
const [editMode, setEditMode] = useState(false);
const [editedSubjects, setEditedSubjects] = useState<Subject[]>([]);

// Allow users to correct OCR mistakes
```

## Environment Variables

Store API keys securely:

```env
# .env
VITE_GOOGLE_VISION_API_KEY=your_key_here
VITE_AZURE_VISION_ENDPOINT=your_endpoint_here
```

Access in code:
```typescript
const apiKey = import.meta.env.VITE_GOOGLE_VISION_API_KEY;
```

## Performance Optimization

1. **Show progress**: Display upload and processing progress
2. **Compress images**: Reduce file size before sending to OCR
3. **Cache results**: Store parsed data to avoid re-processing
4. **Batch processing**: If multiple pages, process in parallel

## Error Handling

```typescript
try {
  const result = await parseTimetableImage(file);
  onUploadComplete(result);
} catch (error) {
  if (error.message.includes('rate limit')) {
    toast.error('Too many requests. Please try again later.');
  } else if (error.message.includes('invalid format')) {
    toast.error('Unable to read timetable. Please try a clearer image.');
  } else {
    toast.error('Failed to parse timetable. Please try again.');
  }
}
```
