# Guida Import SCORM - Corso Sicurezza sul Lavoro

## Pacchetto Generato

**File:** `sicurezza-lavoro-scorm.zip`
**Dimensione:** ~78 KB
**Formato:** SCORM 1.2 (compatibile con tutte le versioni di Moodle)
**Posizione:** `C:\Users\utente\moodle-agent-team\sicurezza-lavoro-scorm.zip`

---

## Contenuto del Corso

Il pacchetto SCORM contiene:

1. **Pagina Indice** - Panoramica del corso
2. **Modulo 1** - Rischio, Prevenzione e Organizzazione Aziendale (~55 KB)
3. **Modulo 2** - I Soggetti della Sicurezza e i Loro Ruoli (~75 KB)
4. **Modulo 3** - Protezione, Vigilanza e Formazione Continua (~111 KB)
5. **Test Finale** - 30 domande a scelta multipla (~30 KB)

**Durata totale stimata:** 4 ore + test finale

---

## ISTRUZIONI PER L'IMPORT IN MOODLE

### Passo 1: Accedi al Corso Moodle

1. Accedi alla tua piattaforma Moodle
2. Vai al corso dove vuoi aggiungere il pacchetto SCORM
3. Attiva la modalità modifica (pulsante "Attiva modifica")

### Passo 2: Aggiungi Attività SCORM

1. Clicca su **"Aggiungi un'attività o una risorsa"** nella sezione desiderata
2. Seleziona **"Pacchetto SCORM"** dall'elenco
3. Clicca su **"Aggiungi"**

### Passo 3: Carica il Pacchetto

1. Nella sezione **"Pacchetto"**, clicca su **"Scegli un file..."**
2. Carica il file: `sicurezza-lavoro-scorm.zip`
3. Compila i campi obbligatori:
   - **Nome:** Sicurezza sul Lavoro - Formazione Generale Lavoratori
   - **Descrizione:** Corso di formazione generale sulla sicurezza sul lavoro conforme al D.Lgs. 81/2008

### Passo 4: Configura Impostazioni SCORM

**Impostazioni consigliate:**

- **Metodo di classificazione:** Situazione di apprendimento
- **Numero massimo di tentativi:** 2 (per il test finale)
- **Forza nuovi tentativi:** No
- **Blocca tentativi dopo l'ultimo tentativo:** Sì
- **Visualizza informazioni su pacchetto:** Sì
- **Modalità finestra:** Corrente (o "Nuova finestra" se preferisci)
- **Larghezza/Altezza:** Default (100%)

**Tracciamento:**
- **Aggiorna i voti:** Ogni volta che si accede al pacchetto
- **Richiedi forzatamente visualizzato:** Sì
- **Stato di completamento automatico:** Richiedi voto

### Passo 5: Salva

1. Scorri in fondo alla pagina
2. Clicca su **"Salva e visualizza"**
3. Il pacchetto SCORM sarà immediatamente disponibile

---

## CARATTERISTICHE DEL PACCHETTO

### Funzionalità SCORM

- **Tracciamento progressi:** Ogni modulo viene segnato come completato quando visualizzato
- **Navigazione intuitiva:** Pulsanti Precedente/Successivo/Indice in ogni pagina
- **Responsive:** Funziona su desktop, tablet e smartphone
- **Tabelle stilizzate:** Tutte le tabelle sono formattate con CSS professionale
- **Colori tematici:** Rosso/arancione per richiamare l'attenzione sulla sicurezza

### Contenuti Formattati

- **Markdown to HTML:** Conversione automatica con supporto per:
  - Headers (H1, H2, H3, H4)
  - Bold, italic, strong emphasis
  - Liste ordinate e non ordinate
  - Tabelle con header e righe alternate
  - Paragrafi giustificati
  - Codice (se presente)
  - Tag `<details>` per contenuti collapsabili

### Compatibilità

- **SCORM 1.2:** Standard universale supportato da tutte le versioni di Moodle
- **Browser:** Chrome, Firefox, Safari, Edge (tutti i browser moderni)
- **Mobile:** Completamente responsive per smartphone e tablet

---

## VERIFICA POST-IMPORT

Dopo l'import, verifica che:

1. La pagina indice si apre correttamente
2. I 4 moduli sono visibili nell'indice
3. I pulsanti di navigazione funzionano (Precedente/Successivo/Indice)
4. Le tabelle sono visualizzate correttamente con colori alternati
5. Il test finale contiene tutte le 30 domande

**Test di navigazione:**
- Indice → Modulo 1 → Modulo 2 → Modulo 3 → Test Finale
- Test Finale → Indice
- Modulo 2 → Precedente (torna a Modulo 1)
- Modulo 2 → Successivo (va a Modulo 3)

---

## RISOLUZIONE PROBLEMI

### Errore: "File non valido"

**Causa:** Il file ZIP potrebbe essere corrotto o non conforme SCORM

**Soluzione:**
1. Verifica che il file sia `sicurezza-lavoro-scorm.zip` (non rinominato)
2. Verifica dimensione: ~78 KB
3. Rigenera il pacchetto con: `python create_sicurezza_scorm.py`

