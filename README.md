# SCORM Course Generator

Sistema professionale per la generazione di contenuti didattici in formato SCORM 1.2, compatibile con qualsiasi LMS (Learning Management System).

## Panoramica

Questo progetto utilizza un'architettura multi-agente basata su AI per creare contenuti didattici di alta qualità in formato SCORM 1.2, lo standard universale supportato da tutti i principali LMS. Il sistema divide il processo di creazione in fasi specializzate, ciascuna gestita da un agente dedicato.

**Compatibile con**:
- Moodle (tutte le versioni)
- Canvas
- Blackboard
- Google Classroom
- TalentLMS
- Schoology
- D2L Brightspace
- E qualsiasi LMS che supporta SCORM 1.2

## Caratteristiche Principali

- **Generazione Automatica**: Creazione completa di corsi e-learning da semplici outline
- **Formato SCORM 1.2**: Compatibilità universale con qualsiasi LMS
- **Qualità Professionale**: Contenuti pedagogicamente validi, grammaticalmente corretti e visivamente accattivanti
- **Supporto Multimediale**: Integrazione di audio e video con compressione intelligente
- **Multi-Agente**: Cinque agenti specializzati per workflow ottimizzato

## Architettura Agenti

Il sistema utilizza cinque agenti specializzati:

### 1. Course Outliner (Orange Agent)
Crea strutture di corso pedagogicamente valide partendo da argomenti generali.

**Input**: Intervista con obiettivi, audience, durata, livello
**Output**: Outline completo con moduli, argomenti e attività

### 2. Content Creator (Blue Agent)
Genera contenuti testuali dettagliati dall'outline strutturato.

**Input**: Outline del corso
**Output**: Contenuti completi in markdown (spiegazioni, istruzioni, esercizi)

### 3. Senior Editor (Red Agent)
Raffina e perfeziona i contenuti per qualità professionale.

**Responsabilità**:
- Correzione grammaticale e ortografica
- Validazione formattazione markdown/tabelle
- Miglioramento chiarezza e concisione
- Consistenza terminologica

### 4. SCORM Package Generator (Green Agent)
Converte i contenuti in pacchetti SCORM 1.2 pronti per qualsiasi LMS.

**Input**: Contenuti markdown
**Output**: Pacchetto SCORM .zip con HTML stilizzato e navigazione

### 5. Multimedia Integrator (Purple Agent)
Integra file audio/video nei pacchetti SCORM con ottimizzazione intelligente.

**Gestisce**:
- Analisi dimensioni e qualità
- Compressione file con ffmpeg
- Creazione SCORM multimediali standalone
- Suggerimenti hosting esterno per file grandi

## Struttura del Progetto

```
scorm-course-generator/
├── .claude/                          # Configurazione agenti Claude Code
├── scripts/                          # Script Python
│   ├── content_generation/          # Editing e generazione HTML
│   ├── scorm_generators/            # Generatori SCORM (package, audio, video)
│   └── legacy/                      # Script deprecati (per riferimento)
├── content/                         # Contenuti corsi
│   ├── ai-principianti/             # Corso AI per principianti
│   └── sicurezza-lavoro/            # Corso sicurezza sul lavoro
├── media/                           # File multimediali
│   ├── audio/                       # File audio (.m4a, .mp3, etc.)
│   └── video/                       # File video (.mp4, .webm, etc.)
├── output/                          # Output generati
│   ├── scorm/                       # Pacchetti SCORM .zip
│   └── mbz/                         # Backup Moodle .mbz (deprecato)
├── docs/                            # Documentazione
├── temp/                            # File temporanei (ignorati da git)
├── README.md                        # Questo file
└── CLAUDE.md                        # Istruzioni per Claude Code
```

## Quick Start

### 1. Creare un Nuovo Corso

Usa l'agente `course-outliner` per creare la struttura:

```python
# In Claude Code, invoca l'agente:
# Task tool con subagent_type="course-outliner"
```

### 2. Generare i Contenuti

Usa l'agente `content-creator` per scrivere i contenuti:

```python
# Task tool con subagent_type="content-creator"
```

### 3. Editare i Contenuti

Usa l'agente `senior-editor` per raffinare:

```python
# Task tool con subagent_type="senior-editor"
```

### 4. Creare il Pacchetto SCORM

```bash
python scripts/scorm_generators/create_scorm_package.py
```

