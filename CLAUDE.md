# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a SCORM 1.2 course content generation system that uses a specialized multi-agent workflow to create universally-compatible e-learning content from structured outlines. SCORM 1.2 packages work on **all major LMS platforms** including Moodle, Canvas, Blackboard, Google Classroom, TalentLMS, Schoology, D2L Brightspace, and any other system that supports SCORM 1.2.

The system leverages Claude Code's agent capabilities to divide the content creation process into distinct, specialized phases.

## Agent-Based Architecture

The project uses five specialized agents defined in `.claude/agents/`:

### 1. course-outliner (Orange Agent)
- **Purpose**: Creates structured, pedagogically-sound course outlines from general topics and goals
- **Input**: User interview responses about course topic, audience, level, duration, and objectives
- **Output**: Complete structured markdown outline ready for content creation
- **Key Responsibilities**:
  - Interview user to gather requirements (topic, audience, duration, objectives)
  - Design optimal module/topic breakdown based on educational best practices
  - Write clear, measurable learning objectives using Bloom's Taxonomy
  - Balance theory/practice ratio appropriate for target level
  - Ensure progressive complexity across modules
  - Include variety of activity types (quizzes, exercises, projects, discussions)
- **Workflow**: Asks targeted questions → Presents design options → Generates complete outline

### 2. content-creator (Blue Agent)
- **Purpose**: Generates raw textual content from structured course outlines
- **Input**: Course outline with modules, topics, learning objectives, and activities
- **Output**: Textual content including explanations, instructions, prompts, and assignment descriptions
- **Key Responsibilities**:
  - Write content adhering to specified tone and target audience level
  - Create engaging, accurate, and actionable content
  - Format content for easy integration into LMS platforms (headings, bullet points, paragraphs)
  - Use proper markdown structure (tables, lists, headers)
  - Apply Italian tone guidelines (informal "tu", cultural relevance)
  - Include multimedia integration placeholders where appropriate

### 3. senior-editor (Red Agent)
- **Purpose**: Refines and polishes text for publication quality
- **Model**: Uses Sonnet model specifically
- **Key Responsibilities**:
  - Correct spelling, grammar, and punctuation errors (especially Italian accents)
  - Validate and fix markdown table formatting
  - Improve clarity by simplifying complex sentences
  - Remove redundancy and filler words
  - Ensure terminology consistency throughout content
  - Maintain appropriate readability for target audience (sentence length, concept density)
  - Preserve author's voice while enhancing readability
  - Conduct 6-pass editing: mechanics → clarity → conciseness → consistency → e-learning → flow

### 4. moodle-xml-formatter (Green Agent) → SCORM Package Generator
- **Purpose**: Converts raw content into SCORM 1.2 packages (universally compatible with all LMS platforms)
- **Input**: Raw textual content from content-creator (markdown format)
- **Output**: SCORM .zip package ready for import into any LMS
- **Key Responsibilities**:
  - Convert markdown to beautifully styled HTML pages
  - Create proper navigation between modules (Previous/Next/Index buttons)
  - Convert markdown tables into styled HTML tables
  - Generate valid imsmanifest.xml for SCORM 1.2 compliance
  - Package everything into a .zip file
- **Why SCORM 1.2**:
  - Works on ALL major LMS platforms (Moodle, Canvas, Blackboard, etc.)
  - Most reliable and stable e-learning standard since 2001
  - Universal compatibility unlike platform-specific formats
  - Supports progress tracking and completion status

### 5. multimedia-integrator (Purple Agent)
- **Purpose**: Integrates audio and video files into SCORM packages for any LMS
- **Input**: Audio/video files (MP3, MP4, etc.)
- **Output**: Standalone multimedia SCORM packages or compressed files ready for integration
- **Key Responsibilities**:
  - Analyze file sizes, formats, duration, and quality
  - Create standalone SCORM packages for audio (with HTML5 audio player)
  - Create standalone SCORM packages for video (with HTML5 video player, progress tracking)
  - Suggest and perform compression for large files using ffmpeg
  - Provide alternatives for files too large for direct upload (YouTube/Vimeo embedding)
  - Guide integration of multimedia into existing courses
  - Ensure cross-browser and cross-platform compatibility
- **Decision Tree**:
  - < 10 MB: Use directly in SCORM
  - 10-25 MB: Suggest optional compression
  - 25-50 MB: Recommend compression
  - 50-100 MB: Require compression or external hosting
  - \> 100 MB: YouTube/Vimeo embedding required

## Typical Workflow

The standard content creation workflow follows this sequence:

### For Text-Based Courses:
1. **Course Design**: Use the `course-outliner` agent to interview user and create pedagogically-sound outline
2. **Content Creation**: Use the `content-creator` agent to generate textual content from the outline
3. **Editing**: Use the `senior-editor` agent to refine and polish the generated content
4. **SCORM Packaging**: Use the `moodle-xml-formatter` agent to convert finalized content into a SCORM package
5. **Import**: Upload the SCORM .zip file to any LMS as a SCORM activity (100% compatible with all platforms)

### For Multimedia Integration:
1. **Analysis**: Use the `multimedia-integrator` agent to analyze audio/video files
2. **Processing**: Agent will compress files if needed or suggest alternatives
3. **SCORM Creation**: Generate standalone multimedia SCORM packages
4. **Import**: Upload as separate SCORM activities in your LMS course

## Working with Agents

