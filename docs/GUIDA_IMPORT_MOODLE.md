# Guida Importazione Corso AI in Moodle

## ⚠️ Soluzione Consigliata: Import in Corso Esistente

Se ricevi l'errore `restore_unknown_restore_type`, usa questo metodo alternativo:

### Passo 1: Crea un Corso Vuoto

1. **Accedi a Moodle** come amministratore o teacher con permessi

2. **Vai su:**
   - Amministrazione del sito → Corsi → Gestisci corsi e categorie
   - (Site administration → Courses → Manage courses and categories)

3. **Crea nuovo corso:**
   - Clicca "Crea nuovo corso" / "Create new course"

4. **Compila i dettagli:**
   - **Nome completo**: `Introduzione all'Intelligenza Artificiale per Principianti`
   - **Nome breve**: `AI-Principianti-2024`
   - **Categoria**: Seleziona o crea una categoria (es. "Tecnologia" o "AI")
   - **Formato corso**: **Topics** (Argomenti)
   - **Numero di sezioni**: **10**
   - **Data inizio**: Seleziona la data desiderata

5. **Salva**: Clicca "Salva e visualizza" / "Save and display"

### Passo 2: Ripristina il Backup nel Corso

1. **Entra nel corso** appena creato

2. **Vai su:**
   - Ingranaggio (⚙️) in alto a destra → **"Ripristina"** / **"Restore"**
   - Oppure: Altro → Ripristina (More → Restore)

3. **Carica il file:**
   - Clicca "Scegli un file" / "Choose a file"
   - Seleziona **`AI-Principianti-FIXED.mbz`**
   - Clicca "Ripristina" / "Restore"

4. **Conferma:**
   - Vedrai i dettagli del backup
   - Clicca "Continua" / "Continue"

5. **Destinazione:**
   - Seleziona **"Unisci il corso di backup a questo corso"** / **"Merge the backup course into this course"**
   - Oppure: **"Elimina i contenuti di questo corso e poi ripristina"** / **"Delete the contents of this course and then restore"** (consigliato se il corso è vuoto)
   - Clicca "Continua"

6. **Impostazioni:**
   - Assicurati che siano selezionati:
     - ✅ Includi attività e risorse
     - ✅ Includi contenuti utente (se richiesto)
   - Clicca "Continua"

7. **Schema:**
   - Rivedi cosa verrà importato
   - Clicca "Esegui ripristino" / "Perform restore"

8. **Completa:**
   - Attendi il completamento (30-90 secondi)
   - Clicca "Continua"
   - ✅ Il corso è pronto!

---

## 🔄 Metodo Alternativo: Import Diretto (se disponibile)

Alcune versioni di Moodle permettono l'import diretto:

1. **Crea corso vuoto** (come sopra)

2. **Entra nel corso**

3. **Vai su:**
   - Ingranaggio → **"Importa"** / **"Import"**

4. **Seleziona il file o altro corso**
   - Se c'è l'opzione di caricare file, usa `AI-Principianti-FIXED.mbz`
   - Altrimenti seleziona le attività da importare da un altro corso

---

## 📋 Metodo Manuale (Piano B)

Se nemmeno questo funziona, puoi importare manualmente il contenuto:

### 1. Usa il File Markdown

Hai a disposizione il file `course-content-edited.md` con tutto il contenuto del corso.

### 2. Crea Manualmente le Sezioni

Per ogni modulo (1-10):

1. **Aggiungi o modifica sezione**
2. **Titolo sezione**: Copia dal file markdown
3. **Aggiungi attività o risorsa**:
   - Per contenuti teorici → **Pagina**
   - Per esercizi → **Compito** (Assignment)
   - Per discussioni → **Forum**
   - Per quiz → **Quiz**

### 3. Copia il Contenuto

- Apri `course-content-edited.md` in un editor
- Copia e incolla il contenuto nelle rispettive attività
- Il markdown verrà convertito in HTML automaticamente da Moodle

---

## 🛠️ Troubleshooting

### Errore: "restore_unknown_restore_type"
→ Usa il metodo "Import in corso esistente" descritto sopra

### Errore: "Invalid backup file"
→ Verifica che il file non sia corrotto, ri-scaricalo se necessario

### Il corso appare vuoto dopo l'import
→ Controlla che le opzioni "Includi attività" e "Includi contenuti" fossero selezionate

### Alcune attività non sono importate
→ Verifica i permessi del tuo utente e le capacità del ruolo

### Caratteri italiani non visualizzati correttamente
→ Verifica che Moodle sia configurato con encoding UTF-8

---

## ✅ Verifica Post-Import

Dopo l'importazione, verifica:

1. **Tutte le 10 sezioni** sono presenti
2. **Ogni sezione contiene**:
   - Introduzione (Label)
   - Pagine di contenuto teorico
   - Attività (assignment, forum, quiz)
3. **Il contenuto** è formattato correttamente
4. **I caratteri italiani** (à, è, ì, ò, ù) sono visualizzati correttamente
5. **La navigazione** tra sezioni funziona

---

## 📞 Supporto

Se hai ancora problemi:

1. Verifica la **versione di Moodle** (il backup è per Moodle 4.x)
2. Controlla i **log di Moodle** per errori dettagliati
3. Verifica i **permessi** del tuo ruolo utente
4. Usa il metodo manuale come ultima risorsa

---

## 📂 File Disponibili

- **AI-Principianti-FIXED.mbz** (234 KB) - Backup Moodle completo
- **course-content-edited.md** (395 KB) - Contenuto testuale completo
- **course-outline.md** - Struttura del corso

Buona fortuna con l'importazione! 🎓
