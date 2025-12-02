# Chennai Music Season 2025-26 Schedule Generator
## Detailed Specification for Claude Code

---

## PROJECT OVERVIEW

Create a comprehensive **Rasika's Ready Reckoner** for the Chennai Margazhi Music Season 2025-26. This should be a professional-quality schedule viewer that consolidates concerts from multiple sabhas into a single chronological view, allowing music lovers to plan their concert attendance efficiently.

---

## INPUT DATA

### Source Files (Already Available)
1. **Music Academy Schedule** - `/mnt/user-data/uploads/Madras_Music_Academy_Schedule.pdf`
   - Venue: TTK Auditorium, Music Academy
   - Dates: December 15, 2025 to January 1, 2026
   - 99th Annual Concerts

2. **Sri Parthasarathy Swami Sabha (SPSS)** - `/mnt/user-data/uploads/Sri_Pathasarathy_Sami_Sabha.pdf`
   - Venue: Vidya Bharathi, 55 Bheemasena Garden Road, Mylapore
   - Dates: December 16, 2025 to January 1, 2026
   - 125th Year Celebration
   - Note: Daily Lecture Demos at 8:30 AM; Admission free except 4 PM and 6:30 PM slots

### Future Additions (Design for Extensibility)
More sabha schedules will be added later:
- Narada Gana Sabha
- Brahma Gana Sabha
- Krishna Gana Sabha
- Mylapore Fine Arts
- Kartik Fine Arts
- Indian Fine Arts
- Nungambakkam Cultural Academy
- And others...

---

## OUTPUT REQUIREMENTS

### 1. HTML File (`chennai_music_season_2025_26.html`)

#### Design Principles
- **Mobile-responsive** - Many rasikas will check on phones between concerts
- **Print-friendly** - Include print stylesheet
- **Fast-loading** - Single HTML file with embedded CSS/JS (no external dependencies except CDN fonts)
- **Accessible** - Good contrast, readable fonts, proper semantic HTML

#### Header Section
- Title: "Chennai Music Season 2025-26 | Margazhi Utsavam"
- Subtitle: "A Rasika's Ready Reckoner"
- Date Range: December 15, 2025 – January 1, 2026
- Stats summary: Total days, Total sabhas, Total concerts, Total artists

#### Filter/Control Panel
- **Filter by Sabha**: All | Music Academy | SPSS | (future sabhas)
- **Filter by Genre**: All | Vocal | Violin | Veena | Flute | Nagaswaram | Chitraveena | Lecture Demo | Upanyasam | Harikatha | Special
- **Filter by Time Slot**: Morning (before 12 PM) | Afternoon (12-5 PM) | Evening (after 5 PM)
- **Search box**: Search by artist name
- **Date Jump**: Quick links to each date

#### Legend Section
- Color codes for each genre
- Color codes for each sabha/venue
- Icons if used

#### Main Schedule Display
Organized by DATE (primary grouping), then TIME (secondary sorting within each date)

For each date section:
```
┌─────────────────────────────────────────────────────────────┐
│  December 17, 2025                              Wednesday   │
├─────────────────────────────────────────────────────────────┤
│ TIME        │ VENUE    │ GENRE  │ ARTISTS                   │
├─────────────────────────────────────────────────────────────┤
│ 08:30 AM    │ SPSS     │ Lecture│ "Understanding Rare Ragas │
│             │          │        │ of Dikshitar" - Dr. Sriram│
│             │          │        │ Parasuram                 │
├─────────────────────────────────────────────────────────────┤
│ 09:00 AM    │ Academy  │ Vocal  │ Dr. Gayathri Girish       │
│ to 11:30 AM │          │        │ Dr. M. Narmadha (Violin)  │
│             │          │        │ Poongulam S. Subramanian  │
│             │          │        │ (Mridangam)               │
├─────────────────────────────────────────────────────────────┤
│ ... more events sorted by time ...                          │
└─────────────────────────────────────────────────────────────┘
```

#### Event Card Information
Each event should display:
1. **Time**: Start time prominently, end time smaller (if available)
2. **Venue/Sabha**: Color-coded badge (e.g., red for Academy, blue for SPSS)
3. **Genre**: Color-coded pill/badge
4. **Main Artist(s)**: Large, bold text - this is the headliner
5. **Accompanists**: Smaller text, formatted as:
   - Violin: Artist Name
   - Mridangam: Artist Name
   - Ghatam/Kanjira/Moharsing: Artist Name
6. **Special Notes**: (if any) - like "Ticketed", "Free Entry", etc.