Questo genera un file `.zip` in `output/scorm/` pronto per l'upload su qualsiasi LMS.

### 5. Importare nel tuo LMS

**Per Moodle**:
1. Vai al tuo corso Moodle
2. Clicca "Aggiungi un'attività o una risorsa"
3. Seleziona "Pacchetto SCORM"
4. Carica il file `.zip` generato
5. Salva e visualizza

**Per Canvas**:
1. Vai al tuo corso Canvas
2. Clicca su "Settings" → "Import Course Content"
3. Seleziona "SCORM Package" come tipo di contenuto
4. Carica il file `.zip` generato
5. Clicca "Import"

**Per Blackboard**:
1. Vai al tuo corso Blackboard
2. Clicca su "Content" → "Build Content" → "SCORM Package"
3. Carica il file `.zip` generato
4. Configura le opzioni e salva

**Per altri LMS**: Consulta la documentazione specifica del tuo LMS per l'importazione di pacchetti SCORM 1.2

## Integrazione Multimediale

### Audio

```bash
python scripts/scorm_generators/create_audio_scorm.py <file_audio> [titolo] [descrizione]
```

**Formati supportati**: MP3, WAV, OGG, M4A, AAC

### Video

```bash
python scripts/scorm_generators/create_video_scorm.py <file_video> [titolo] [descrizione]
```

**Formati supportati**: MP4, WEBM, MOV, AVI, MKV

### Compressione Video

Per file video di grandi dimensioni:

```bash
# Alta qualità (consigliato)
ffmpeg -i input.mp4 -vcodec libx264 -crf 23 -preset medium -acodec aac -b:a 128k output.mp4

# File più piccolo
ffmpeg -i input.mp4 -vcodec libx264 -crf 28 -preset fast -acodec aac -b:a 96k output.mp4
```

**Valori CRF**:
- 18-20: Qualità visivamente perfetta (file grande)
- 23: Alta qualità (consigliato)
- 28: Buona qualità, file piccolo
- 32: Qualità accettabile, file molto piccolo

## Linee Guida per la Qualità

- **Pedagogia**: Strutture basate su Bloom's Taxonomy, complessità progressiva
- **Accuratezza**: Contenuti fattuali, rilevanti e aggiornati
- **Engagement**: Varietà di attività, esempi del mondo reale
- **Accessibilità**: Linguaggio appropriato al livello target
- **Lingua Italiana**:
  - Accenti corretti (è, à, ò, ù, ì, più, però, già, può)
  - Tono informale "tu" consistente
  - Esempi culturalmente rilevanti (contesto italiano/europeo)
- **Tabelle**: Formattazione markdown corretta, HTML stilizzato
- **SCORM**: Conformità SCORM 1.2, compatibilità universale
- **Multimedia**: File ottimizzati, qualità preservata

## Documentazione

Consulta la cartella `docs/` per guide dettagliate:

- `GUIDA_IMPORT_MOODLE.md` - Procedura completa per importare contenuti in Moodle
- `GUIDA_AUMENTARE_LIMITE_UPLOAD_MOODLE.md` - Configurazione limiti upload in Moodle
- `ISTRUZIONI_IMPORT_SICUREZZA_SCORM.md` - Esempio di import corso sicurezza

Per altri LMS, i pacchetti SCORM generati sono compatibili con tutti i sistemi che supportano SCORM 1.2. Consulta la documentazione del tuo LMS specifico per le procedure di importazione.

## Requisiti

- Python 3.x
- ffmpeg (per compressione video/audio)
- Claude Code (per utilizzo agenti AI)

## Vantaggi di SCORM 1.2

SCORM 1.2 è lo standard e-learning più affidabile e compatibile:

- **Compatibilità Universale**: Funziona su qualsiasi LMS moderno
- **Affidabilità**: Standard maturo e stabile dal 2001
- **Tracciamento**: Supporta il tracciamento di completamento e progressi
- **Portabilità**: Un unico pacchetto funziona ovunque
- **Offline-Ready**: Può essere visualizzato anche localmente senza LMS

## Licenza

Questo progetto è stato creato per generare contenuti didattici di qualità professionale per qualsiasi piattaforma e-learning.

## Supporto

Per problemi o domande:
1. Controlla la documentazione in `docs/`
2. Verifica `CLAUDE.md` per istruzioni agenti
3. Consulta i file di esempio in `content/`