### Errore: "Pacchetto SCORM non trovato nel menu"

**Causa:** L'attività SCORM potrebbe non essere abilitata in Moodle

**Soluzione:**
1. Vai in **Amministrazione sito → Plugin → Moduli attività → Gestione moduli attività**
2. Verifica che "Pacchetto SCORM" sia abilitato (occhio aperto)
3. Se disabilitato, clicca sull'icona dell'occhio per abilitarlo

### Le tabelle non sono stilizzate

**Causa:** CSS non caricato correttamente

**Soluzione:**
- Le tabelle hanno classe `.data-table` con CSS inline, dovrebbero funzionare sempre
- Verifica con "Ispeziona elemento" nel browser che il CSS sia presente
- Prova a ricaricare la pagina (Ctrl+F5 per cache refresh)

### Navigazione non funziona

**Causa:** JavaScript SCORM non caricato

**Soluzione:**
1. Verifica che JavaScript sia abilitato nel browser
2. Nelle impostazioni SCORM, assicurati che "Forza JavaScript" sia impostato su "Sì"
3. Prova in modalità incognito/privata del browser

### Dimensioni file troppo grandi per l'upload

**Causa:** Limite upload di Moodle troppo basso (default 2 MB)

**Soluzione (XAMPP/Moodle locale):**
1. Apri XAMPP Control Panel
2. Clicca su "Config" → "PHP (php.ini)"
3. Cerca e modifica:
   ```ini
   upload_max_filesize=100M
   post_max_size=100M
   max_execution_time=300
   ```
4. Salva e riavvia Apache

**Soluzione (Moodle produzione):**
- Contatta l'amministratore di sistema per aumentare i limiti

---

## AMMINISTRAZIONE POST-IMPORT

### Monitoraggio Completamenti

Per verificare chi ha completato il corso:

1. Entra nel corso Moodle
2. Nel menu laterale vai su **"Rapporti" → "Completamento attività"**
3. Vedrai un riepilogo di quali studenti hanno completato ogni modulo

### Esportazione Risultati Test

Per esportare i risultati del test finale:

1. Entra nell'attività SCORM
2. Clicca su **"Rapporti"**
3. Seleziona gli utenti da esportare
4. Clicca su **"Scarica in formato Excel"** o **"CSV"**

### Backup del Pacchetto

**Consigliato:** Fai sempre un backup del file `.zip` originale

```bash
# Location del file originale
C:\Users\utente\moodle-agent-team\sicurezza-lavoro-scorm.zip

# Crea backup con data
copy sicurezza-lavoro-scorm.zip sicurezza-lavoro-scorm-2025-10-24.zip
```

---

## RIGENERAZIONE PACCHETTO

Se devi modificare i contenuti e rigenerare il pacchetto:

### 1. Modifica i File Sorgente

Modifica i file markdown:
- `modulo1-content.md`
- `modulo2-content.md`
- `modulo3-content.md`
- `test-finale.md`

### 2. Rigenera SCORM

```bash
cd C:\Users\utente\moodle-agent-team
python create_sicurezza_scorm.py
```

### 3. Sostituisci in Moodle

**Opzione A - Aggiorna pacchetto esistente:**
1. Entra nell'attività SCORM
2. Clicca su "Modifica impostazioni"
3. Nella sezione "Pacchetto", rimuovi il vecchio file
4. Carica il nuovo `sicurezza-lavoro-scorm.zip`
5. Salva

**Opzione B - Crea nuova attività:**
1. Crea una nuova attività SCORM con il pacchetto aggiornato
2. Nascondi o elimina la vecchia attività

---

## SUPPORTO E CONTATTI

**Script Python:** `create_sicurezza_scorm.py`

**File sorgenti:**
- Modulo 1: `modulo1-content.md`
- Modulo 2: `modulo2-content.md`
- Modulo 3: `modulo3-content.md`
- Test Finale: `test-finale.md`

**Output:**
- Pacchetto SCORM: `sicurezza-lavoro-scorm.zip`
- Directory temporanea: `scorm_package/`

**Documentazione:**
- D.Lgs. 81/2008: https://www.lavoro.gov.it
- SCORM 1.2 Spec: https://scorm.com/scorm-explained/technical-scorm/scorm-12/

---

## CHECKLIST IMPORT

- [ ] File `sicurezza-lavoro-scorm.zip` presente e integro
- [ ] Moodle accessibile e modalità modifica attiva
- [ ] Attività SCORM aggiunta al corso
- [ ] Pacchetto caricato correttamente
- [ ] Impostazioni configurate (tentativi, tracciamento)
- [ ] Pagina indice visualizzata correttamente
- [ ] Navigazione testata (Precedente/Successivo/Indice)
- [ ] Tutti i 4 moduli accessibili
- [ ] Tabelle formattate con colori
- [ ] Test finale con 30 domande visibile
- [ ] Tracciamento SCORM funzionante (check in Rapporti)

---

**Data creazione:** 24 Ottobre 2025
**Versione:** 1.0
**Formato:** SCORM 1.2
**Compatibilità:** Tutte le versioni di Moodle