#### Footer
- Last updated date
- Disclaimer: "For accurate timings, please verify with respective Sabhas"
- Credits/Source acknowledgment

#### Interactive Features (JavaScript)
1. **Filters**: Real-time filtering without page reload
2. **Search**: Instant search as user types
3. **Sticky date headers**: When scrolling, current date stays visible
4. **Print button**: Opens print dialog with print-optimized view
5. **Expand/Collapse**: Option to collapse past dates
6. **Local Storage**: Remember filter preferences

---

### 2. PDF File (`chennai_music_season_2025_26.pdf`)

#### Design Principles
- **A4 size**, portrait orientation
- **Printable**: Good margins, readable when printed in B&W
- **Compact but readable**: Fit more content per page while maintaining clarity

#### Structure
1. **Cover Page**
   - Title: Chennai Music Season 2025-26
   - Subtitle: Margazhi Utsavam - A Rasika's Ready Reckoner
   - Date Range
   - List of Sabhas included
   - Generated date

2. **Table of Contents**
   - Quick links to each date

3. **Daily Schedule Pages**
   - One or more pages per date depending on event count
   - Clear date header on each page
   - Table format with columns:
     | Time | Sabha | Genre | Main Artist | Accompanists |
   - Alternating row colors for readability
   - Page numbers

4. **Appendix: Venue Information**
   - Address and contact for each sabha
   - Map reference or landmark

---

## DATA STRUCTURE

### Event Object Schema
```python
{
    "date": "2025-12-17",           # ISO format YYYY-MM-DD
    "day": "Wednesday",              # Day name
    "time_start": "09:00 AM",        # 12-hour format with AM/PM
    "time_end": "11:30 AM",          # Optional - some events don't have end time
    "time_sort": 900,                # Minutes from midnight for sorting
    "venue": "Music Academy",        # Full venue name
    "venue_short": "Academy",        # Short code for display
    "venue_address": "TTK Auditorium, Royapettah", # Full address
    "genre": "Vocal",                # Genre category
    "main_artist": "Dr. Gayathri Girish",  # Headliner name(s)
    "accompanists": [                # List of accompanists with instruments
        {"name": "Dr. M. Narmadha", "instrument": "Violin"},
        {"name": "Poongulam S. Subramanian", "instrument": "Mridangam"},
        {"name": "M Gururaj", "instrument": "Moharsing"}
    ],
    "accompanists_text": "Dr. M. Narmadha (Violin), ...",  # Raw text version
    "is_ticketed": True,             # Whether paid entry
    "special_notes": "",             # Any special notes
    "sabha_id": "academy"            # Unique sabha identifier
}
```

### Genre Categories
Standardize to these categories:
- **Vocal** - Solo or duet vocal concerts
- **Violin** - Violin solo or duet
- **Veena** - Veena/Saraswathi Veena concerts
- **Flute** - Flute concerts
- **Nagaswaram** - Nagaswaram with Thavil
- **Chitraveena** - Chitraveena/Gottuvadhyam
- **Lecture** - Lecture Demonstrations
- **Upanyasam** - Spiritual discourses, Kalakshepam
- **Harikatha** - Harikatha performances
- **Special** - Ensemble, Jugalbandi, Inauguration, Sadas, etc.
- **Bhakti Sangeet** - Devotional music concerts

### Sabha/Venue Codes
```python
SABHAS = {
    "academy": {
        "name": "Music Academy",
        "short": "Academy",
        "color": "#E74C3C",  # Red
        "address": "TTK Auditorium, 306 TTK Road, Royapettah, Chennai - 14",
        "phone": "044-28112231"
    },
    "spss": {
        "name": "Sri Parthasarathy Swami Sabha",
        "short": "SPSS", 
        "color": "#3498DB",  # Blue
        "address": "Vidya Bharathi, 55 Bheemasena Garden Road, Mylapore, Chennai - 4",
        "phone": "044-24997269"
    }
    # Add more sabhas here later
}
```

---

## PARSING GUIDELINES

### Music Academy PDF Parsing
- Date format: "Mon Dec 15th, 2025"
- Time format: "09:00 AM to 11:30 AM" or just "05:00 PM"
- Artists listed with instruments in parentheses
- Identify genre from instrument mentioned or default to Vocal

### SPSS PDF Parsing  
- Date format: "17-12-2025 (Wednesday)"
- Time format: "8.30 a.m." or "10.00 a.m."
- Lecture demos always at 8:30 AM
- Artists separated by " – " (en-dash)
- Instruments in parentheses
- UPPERCASE names indicate senior/featured artists
- Note: "Admission Free except 4.00 p.m. and 6 p.m." - mark those as ticketed

