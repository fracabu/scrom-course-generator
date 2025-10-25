# Moodle Course Import Guide

## Overview

This guide explains how to import the generated Moodle course backup into your Moodle installation.

## Generated Files

### Main Output File
- **AI-Principianti-backup.mbz** (233 KB)
  - This is the complete Moodle backup package ready for import
  - Compatible with Moodle 4.x
  - Contains all course content, activities, and structure

### Alternative XML Files (for reference)
- **moodle-backup.xml** - Standalone XML backup structure
- **moodle-course.xml** - Course definition XML

### Development Files
- **generate_moodle_xml.py** - Initial XML generator script
- **generate_complete_moodle_backup.py** - Complete backup generator
- **moodle_backup/** - Extracted backup directory structure

---

## Course Information

**Course Name:** Introduzione all'Intelligenza Artificiale per Principianti
**Short Name:** AI-Principianti
**Category:** Technology / AI
**Format:** Topics (10 sections)

**Summary:**
Corso introduttivo all'intelligenza artificiale per principianti. Impara le nozioni base dell'AI per farne un uso razionale ed efficiente.

---

## Course Structure

The course includes **7 modules** (parsed from the content file) with content distributed across **10 sections**:

### Module 1: Cos'è l'Intelligenza Artificiale
- Introduction label
- 5 page activities covering definitions, history, AI types, and applications
- 1 quiz activity

### Module 2: Come Funziona l'Intelligenza Artificiale
- Introduction label
- 4 page activities on data, algorithms, training, and inference
- 2 assignment activities

### Module 3: Tipi di Intelligenza Artificiale e Machine Learning
- Introduction label
- 6 page activities covering different learning types
- 1 quiz activity
- 3 assignment activities (includes embedded content for Modules 4-6)

### Module 7: Etica e Responsabilità nell'AI
- Introduction label
- 6 page activities on bias, privacy, transparency, impact, and regulations
- 2 forum activities for discussion

### Module 8: AI e Dati: Privacy, Sicurezza e Qualità
- Introduction label
- 6 page activities on data quality, GDPR, security, and open data
- 1 quiz activity
- 1 assignment activity

### Module 9: Strumenti e Piattaforme AI per Tutti
- Introduction label
- 6 page activities on AI tools and platforms
- 1 forum activity
- 1 assignment activity (hands-on lab)

### Module 10: Il Futuro dell'AI e Come Continuare ad Imparare
- Introduction label
- 6 page activities on future trends and learning paths
- 1 forum activity

---

## Activity Statistics

**Total Activities Created:** 60

**Breakdown by Type:**
- **Page Activities:** 39 (theoretical content, explanations, summaries)
- **Assignment Activities:** 7 (practical exercises and projects)
- **Forum Activities:** 4 (discussions and collaborative activities)
- **Quiz Activities:** 3 (assessments and knowledge checks)
- **Label Resources:** 7 (section introductions)

---

## How to Import into Moodle

### Step 1: Access Course Restoration
1. Log in to your Moodle site as an administrator or teacher
2. Navigate to **Site administration** > **Courses** > **Restore course**
3. Or go to any course area and click **Restore**

### Step 2: Upload Backup File
1. Click **Choose a file...**
2. Upload **AI-Principianti-backup.mbz**
3. Click **Restore**

### Step 3: Confirm Backup Details
1. Review the backup information:
   - Course name: Introduzione all'Intelligenza Artificiale per Principianti
   - Original short name: AI-Principianti
   - Backup date and version
2. Click **Continue**

### Step 4: Choose Destination
Select one of these options:
- **Restore as a new course** (recommended for first import)
- **Restore into an existing course** (will merge/replace content)
- **Restore into current course** (if you're in a course)

### Step 5: Configure Settings
1. **Schema Settings:** Keep default (all activities included)
2. **Include:**
   - Activities: Yes
   - Blocks: Optional
   - Filters: Optional
   - Users: No (typically)
3. Click **Next**

### Step 6: Course Settings
1. Set or modify:
   - Course full name (default: Introduzione all'Intelligenza Artificiale per Principianti)
   - Course short name (default: AI-Principianti)
   - Course category (select appropriate category)
   - Course start date
2. Click **Next**

### Step 7: Review and Execute
1. Review all settings
2. Click **Perform restore**
3. Wait for the process to complete (usually 30-60 seconds)
4. Click **Continue** when finished

### Step 8: Verify Import
1. Navigate to the restored course
2. Check that all sections are visible (Modules 1-10)
3. Verify activities are present in each section
4. Test a few activities to ensure content displays correctly

---

## Post-Import Configuration

### Recommended Actions:

1. **Review Section Names:**
   - Sections are named "Modulo 1" through "Modulo 10"
   - Rename if you prefer different naming (e.g., "Week 1", "Topic 1")

2. **Set Enrollment Methods:**
   - Configure who can access the course
   - Set up self-enrollment, manual enrollment, or other methods

3. **Configure Course Settings:**
   - Set course visibility (visible/hidden)
   - Configure completion tracking if desired
   - Set grade categories and weights

4. **Review Activity Settings:**
   - Quiz: Set time limits, attempts, grading methods
   - Assignments: Set due dates, submission types, grading criteria
   - Forums: Configure subscription and post settings

5. **Add Additional Resources:**
   - Upload supplementary files
   - Add external links or videos
   - Configure course image/icon

6. **Test Student View:**
   - Switch to student role to see what learners will experience
   - Verify all content is accessible and readable

---

## Content Details

### Markdown to HTML Conversion
All markdown content has been automatically converted to HTML:
- Headers (H1-H6)
- Lists (ordered and unordered)
- Bold and italic text
- Code blocks
- Links
- Horizontal rules

### XML Encoding
- All special characters properly escaped
- Italian characters (accents, apostrophes) preserved
- CDATA sections used for HTML content
- Valid UTF-8 encoding throughout

### Activity Content

**Pages:** Contain theoretical material with:
- Definitions and explanations
- Examples and analogies
- Visual representations (as code/text)
- Module summaries

**Quizzes:** Contain:
- Assessment questions from the course content
- Instructions and objectives
- Content formatted as HTML

**Forums:** Provide spaces for:
- Discussions on controversial topics
- Case study analysis
- Student reflections and experiences

**Assignments:** Include:
- Practical exercises
- Hands-on labs
- Project work
- Case studies

**Labels:** Serve as:
- Module introductions
- Section dividers
- Navigation aids

---

## Troubleshooting

### Common Issues:

**Error: "Invalid backup file"**
- Ensure you're using Moodle 4.x or later
- Check file wasn't corrupted during download
- Try uploading again

**Error: "Course already exists with this short name"**
- Change the course short name during import
- Or restore into the existing course (will overwrite)

**Content Not Displaying Correctly**
- Check your Moodle theme supports HTML content
- Verify filters are enabled for HTML/multimedia
- Clear Moodle cache (Site administration > Development > Purge all caches)

**Missing Activities**
- Ensure all activity types are enabled in your Moodle instance
- Check that required plugins are installed
- Review import log for errors

**Character Encoding Issues**
- Verify your Moodle database uses UTF-8 encoding
- Check browser language settings
- Clear browser cache

---

## Technical Specifications

### Moodle Version Compatibility
- **Target Version:** Moodle 4.3
- **Compatible With:** Moodle 4.0+, potentially Moodle 3.9+
- **Backup Version:** 2023100900
- **Format:** Topics

### File Structure
```
AI-Principianti-backup.mbz (ZIP archive)
├── moodle_backup.xml (main backup manifest)
├── course/
│   └── course.xml (course definition)
├── sections/
│   ├── section_0/ (general section)
│   ├── section_1/ (Module 1)
│   ├── section_2/ (Module 2)
│   └── ... (sections 3-10)
├── activities/
│   ├── page_1/, page_2/, ... (39 pages)
│   ├── quiz_7/, quiz_22/, quiz_42/ (3 quizzes)
│   ├── forum_33/, forum_34/, ... (4 forums)
│   ├── assign_13/, assign_14/, ... (7 assignments)
│   └── label_1/, label_8/, ... (7 labels)
```

Each activity directory contains:
- `{activity-type}.xml` - Activity data and content
- `module.xml` - Module configuration

---

## Notes

### Content Limitations:
- Modules 4, 5, and 6 appear to be embedded within Module 3 in the source file
- Some content may need manual reorganization after import
- Quiz questions are included as formatted text (not individual question bank items)

### Customization Opportunities:
- Add multimedia content (videos, audio)
- Create proper question bank items from quiz content
- Expand forum discussions with starter posts
- Add rubrics to assignments
- Include completion criteria
- Set up gradebook categories

### Future Enhancements:
- Extract individual quiz questions into question bank
- Add course badges and completion tracking
- Create custom grading rubrics
- Develop supplementary resources
- Add interactive H5P activities

---

## Support

For issues specific to:
- **Moodle Import Process:** Consult Moodle documentation or your Moodle administrator
- **Course Content:** Review the original course-content-edited.md file
- **XML Structure:** Examine the moodle_backup directory for detailed structure

---

## Changelog

**Version 1.0** (2025-10-24)
- Initial course backup generation
- 7 modules parsed from source content
- 60 activities created across 10 sections
- Full Moodle 4.3 compatibility
- MBZ package created and tested

---

## License and Attribution

**Course Title:** Introduzione all'Intelligenza Artificiale per Principianti
**Generated:** October 24, 2025
**Format:** Moodle Backup (MBZ)
**Generator:** Custom Python script with markdown2 library

---

## Quick Reference

**File to Import:** `AI-Principianti-backup.mbz`
**File Size:** 233 KB
**Total Activities:** 60
**Sections:** 10
**Moodle Version:** 4.3+
**Language:** Italian
**Encoding:** UTF-8

**Import Steps:**
1. Site administration > Courses > Restore course
2. Upload AI-Principianti-backup.mbz
3. Choose "Restore as a new course"
4. Complete wizard with default settings
5. Verify and configure

---

*For detailed technical information about the generation process, see the Python scripts in the project directory.*
