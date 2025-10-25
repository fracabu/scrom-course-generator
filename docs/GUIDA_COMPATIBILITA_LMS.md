# Guida alla Compatibilità con Diversi LMS

Questa guida spiega come importare i pacchetti SCORM 1.2 generati dal sistema su diverse piattaforme LMS.

## Cos'è SCORM 1.2?

SCORM (Sharable Content Object Reference Model) 1.2 è lo standard e-learning più utilizzato e affidabile. Pubblicato nel 2001, è supportato da praticamente tutti i sistemi LMS moderni.

**Vantaggi di SCORM 1.2**:
- **Compatibilità Universale**: Funziona su qualsiasi LMS che supporta SCORM
- **Affidabilità**: Standard maturo e testato da oltre 20 anni
- **Portabilità**: Un unico pacchetto funziona su tutte le piattaforme
- **Tracciamento**: Monitora progressi e completamento degli studenti
- **Offline-Ready**: Può essere visualizzato anche senza connessione

---

## Moodle

**Versioni supportate**: Tutte (dalla 1.9 in poi)

### Procedura di Import

1. **Accedi al corso** come docente/amministratore
2. **Attiva la modalità modifica**: Clicca "Attiva modifica" in alto a destra
3. **Aggiungi attività**:
   - Clicca "Aggiungi un'attività o una risorsa"
   - Seleziona "Pacchetto SCORM"
4. **Carica il file**:
   - Nome: Inserisci il titolo del corso
   - Descrizione: (opzionale) Descrivi il contenuto
   - File del pacchetto: Trascina il file .zip o usa "Scegli un file"
5. **Configura opzioni** (raccomandato):
   - Metodo di valutazione: "Punteggio più alto"
   - Numero massimo di tentativi: "Illimitato" (o come preferisci)
   - Forza nuovo tentativo: "Quando completato"
6. **Salva e visualizza**

### Problemi Comuni

**Upload fallisce (file troppo grande)**:
- Aumenta il limite in `php.ini`: `upload_max_filesize=100M` e `post_max_size=100M`
- Per XAMPP: Modifica tramite Control Panel → Config → PHP (php.ini)
- Riavvia Apache dopo le modifiche

**SCORM non si apre**:
- Verifica che il plugin SCORM sia abilitato: Amministrazione del sito → Plugin → Attività
- Controlla i permessi del file: deve essere leggibile dal web server

---

## Canvas

**Versioni supportate**: Tutte le versioni moderne di Canvas LMS

### Procedura di Import

1. **Accedi al corso** come istruttore
2. **Vai a Settings** (Impostazioni):
   - Clicca su "Settings" nella navigazione del corso
3. **Import Course Content**:
   - Clicca "Import Course Content"
   - Content Type: Seleziona "Common Cartridge 1.x Package" o "SCORM Package"
4. **Carica il pacchetto**:
   - Choose File: Seleziona il tuo file .zip SCORM
   - Opzioni: Lascia le impostazioni predefinite
5. **Import**: Clicca "Import"
6. **Verifica**: Vai su "Modules" per vedere il contenuto importato

### Note Canvas

- Canvas supporta SCORM 1.2 tramite il formato Common Cartridge
- Il contenuto apparirà come modulo separato
- Il tracciamento del completamento funziona automaticamente

### Problemi Comuni

**Import non funziona**:
- Verifica che il file .zip non sia corrotto
- Prova a ri-scaricare/rigenerare il pacchetto SCORM
- Contatta l'amministratore Canvas se il problema persiste

---

## Blackboard Learn

**Versioni supportate**: Blackboard Learn 9.x e superiori

### Procedura di Import

1. **Accedi al corso** come istruttore
2. **Vai a Content** (Contenuto):
   - Clicca "Content" nella navigazione
   - Scegli la sezione dove vuoi aggiungere il SCORM
3. **Build Content**:
   - Clicca "Build Content" (Crea contenuto)
   - Seleziona "Content Package (SCORM)"
4. **Upload del pacchetto**:
   - Name: Inserisci il nome del corso
   - Browse My Computer: Seleziona il file .zip
   - Opzioni: Configura come preferisci
5. **Submit**: Clicca "Submit"

### Configurazioni Consigliate

- **Make Available**: Seleziona per rendere visibile agli studenti
- **Track Number of Views**: Attiva per monitorare accessi
- **Open in New Window**: Consigliato per migliore esperienza utente

---

## Google Classroom

**Nota importante**: Google Classroom **non supporta nativamente SCORM**.

### Soluzioni Alternative