To invoke agents in this project:
- Course design: Use Task tool with `subagent_type="course-outliner"`
- Content creation: Use Task tool with `subagent_type="content-creator"`
- Text editing: Use Task tool with `subagent_type="senior-editor"`
- SCORM packaging: Use Task tool with `subagent_type="moodle-xml-formatter"` (generates SCORM, not XML)
- Multimedia integration: Use Task tool with `subagent_type="multimedia-integrator"`

Each agent operates independently and focuses on its specialized task. Pass clear, structured inputs to each agent and ensure outputs from one agent are properly formatted for the next agent in the workflow.

## SCORM Package Generation

The system uses `create_scorm_package.py` to generate SCORM 1.2 packages. This script:
- Converts markdown content to styled HTML
- Handles tables, lists, headers, bold/italic text
- Adds navigation buttons between modules
- Creates SCORM manifest (imsmanifest.xml)
- Packages everything into a .zip file

**To generate SCORM manually:**
```bash
python create_scorm_package.py
```

**To import into your LMS:**

**Moodle:**
1. Go to your Moodle course
2. Click "Aggiungi un'attività o una risorsa"
3. Select "Pacchetto SCORM"
4. Upload the generated .zip file
5. Save and view - Done!

**Canvas:**
1. Settings → Import Course Content
2. Select "SCORM Package"
3. Upload the .zip file

**Blackboard:**
1. Content → Build Content → SCORM Package
2. Upload the .zip file

**Other LMS:** Consult your LMS documentation for SCORM 1.2 import procedure.

## Multimedia SCORM Generation

### Audio SCORM Packages
The system uses `create_audio_scorm.py` to create standalone audio SCORM packages:

**Supported formats:** MP3, WAV, OGG, M4A, AAC

**To generate audio SCORM:**
```bash
python create_audio_scorm.py <audio_file> [title] [description]
```

**Features:**
- Professional HTML5 audio player
- SCORM tracking (marks complete when audio finishes)
- Mobile-responsive design
- Progress bar and playback controls

### Video SCORM Packages
The system uses `create_video_scorm.py` to create standalone video SCORM packages:

**Supported formats:** MP4, WEBM, MOV, AVI, MKV

**To generate video SCORM:**
```bash
python create_video_scorm.py <video_file> [title] [description]
```

**Features:**
- Professional HTML5 video player
- SCORM tracking (marks complete at 90% viewed)
- Fullscreen mode
- Progress tracking
- Mobile-responsive design

### Video Compression
For large video files, use ffmpeg compression:

```bash
# Good quality (recommended)
ffmpeg -i input.mp4 -vcodec libx264 -crf 23 -preset medium -acodec aac -b:a 128k output.mp4

# Smaller file size
ffmpeg -i input.mp4 -vcodec libx264 -crf 28 -preset fast -acodec aac -b:a 96k output.mp4
```

**CRF Values:**
- 18-20: Visually lossless (large file)
- 23: High quality (recommended)
- 28: Good quality, smaller file
- 32: Acceptable quality, very small file

## Quality Standards

- **Pedagogical Soundness**: Course structures follow educational best practices (Bloom's Taxonomy, progressive complexity)
- **Accuracy**: All educational content must be factually correct and relevant
- **Engagement**: Content should capture and maintain learner interest through variety and real-world examples
- **Accessibility**: Text should be appropriate for the target audience's level (sentence length, concept density)
- **Italian Language Excellence**:
  - Proper accents (è, à, ò, ù, ì, più, però, già, può)
  - Informal "tu" tone consistently
  - Culturally relevant examples (Italian/European context)
- **Table Quality**: All markdown tables properly formatted with headers, separators, and styled HTML output
- **SCORM Compliance**: SCORM packages must be valid SCORM 1.2 format and work on all LMS platforms
- **Professional Styling**: HTML output must be beautifully formatted with proper tables, colors, and responsive design
- **Cross-Platform Compatibility**: Content must work in all major browsers (Chrome, Firefox, Safari, Edge)
- **Terminology Consistency**: Technical terms defined on first use and used consistently throughout
- **Multimedia Optimization**: Audio/video files appropriately sized for LMS upload with quality preservation
- **Mobile Responsive**: All content must be viewable and functional on mobile devices

## Troubleshooting

**If SCORM import fails:**
- Verify the .zip file is not corrupted
- Check that imsmanifest.xml is present in the root of the zip
- Ensure SCORM activity/content type is enabled in your LMS
- Try importing in a different browser
- Consult your LMS administrator if issues persist

**If tables don't display correctly:**
- Re-run `create_scorm_package.py` (latest version includes table CSS)
- Check that markdown tables have proper formatting with `|` separators
- Ensure same number of columns in all rows
- Verify header row and separator row (`|---|---|`) are present

**If file upload fails (too large):**
- **For Moodle (XAMPP/Local)**: Edit `php.ini` through XAMPP Control Panel
  - Set `upload_max_filesize=100M`
  - Set `post_max_size=100M`
  - Set `max_execution_time=300`
  - Restart Apache
- **For any LMS**: Contact your LMS administrator to increase upload limits
- **Alternative**: Compress video/audio files using ffmpeg (see compression section)
- **Alternative**: Use YouTube/Vimeo embedding for very large videos
- **Alternative**: Split large courses into smaller SCORM modules

**If video/audio won't play in SCORM:**
- Re-encode to H.264/AAC (most compatible format)
- Check browser console for errors
- Verify file is included in SCORM zip
- Test in different browsers (Chrome, Firefox, Edge)

**For other issues:**
- Check `GUIDA_IMPORT_MOODLE.md` for detailed import instructions
- Check `GUIDA_AUMENTARE_LIMITE_UPLOAD_MOODLE.md` for upload limit solutions
- Review generated HTML files in `scorm_package/` directory before zipping
