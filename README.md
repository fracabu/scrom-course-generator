# SCORM Course Generator

Sistema professionale per la generazione di contenuti didattici in formato SCORM 1.2, compatibile con qualsiasi LMS (Learning Management System).

[![Python 3.x](https://img.shields.io/badge/Python-3.x-blue.svg)](https://www.python.org/)
[![SCORM 1.2](https://img.shields.io/badge/SCORM-1.2-green.svg)](https://scorm.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## Indice

- [Panoramica](#panoramica)
- [Caratteristiche Principali](#caratteristiche-principali)
- [Requisiti di Sistema](#requisiti-di-sistema)
- [Installazione](#installazione)
- [Quick Start](#quick-start)
- [Architettura Multi-Agente](#architettura-multi-agente)
- [Struttura del Progetto](#struttura-del-progetto)
- [Guida Completa agli Script](#guida-completa-agli-script)
- [Integrazione Multimediale](#integrazione-multimediale)
- [Importazione nei LMS](#importazione-nei-lms)
- [Standard di Qualità](#standard-di-qualità)
- [Risoluzione Problemi](#risoluzione-problemi)
- [Esempi di Corsi](#esempi-di-corsi)
- [Contributing](#contributing)
- [Licenza](#licenza)

---

## Panoramica

Questo progetto utilizza un'**architettura multi-agente basata su AI** per creare contenuti didattici di alta qualità in formato SCORM 1.2. Il sistema divide il processo di creazione in fasi specializzate, ciascuna gestita da un agente dedicato con competenze specifiche.

### Perché SCORM 1.2?

SCORM 1.2 è lo standard e-learning più affidabile e universalmente supportato:

| Vantaggio | Descrizione |
|-----------|-------------|
| **Compatibilità Universale** | Funziona su qualsiasi LMS moderno |
| **Affidabilità** | Standard maturo e stabile dal 2001 |
| **Tracciamento** | Supporta completamento e progressi dell'utente |
| **Portabilità** | Un unico pacchetto funziona ovunque |
| **Offline-Ready** | Visualizzabile anche localmente senza LMS |

### LMS Supportati

- **Moodle** (tutte le versioni)
- **Canvas** (Instructure)
- **Blackboard Learn**
- **Google Classroom**
- **TalentLMS**
- **Schoology**
- **D2L Brightspace**
- **SAP Litmos**
- **Docebo**
- **iSpring Learn**
- E qualsiasi altro LMS che supporta SCORM 1.2

---

## Caratteristiche Principali

### Generazione Contenuti
- **Creazione Automatica**: Da semplice outline a corso completo
- **Qualità Professionale**: Contenuti pedagogicamente validi e grammaticalmente corretti
- **Multi-lingua**: Ottimizzato per italiano con supporto accenti e tono formale/informale

### Formattazione
- **Markdown → HTML**: Conversione automatica con stili professionali
- **Tabelle Responsive**: Rendering perfetto su desktop e mobile
- **Navigazione Integrata**: Pulsanti Precedente/Successivo/Indice

### Multimedia
- **Audio SCORM**: Player HTML5 con tracciamento completamento
- **Video SCORM**: Player con progress bar e completamento al 90%
- **Compressione Intelligente**: Ottimizzazione automatica file grandi

### Tracciamento
- **SCORM API**: Comunicazione completa con LMS
- **Stato Completamento**: incomplete → completed
- **Punteggio**: Supporto score reporting

---

## Requisiti di Sistema

### Obbligatori

| Requisito | Versione | Note |
|-----------|----------|------|
| **Python** | 3.8+ | Testato su 3.9, 3.10, 3.11 |
| **Claude Code** | Latest | Per utilizzo agenti AI |

### Opzionali

| Requisito | Versione | Utilizzo |
|-----------|----------|----------|
| **ffmpeg** | 4.0+ | Compressione video/audio |
| **Git** | 2.0+ | Version control |

### Installazione ffmpeg

**Windows (con Chocolatey):**
```powershell
choco install ffmpeg
```

**Windows (manuale):**
1. Scarica da https://ffmpeg.org/download.html
2. Estrai in `C:\ffmpeg`
3. Aggiungi `C:\ffmpeg\bin` al PATH di sistema

**macOS:**
```bash
brew install ffmpeg
```

**Linux (Ubuntu/Debian):**
```bash
sudo apt update && sudo apt install ffmpeg
```

---

## Installazione

### 1. Clona il Repository

```bash
git clone https://github.com/tuousername/scorm-course-generator.git
cd scorm-course-generator
```

### 2. Verifica Python

```bash
python --version  # Deve essere 3.8+
```

### 3. (Opzionale) Crea Virtual Environment

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS/Linux
source venv/bin/activate
```

### 4. Verifica Installazione

```bash
python scripts/scorm_generators/create_scorm_package.py --help
```

---

## Quick Start

### Metodo 1: Usando gli Agenti AI (Consigliato)

Il modo più semplice per creare un corso completo è utilizzare gli agenti AI in Claude Code:

```
1. Apri Claude Code nella directory del progetto
2. Chiedi: "Voglio creare un corso su [ARGOMENTO]"
3. L'agente course-outliner ti intervisterà per capire i requisiti
4. Seguiranno automaticamente content-creator, senior-editor e il packaging SCORM
```

### Metodo 2: Usando gli Script Direttamente

#### Passo 1: Prepara il Contenuto

Crea un file markdown con la struttura:

```markdown
# Modulo 1: Introduzione

## Obiettivi di Apprendimento
- Comprendere i concetti base
- Applicare le tecniche fondamentali

## Contenuto
Testo del modulo...

# Modulo 2: Approfondimento

## Obiettivi di Apprendimento
...
```

#### Passo 2: Genera il Pacchetto SCORM

```bash
python scripts/scorm_generators/create_scorm_package.py
```

#### Passo 3: Importa nel tuo LMS

Carica il file `.zip` generato nel tuo LMS come "Pacchetto SCORM".

---

## Architettura Multi-Agente

Il sistema utilizza **cinque agenti specializzati**, ciascuno con competenze specifiche:

```
┌─────────────────────────────────────────────────────────────────┐
│                        WORKFLOW COMPLETO                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐       │
│  │   COURSE     │    │   CONTENT    │    │   SENIOR     │       │
│  │   OUTLINER   │───▶│   CREATOR    │───▶│   EDITOR     │       │
│  │   (Orange)   │    │   (Blue)     │    │   (Red)      │       │
│  └──────────────┘    └──────────────┘    └──────────────┘       │
│         │                                        │               │
│         │              Outline                   │ Contenuto     │
│         │              Strutturato               │ Raffinato     │
│         ▼                                        ▼               │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                    SCORM PACKAGER                         │   │
│  │                       (Green)                             │   │
│  └──────────────────────────────────────────────────────────┘   │
│                              │                                   │
│                              ▼                                   │
│                    ┌──────────────────┐                         │
│                    │  Pacchetto SCORM │                         │
│                    │     (.zip)       │                         │
│                    └──────────────────┘                         │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │              MULTIMEDIA INTEGRATOR (Purple)               │   │
│  │         Audio/Video → SCORM Standalone Packages           │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Dettaglio Agenti

#### 1. Course Outliner (Arancione)
**Scopo**: Crea strutture di corso pedagogicamente valide

| Aspetto | Dettaglio |
|---------|-----------|
| **Input** | Intervista con obiettivi, audience, durata, livello |
| **Output** | Outline completo con moduli, argomenti e attività |
| **Metodologia** | Bloom's Taxonomy, complessità progressiva |
| **Invocazione** | `subagent_type="course-outliner"` |

**Esempio di output:**
```markdown
# Corso: Introduzione all'Intelligenza Artificiale

## Modulo 1: Fondamenti (2 ore)
### Obiettivi
- Definire l'intelligenza artificiale
- Distinguere AI debole e forte

### Argomenti
1.1 Storia dell'AI
1.2 Tipi di AI
1.3 Applicazioni quotidiane

### Attività
- Quiz di autovalutazione
- Discussione: "L'AI nella tua vita"
```

#### 2. Content Creator (Blu)
**Scopo**: Genera contenuti testuali dettagliati

| Aspetto | Dettaglio |
|---------|-----------|
| **Input** | Outline strutturato del corso |
| **Output** | Contenuti completi in markdown |
| **Stile** | Tono "tu", esempi pratici, italiano corretto |
| **Invocazione** | `subagent_type="content-creator"` |

#### 3. Senior Editor (Rosso)
**Scopo**: Raffina e perfeziona i contenuti

| Aspetto | Dettaglio |
|---------|-----------|
| **Input** | Bozza dei contenuti |
| **Output** | Contenuti pubblicabili |
| **Modello** | Usa specificamente Sonnet |
| **Invocazione** | `subagent_type="senior-editor"` |

**Processo di editing in 6 passaggi:**
1. **Meccanica**: Grammatica, ortografia, punteggiatura
2. **Chiarezza**: Semplificazione frasi complesse
3. **Concisione**: Rimozione ridondanze
4. **Consistenza**: Terminologia uniforme
5. **E-learning**: Adattamento formato digitale
6. **Flusso**: Coerenza narrativa

#### 4. SCORM Packager (Verde)
**Scopo**: Converte contenuti in pacchetti SCORM

| Aspetto | Dettaglio |
|---------|-----------|
| **Input** | Contenuti markdown finali |
| **Output** | File .zip SCORM 1.2 compliant |
| **Include** | HTML stilizzato, navigazione, imsmanifest.xml |
| **Invocazione** | `subagent_type="moodle-xml-formatter"` |

#### 5. Multimedia Integrator (Viola)
**Scopo**: Crea pacchetti SCORM per audio/video

| Aspetto | Dettaglio |
|---------|-----------|
| **Input** | File audio (MP3, WAV, etc.) o video (MP4, WEBM, etc.) |
| **Output** | Pacchetti SCORM standalone con player HTML5 |
| **Funzioni** | Analisi, compressione, ottimizzazione |
| **Invocazione** | `subagent_type="multimedia-integrator"` |

---

## Struttura del Progetto

```
scorm-course-generator/
│
├── .claude/                          # Configurazione Claude Code
│   ├── agents/                       # Definizioni agenti
│   │   ├── course-outliner.md       # Agente struttura corso
│   │   ├── content-creator.md       # Agente creazione contenuti
│   │   ├── senior-editor.md         # Agente editing
│   │   ├── moodle-xml-formatter.md  # Agente SCORM packaging
│   │   └── multimedia-integrator.md # Agente multimedia
│   └── settings.local.json          # Impostazioni locali
│
├── scripts/                          # Script Python
│   ├── scorm_generators/            # Generatori SCORM
│   │   ├── create_scorm_package.py  # Genera pacchetto testo
│   │   ├── create_audio_scorm.py    # Genera pacchetto audio
│   │   ├── create_video_scorm.py    # Genera pacchetto video
│   │   └── create_sicurezza_scorm.py # Template corso sicurezza
│   ├── content_generation/          # Generazione contenuti
│   │   ├── create_html_pages.py     # Conversione HTML
│   │   └── edit_course_correct.py   # Editing automatico
│   └── legacy/                      # Script deprecati
│       └── ...                      # Mantenuti per riferimento
│
├── content/                         # Contenuti corsi
│   ├── ai-principianti/            # Esempio: Corso AI
│   │   ├── course-outline.md       # Struttura corso
│   │   ├── course-content-edited.md # Contenuto finale
│   │   └── modules/                # Moduli separati
│   ├── sicurezza-lavoro/           # Esempio: Sicurezza
│   │   ├── modulo1-content.md
│   │   ├── modulo2-content.md
│   │   └── modulo3-content.md
│   └── eu-ai-act-pmi/              # Esempio: AI Act EU
│       ├── course-outline.md
│       └── modulo*.md
│
├── media/                           # File multimediali
│   ├── audio/                      # File audio sorgente
│   └── video/                      # File video sorgente
│
├── output/                          # Output generati
│   └── scorm/                      # Pacchetti SCORM .zip
│
├── docs/                            # Documentazione
│   ├── GUIDA_IMPORT_MOODLE.md      # Guida import Moodle
│   ├── GUIDA_AUMENTARE_LIMITE_UPLOAD_MOODLE.md
│   ├── GUIDA_COMPATIBILITA_LMS.md  # Compatibilità LMS
│   └── ISTRUZIONI_IMPORT_*.md      # Guide specifiche
│
├── temp/                            # File temporanei (gitignore)
│
├── CLAUDE.md                        # Istruzioni per Claude Code
├── README.md                        # Questo file
└── .gitignore                       # File ignorati da Git
```

---

## Guida Completa agli Script

### create_scorm_package.py

**Scopo**: Genera pacchetto SCORM da file markdown

**Utilizzo**:
```bash
python scripts/scorm_generators/create_scorm_package.py
```

**Requisiti input**:
- File `course-content-edited.md` nella directory corrente
- Struttura con intestazioni `# Modulo X: Titolo`

**Output**:
- Directory `scorm_package/` con file HTML
- File `[nome-corso]-SCORM.zip`

**Funzionalità**:
- Conversione Markdown → HTML
- Gestione tabelle con CSS styling
- Navigazione inter-modulo
- Manifest SCORM 1.2 valido

### create_audio_scorm.py

**Scopo**: Crea pacchetto SCORM con player audio

**Utilizzo**:
```bash
# Base
python scripts/scorm_generators/create_audio_scorm.py lezione.mp3

# Con titolo
python scripts/scorm_generators/create_audio_scorm.py lezione.mp3 "Lezione 1"

# Con titolo e descrizione
python scripts/scorm_generators/create_audio_scorm.py lezione.mp3 "Lezione 1" "Introduzione al corso"
```

**Formati supportati**: MP3, WAV, OGG, M4A, AAC

**Caratteristiche**:
- Player HTML5 responsive
- Tracciamento SCORM (completato quando audio finisce)
- Design mobile-friendly
- Messaggio completamento visivo

### create_video_scorm.py

**Scopo**: Crea pacchetto SCORM con player video

**Utilizzo**:
```bash
# Base
python scripts/scorm_generators/create_video_scorm.py video.mp4

# Con titolo
python scripts/scorm_generators/create_video_scorm.py video.mp4 "Video Lezione 1"

# Completo
python scripts/scorm_generators/create_video_scorm.py video.mp4 "Video Lezione 1" "Panoramica del modulo"
```

**Formati supportati**: MP4, WEBM, MOV, AVI, MKV

**Caratteristiche**:
- Player HTML5 con controlli nativi
- Progress bar personalizzata
- Completamento al 90% della visualizzazione
- Fullscreen mode
- Design responsive

---

## Integrazione Multimediale

### Linee Guida Dimensioni File

| Dimensione | Raccomandazione | Azione |
|------------|-----------------|--------|
| < 10 MB | Ideale | Usa direttamente |
| 10-25 MB | Accettabile | Compressione opzionale |
| 25-50 MB | Grande | Compressione consigliata |
| 50-100 MB | Molto grande | Compressione necessaria |
| > 100 MB | Troppo grande | Hosting esterno (YouTube/Vimeo) |

### Compressione Video con ffmpeg

#### Presets Consigliati

**Alta Qualità (bilanciato)**:
```bash
ffmpeg -i input.mp4 -vcodec libx264 -crf 23 -preset medium -acodec aac -b:a 128k output.mp4
```

**File Piccolo (qualità buona)**:
```bash
ffmpeg -i input.mp4 -vcodec libx264 -crf 28 -preset fast -acodec aac -b:a 96k output.mp4
```

**Minimo (qualità accettabile)**:
```bash
ffmpeg -i input.mp4 -vcodec libx264 -crf 32 -preset veryfast -acodec aac -b:a 64k output.mp4
```

#### Guida Valori CRF

| CRF | Qualità | Uso Tipico |
|-----|---------|------------|
| 18-20 | Visivamente lossless | Archivio, master |
| 21-23 | Alta qualità | Raccomandato per corsi |
| 24-27 | Buona qualità | Bilanciamento qualità/dimensione |
| 28-32 | Accettabile | Quando dimensione è priorità |

### Compressione Audio

```bash
# MP3 alta qualità
ffmpeg -i input.wav -codec:a libmp3lame -b:a 192k output.mp3

# MP3 bilanciato
ffmpeg -i input.wav -codec:a libmp3lame -b:a 128k output.mp3

# MP3 compatto
ffmpeg -i input.wav -codec:a libmp3lame -b:a 96k output.mp3
```

### Embedding Video Esterni

Per video > 100 MB, usa embedding YouTube/Vimeo nel contenuto HTML:

```html
<!-- YouTube -->
<iframe width="560" height="315"
        src="https://www.youtube.com/embed/VIDEO_ID"
        frameborder="0" allowfullscreen></iframe>

<!-- Vimeo -->
<iframe src="https://player.vimeo.com/video/VIDEO_ID"
        width="560" height="315"
        frameborder="0" allowfullscreen></iframe>
```

---

## Importazione nei LMS

### Moodle

#### Procedura Standard

1. **Accedi al corso** Moodle dove vuoi aggiungere il contenuto
2. **Attiva modifica**: Clicca "Attiva modifica" in alto a destra
3. **Aggiungi attività**: Clicca "Aggiungi un'attività o una risorsa"
4. **Seleziona SCORM**: Scegli "Pacchetto SCORM" dalla lista
5. **Carica file**:
   - Clicca "Aggiungi file" o trascina il .zip
   - Attendi il caricamento completo
6. **Configura** (opzionale):
   - Nome: Personalizza il titolo visualizzato
   - Descrizione: Aggiungi note per gli studenti
   - Aspetto: Configura dimensioni finestra
7. **Salva**: Clicca "Salva e visualizza"

#### Configurazione Avanzata Moodle

**Impostazioni Pacchetto**:
- **Metodo di grading**: "Punteggio più alto" per quiz
- **Numero massimo tentativi**: Illimitato per studio
- **Visualizzazione struttura**: "Disabilitata" per navigazione custom

**Impostazioni Aspetto**:
- **Tipo visualizzazione**: "Nuova finestra" consigliato
- **Larghezza/Altezza**: 100% per responsive

### Canvas

1. **Vai a Settings** del corso
2. **Import Course Content** → Seleziona "SCORM Package"
3. **Choose File**: Carica il .zip
4. **Import**: Attendi completamento
5. **Pubblica**: Il contenuto apparirà nei Moduli

### Blackboard

1. **Content Area** → "Build Content"
2. **Content Package (SCORM)**
3. **Browse**: Seleziona il .zip
4. **Submit**: Configura opzioni e salva

### Google Classroom

Google Classroom non supporta nativamente SCORM. Opzioni:
1. **Usa SCORM Cloud** come intermediario
2. **Estrai HTML** e carica come materiale
3. **Link esterno** a LMS con supporto SCORM

### Altri LMS

La maggior parte dei LMS moderni supporta SCORM 1.2:

| LMS | Percorso Import |
|-----|-----------------|
| TalentLMS | Course → Add Content → SCORM |
| Schoology | Materials → Add File → SCORM Package |
| D2L Brightspace | Content → Import Components |
| SAP Litmos | Courses → Create → SCORM |
| Docebo | Course Management → Training Material |

---

## Standard di Qualità

### Pedagogia

- **Bloom's Taxonomy**: Obiettivi strutturati per livelli cognitivi
- **Complessità Progressiva**: Dal semplice al complesso
- **Varietà Attività**: Quiz, esercizi, discussioni, progetti
- **Feedback Immediato**: Riscontro su quiz e attività

### Contenuti

- **Accuratezza**: Informazioni verificate e aggiornate
- **Rilevanza**: Esempi pratici e casi reali
- **Engagement**: Stile coinvolgente, non accademico
- **Accessibilità**: Linguaggio appropriato al target

### Lingua Italiana

| Aspetto | Standard |
|---------|----------|
| **Tono** | Informale "tu" (non "Lei" o "voi") |
| **Accenti** | Sempre corretti: è, à, ò, ù, ì, é |
| **Apostrofi** | Uso corretto: un'altra, qual è (no apostrofo) |
| **Esempi** | Contesto italiano/europeo |
| **Terminologia** | Italiano quando possibile, inglese se standard |

### Tecnici

- **SCORM 1.2**: Manifest valido, risorse dichiarate
- **HTML5**: Semantico, accessibile, responsive
- **CSS**: Mobile-first, cross-browser
- **JavaScript**: SCORM API corretto, fallback graceful

---

## Risoluzione Problemi

### Problemi Comuni

#### SCORM non si apre nel LMS

**Sintomi**: Errore import, pagina bianca, "file non valido"

**Soluzioni**:
1. Verifica che `imsmanifest.xml` sia nella root dello zip (non in sottocartella)
2. Apri lo zip e controlla la struttura
3. Rigenera il pacchetto con lo script

```bash
# Verifica contenuto zip
python -c "import zipfile; print(zipfile.ZipFile('package.zip').namelist())"
```

#### Tabelle non visualizzate correttamente

**Sintomi**: Tabelle senza bordi, formattazione rotta

**Soluzioni**:
1. Verifica formato markdown:
   ```markdown
   | Colonna 1 | Colonna 2 |
   |-----------|-----------|
   | Dato 1    | Dato 2    |
   ```
2. Controlla che tutte le righe abbiano stesso numero di `|`
3. Rigenera il pacchetto (include CSS tabelle aggiornato)

#### Upload fallisce (file troppo grande)

**Sintomi**: Timeout, errore upload, "file exceeds limit"

**Soluzioni per Moodle locale (XAMPP)**:

1. Apri XAMPP Control Panel
2. Apache → Config → php.ini
3. Modifica:
   ```ini
   upload_max_filesize = 100M
   post_max_size = 100M
   max_execution_time = 300
   max_input_time = 300
   memory_limit = 256M
   ```
4. Riavvia Apache

**Soluzioni generali**:
- Comprimi video/audio con ffmpeg
- Dividi corso in moduli separati
- Usa hosting esterno per media grandi

#### Video/Audio non si riproduce

**Sintomi**: Player vuoto, errore codec, no audio

**Soluzioni**:
1. **Converti a formato standard**:
   ```bash
   # Video → MP4 H.264
   ffmpeg -i input.mov -vcodec libx264 -acodec aac output.mp4

   # Audio → MP3
   ffmpeg -i input.wav -codec:a libmp3lame -b:a 128k output.mp3
   ```
2. Verifica che il file sia incluso nello zip
3. Testa in browser diversi (Chrome, Firefox, Edge)
4. Controlla console browser per errori (F12)

#### Completamento non tracciato

**Sintomi**: Corso sempre "incomplete", punteggio non salvato

**Soluzioni**:
1. Verifica che LMS abbia SCORM abilitato
2. Controlla impostazioni pacchetto nel LMS
3. Testa con SCORM Cloud (debug)
4. Verifica JavaScript non abbia errori (console browser)

### Debug Avanzato

#### Testare SCORM Localmente

```bash
# Server locale Python
cd scorm_package
python -m http.server 8000
# Apri http://localhost:8000/index.html
```

#### Validare Manifest

```bash
# Verifica XML ben formato
python -c "import xml.etree.ElementTree as ET; ET.parse('imsmanifest.xml')"
```

#### SCORM Cloud Testing

1. Crea account su https://cloud.scorm.com
2. Upload pacchetto per test
3. Usa debugger integrato per verificare chiamate API

---

## Esempi di Corsi

### Corsi Inclusi

Il repository include esempi completi:

#### 1. AI per Principianti (`content/ai-principianti/`)
- **Moduli**: 10
- **Durata**: ~8 ore
- **Livello**: Base
- **Contenuto**: Introduzione completa all'intelligenza artificiale

#### 2. Sicurezza sul Lavoro (`content/sicurezza-lavoro/`)
- **Moduli**: 3 + Test finale
- **Durata**: ~4 ore
- **Livello**: Base
- **Contenuto**: Formazione obbligatoria D.Lgs. 81/08

#### 3. EU AI Act per PMI (`content/eu-ai-act-pmi/`)
- **Moduli**: 4
- **Durata**: ~3 ore
- **Livello**: Intermedio
- **Contenuto**: Regolamento europeo AI per piccole/medie imprese

### Creare un Nuovo Corso

1. **Crea directory**:
   ```bash
   mkdir content/mio-nuovo-corso
   ```

2. **Crea outline** (`course-outline.md`):
   ```markdown
   # Corso: Nome del Corso

   ## Informazioni Generali
   - Target: [descrizione audience]
   - Durata: [ore totali]
   - Livello: [base/intermedio/avanzato]

   ## Modulo 1: [Titolo]
   ### Obiettivi
   - ...
   ### Argomenti
   - ...
   ```

3. **Genera contenuti** con agente o manualmente

4. **Crea pacchetto SCORM**:
   ```bash
   cd content/mio-nuovo-corso
   python ../../scripts/scorm_generators/create_scorm_package.py
   ```

---

## Contributing

### Come Contribuire

1. **Fork** del repository
2. **Crea branch**: `git checkout -b feature/nuova-funzione`
3. **Commit**: `git commit -m "Aggiunge nuova funzione"`
4. **Push**: `git push origin feature/nuova-funzione`
5. **Pull Request**: Apri PR con descrizione dettagliata

### Linee Guida

- **Codice**: Segui PEP 8 per Python
- **Commit**: Messaggi chiari in italiano o inglese
- **Documentazione**: Aggiorna README e CLAUDE.md se necessario
- **Test**: Verifica che i pacchetti generati funzionino

### Segnalare Bug

Apri una Issue con:
- Descrizione del problema
- Passi per riprodurre
- Output/errore completo
- Sistema operativo e versione Python

---

## Licenza

Questo progetto è rilasciato sotto licenza MIT. Vedi il file `LICENSE` per dettagli.

---

## Contatti e Supporto

Per problemi o domande:

1. **Documentazione**: Controlla `docs/` per guide dettagliate
2. **CLAUDE.md**: Istruzioni per utilizzo con Claude Code
3. **Esempi**: Consulta `content/` per riferimento
4. **Issues**: Apri una issue su GitHub per bug o richieste

---

*Creato con Claude Code - Sistema professionale per la generazione di contenuti e-learning*