### Artist Name Standardization
- Preserve honorifics: "Dr.", "Sangita Kalanidhi", "Vid.", "Smt.", "Sri."
- Keep location prefixes: "Trivandrum", "Delhi", "Madurai", etc.
- Standardize instrument names:
  - Mridangam/Mrudangam → Mridangam
  - Morsing/Moharsing → Morsing
  - Kanjira/Khanjira → Kanjira

---

## COLOR SCHEME

### Sabha Colors
- Music Academy: `#E74C3C` (Red) with `#FADBD8` (Light red bg)
- SPSS: `#3498DB` (Blue) with `#D4E6F1` (Light blue bg)
- (Reserve colors for future sabhas)

### Genre Colors
- Vocal: `#9B59B6` (Purple)
- Violin: `#E67E22` (Orange)
- Veena: `#27AE60` (Green)
- Flute: `#16A085` (Teal)
- Nagaswaram: `#C0392B` (Dark Red)
- Chitraveena: `#8E44AD` (Deep Purple)
- Lecture: `#7F8C8D` (Gray)
- Upanyasam: `#2980B9` (Blue)
- Harikatha: `#D35400` (Dark Orange)
- Special: `#F39C12` (Gold)

### Background
- Main: Gradient from `#1a1a2e` to `#0f3460` (Dark theme)
- Cards: White `#FFFFFF`
- Date headers: `#2C3E50` to `#34495E`

---

## TECHNICAL REQUIREMENTS

### Python Libraries to Use
```python
# For PDF parsing (if needed to re-parse)
import pdfplumber  # or pypdf

# For HTML generation
# Pure string formatting or Jinja2 templates

# For PDF generation
from reportlab.lib.pagesizes import A4
from reportlab.platypus import SimpleDocTemplate, Table, Paragraph
from reportlab.lib.styles import getSampleStyleSheet
```

### File Output Locations
- HTML: `/mnt/user-data/outputs/chennai_music_season_2025_26.html`
- PDF: `/mnt/user-data/outputs/chennai_music_season_2025_26.pdf`

---

## SAMPLE OUTPUT PREVIEW

### HTML Preview (One Event Card)
```
┌────────────────────────────────────────────────────────────────┐
│ ┌──────────┐  ┌─────────┐  ┌────────┐                         │
│ │ 09:00 AM │  │ Academy │  │ Vocal  │                         │
│ │ to       │  │   🔴    │  │   🟣   │                         │
│ │ 11:30 AM │  └─────────┘  └────────┘                         │
│ └──────────┘                                                   │
│                                                                │
│  Dr. Gayathri Girish                                          │
│                                                                │
│  Violin: Dr. M. Narmadha                                      │
│  Mridangam: Poongulam S. Subramanian                          │
│  Morsing: M Gururaj                                           │
└────────────────────────────────────────────────────────────────┘
```

---

## EXECUTION STEPS

1. **Parse both PDF files** and extract all events into the standard data structure
2. **Combine all events** into a single list
3. **Sort events** by date (primary) and time (secondary)
4. **Generate HTML file** with all styling and JavaScript embedded
5. **Generate PDF file** with proper pagination and formatting
6. **Save both files** to `/mnt/user-data/outputs/`
7. **Provide download links** to the user

---

## TESTING CHECKLIST

- [ ] All dates from Dec 15, 2025 to Jan 1, 2026 are covered
- [ ] Events are in correct chronological order
- [ ] No duplicate events
- [ ] All artist names are readable
- [ ] Genre colors are distinct
- [ ] Sabha colors are distinct
- [ ] Filters work correctly in HTML
- [ ] Search works correctly
- [ ] Print view is clean
- [ ] PDF is properly paginated
- [ ] PDF is readable in black & white

---

## FUTURE ENHANCEMENTS (Nice to Have)

1. **Artist Index** - Alphabetical list of all artists with their concert dates
2. **Conflict Highlighter** - Show when same-time concerts exist at different venues
3. **Personal Planner** - Let user mark "interested" concerts (using localStorage)
4. **Export to Calendar** - Generate .ics file for Google/Apple Calendar
5. **Distance Calculator** - Show travel time between venues

---

## NOTES FOR DEVELOPER

- The PDFs are already uploaded and parsed - data is available
- Prioritize getting a working version first, then refine styling
- Test with print preview to ensure PDF-like output
- Keep the code modular so adding new sabhas is easy
- Comment the code well for future maintenance

---

**END OF SPECIFICATION**