**Opzione 1 - SCORM Cloud (Consigliata)**:
1. Carica il tuo SCORM su [SCORM Cloud](https://cloud.scorm.com) (gratuito per uso limitato)
2. Ottieni il link di condivisione
3. In Google Classroom:
   - Crea nuovo "Materiale" o "Compito"
   - Aggiungi il link SCORM Cloud
   - Gli studenti possono accedere al contenuto

**Opzione 2 - Moodle Bridge**:
1. Usa Moodle come backend SCORM
2. Integra con Google Classroom tramite LTI (Learning Tools Interoperability)
3. Richiede configurazione tecnica

**Opzione 3 - Conversione a Google Slides/Sites**:
- Converti manualmente il contenuto in Google Slides o Google Sites
- Perde funzionalità SCORM (tracciamento, interattività)

---

## TalentLMS

**Versioni supportate**: Tutte

### Procedura di Import

1. **Accedi come amministratore/istruttore**
2. **Vai al corso**:
   - Clicca su "Courses"
   - Seleziona il corso o creane uno nuovo
3. **Add Content**:
   - Clicca "Add Content"
   - Seleziona "SCORM/AICC"
4. **Upload**:
   - Clicca "Upload SCORM Package"
   - Seleziona il file .zip
   - Attendi il caricamento
5. **Configura**:
   - Nome: Inserisci il titolo
   - Completion: Imposta criteri di completamento
6. **Save**

### Note TalentLMS

- Supporto eccellente per SCORM 1.2
- Tracciamento dettagliato dei progressi
- Funziona out-of-the-box senza configurazioni aggiuntive

---

## D2L Brightspace

**Versioni supportate**: Tutte le versioni moderne

### Procedura di Import

1. **Accedi al corso**
2. **Content** (Contenuto):
   - Clicca su "Content" nella navbar
3. **Upload/Create**:
   - Clicca "Upload/Create"
   - Seleziona "Upload SCORM Package"
4. **Upload del file**:
   - Seleziona il file .zip
   - Configura le opzioni di tracciamento
5. **Publish**: Rendi disponibile il contenuto

### Configurazioni Consigliate

- **Completion Tracking**: Attiva per monitorare progressi
- **Release Conditions**: (opzionale) Imposta prerequisiti
- **Availability**: Imposta date di disponibilità se necessario

---

## Schoology

**Versioni supportate**: Tutte

### Procedura di Import

1. **Accedi al corso**
2. **Add Materials**:
   - Clicca "Add Materials"
   - Seleziona "Add File/Link/External Tool"
3. **Upload SCORM**:
   - Scegli "File"
   - Carica il file .zip SCORM
   - Schoology lo riconoscerà automaticamente come SCORM
4. **Configura**:
   - Titolo e descrizione
   - Opzioni di completamento
5. **Save**

---

## Verificare la Compatibilità

Per verificare che il tuo pacchetto SCORM sia valido:

1. **Controlla la struttura del .zip**:
   ```
   pacchetto.zip
   ├── imsmanifest.xml  (DEVE essere nella root)
   ├── index.html
   └── [altri file]
   ```

2. **Valida con SCORM Cloud**:
   - Vai su [https://cloud.scorm.com](https://cloud.scorm.com)
   - Carica il tuo pacchetto (gratuito)
   - Testa il funzionamento
   - Se funziona lì, funzionerà ovunque

3. **Testa in locale**:
   - Estrai il .zip
   - Apri `index.html` in un browser
   - Verifica che il contenuto si carichi correttamente

---

## Risoluzione Problemi Comuni

### Il file .zip non viene riconosciuto come SCORM

**Causa**: `imsmanifest.xml` non è nella root del .zip

**Soluzione**:
1. Estrai il .zip
2. Verifica che `imsmanifest.xml` sia nella cartella principale
3. Se è in una sottocartella, sposta tutti i file un livello sopra
4. Ri-comprimi

### SCORM si apre ma non traccia i progressi

**Causa**: Problema di comunicazione SCORM API

**Soluzioni**:
- Verifica che il LMS supporti SCORM 1.2 (non solo 2004)
- Testa in un browser diverso (preferibilmente Chrome)
- Controlla la console JavaScript per errori (F12)
- Verifica che non ci siano popup blocker attivi

### Il contenuto appare senza stili/formattazione

**Causa**: File CSS non caricati correttamente

**Soluzioni**:
1. Verifica che tutti i file CSS siano inclusi nel .zip
2. Controlla i percorsi nei file HTML (devono essere relativi, non assoluti)
3. Rigenera il pacchetto SCORM con lo script aggiornato

### Upload fallisce (timeout)

**Causa**: File troppo grande o connessione lenta

**Soluzioni**:
- **Comprimi file multimediali**: Usa ffmpeg per ridurre dimensioni video/audio
- **Dividi il corso**: Crea SCORM separati per ogni modulo
- **Aumenta timeout LMS**: Contatta l'amministratore
- **Usa hosting esterno**: Carica video su YouTube/Vimeo e incorporali

---

## Best Practices

1. **Testa sempre prima di distribuire**:
   - Carica su SCORM Cloud per validazione
   - Testa su almeno 2 browser diversi
   - Verifica tracciamento completamento

2. **Ottimizza le dimensioni**:
   - Video: Max 50 MB per file (comprimi se necessario)
   - Audio: Max 10 MB per file
   - Totale pacchetto: Preferibilmente < 100 MB

3. **Mantieni compatibilità**:
   - Usa HTML5 standard (no tecnologie proprietarie)
   - Evita Flash, Java, ActiveX
   - Testa su mobile oltre che desktop

4. **Documenta il contenuto**:
   - Includi istruzioni per gli studenti
   - Specifica requisiti tecnici (browser, connessione)
   - Fornisci supporto per problemi comuni

---

## Risorse Utili

- **SCORM Cloud**: [https://cloud.scorm.com](https://cloud.scorm.com) - Testa gratuitamente i tuoi pacchetti
- **ADL SCORM**: [https://adlnet.gov/projects/scorm/](https://adlnet.gov/projects/scorm/) - Documentazione ufficiale
- **Rustici Software**: [https://rusticisoftware.com/](https://rusticisoftware.com/) - Risorse e strumenti SCORM

---

## Supporto

Se riscontri problemi con l'import su un LMS specifico:

1. Consulta la documentazione ufficiale del tuo LMS
2. Verifica che il pacchetto sia valido con SCORM Cloud
3. Contatta l'amministratore del tuo LMS
4. Controlla i log del browser (F12 → Console) per errori specifici

Per problemi con la generazione dei pacchetti SCORM, consulta `CLAUDE.md` o apri un issue nel repository del progetto.
