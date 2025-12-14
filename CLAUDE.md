# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

SCORM 1.2 course content generation system using a multi-agent workflow. Creates universally-compatible e-learning content for all major LMS platforms (Moodle, Canvas, Blackboard, Google Classroom, TalentLMS, Schoology, D2L Brightspace, etc.).

## Common Commands

```bash
# Generate SCORM package from markdown content
# IMPORTANT: Run from the directory containing 'course-content-edited.md'
cd content/[course-name]
python ../../scripts/scorm_generators/create_scorm_package.py

# Create audio SCORM package
python scripts/scorm_generators/create_audio_scorm.py <audio_file> [title] [description]

# Create video SCORM package
python scripts/scorm_generators/create_video_scorm.py <video_file> [title] [description]

# Compress video (CRF 23 = high quality, CRF 28 = smaller file)
ffmpeg -i input.mp4 -vcodec libx264 -crf 23 -preset medium -acodec aac -b:a 128k output.mp4

# Compress audio to MP3
ffmpeg -i input.wav -codec:a libmp3lame -b:a 128k output.mp3
```

## Directory Structure

```
scripts/
├── scorm_generators/        # SCORM package creators (text, audio, video)
│   ├── create_scorm_package.py   # Expects 'course-content-edited.md' in CWD
│   ├── create_audio_scorm.py     # Standalone audio SCORM
│   └── create_video_scorm.py     # Standalone video SCORM
├── content_generation/      # HTML page generation, content editing
└── legacy/                  # Deprecated scripts (reference only)

content/                     # Course content organized by course
├── ai-principianti/         # AI for beginners (10 modules)
├── sicurezza-lavoro/        # Workplace safety (D.Lgs. 81/08)
└── eu-ai-act-pmi/           # EU AI Act for SMEs

.claude/agents/              # Agent definition files
output/                      # Generated SCORM packages (.zip)
docs/                        # Import guides and troubleshooting
```

## Agent Workflow

The system uses five specialized agents invoked via Task tool with `subagent_type`:

| Agent | subagent_type | Purpose |
|-------|---------------|---------|
| Course Outliner | `course-outliner` | Interview user → create pedagogically-sound course structure |
| Content Creator | `content-creator` | Generate textual content from outline |
| Senior Editor | `senior-editor` | Refine and polish content (uses Sonnet model) |
| SCORM Packager | `moodle-xml-formatter` | Convert markdown → SCORM .zip package |
| Multimedia Integrator | `multimedia-integrator` | Create audio/video SCORM packages |

**Standard workflow:**
1. `course-outliner` → Interview and create outline
2. `content-creator` → Write content from outline
3. `senior-editor` → Polish and edit
4. `moodle-xml-formatter` → Package as SCORM .zip

## SCORM Package Generation

The `create_scorm_package.py` script reads `course-content-edited.md` from the current directory. It:
- Splits content at `# Modulo X:` headers (each becomes a separate HTML page)
- Converts markdown to styled HTML with navigation buttons
- Creates `imsmanifest.xml` for SCORM 1.2 compliance
- Outputs `scorm_package/` directory and a `.zip` file

**Content file format:**
```markdown
# Modulo 1: Titolo Primo Modulo
Content here...

# Modulo 2: Titolo Secondo Modulo
Content here...
```

**Audio SCORM:** Marks complete when audio finishes. Supports MP3, WAV, OGG, M4A, AAC.

**Video SCORM:** Marks complete at 90% viewed. Supports MP4, WEBM, MOV, AVI, MKV.

## Multimedia File Size Guidelines

| Size | Action |
|------|--------|
| < 10 MB | Use directly |
| 10-25 MB | Optional compression |
| 25-50 MB | Recommend compression |
| 50-100 MB | Require compression |
| > 100 MB | External hosting (YouTube/Vimeo) |

## Italian Language Guidelines

- Use informal "tu" tone consistently
- Proper accents: è, à, ò, ù, ì, più, però, già, può
- Culturally relevant examples (Italian/European context)

## Quality Standards

- **Pedagogical**: Bloom's Taxonomy, progressive complexity
- **Tables**: Markdown tables with `|` separators, header row, and `|---|---|` separator
- **SCORM**: Valid imsmanifest.xml in zip root
- **Responsive**: Mobile-friendly HTML output

## Troubleshooting

**SCORM import fails:** Check imsmanifest.xml exists in zip root.

**Tables broken:** Ensure header row + separator row (`|---|---|`) + consistent column count.

**Upload too large:** For Moodle/XAMPP, edit php.ini: `upload_max_filesize=100M`, `post_max_size=100M`.

**Media won't play:** Re-encode to H.264/AAC format.

See `docs/` for detailed guides: `GUIDA_IMPORT_MOODLE.md`, `GUIDA_AUMENTARE_LIMITE_UPLOAD_MOODLE.md`
