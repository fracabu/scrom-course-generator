# Guida: Aumentare Limite Upload File in Moodle

Il file video SCORM (52 MB) supera il limite di upload. Segui questa guida per aumentarlo.

## ⚠️ Requisiti

**Devi avere accesso amministratore a:**
- Moodle (come admin)
- Server web (accesso FTP/SSH)
- File di configurazione PHP

**Se NON hai accesso admin:** Contatta l'amministratore del server o usa soluzioni alternative (compressione video, YouTube).

---

## 🎯 Livello 1: Impostazioni Moodle (INIZIA QUI)

### Passo 1: Verifica Limite Attuale

1. **Accedi a Moodle** come amministratore
2. Vai su: **Amministrazione del sito** → **Sicurezza** → **Politiche del sito**
3. Cerca il campo: **Dimensione massima dei file caricati**
4. **Annotati il valore** (es. 16MB, 32MB, 50MB)

### Passo 2: Aumenta il Limite in Moodle

1. Nella stessa pagina (**Politiche del sito**)
2. Campo **"Dimensione massima dei file caricati"**
3. Seleziona dal menu a tendina: **100MB** (o superiore)
4. Clicca **"Salva modifiche"**

### Passo 3: Limite a Livello di Corso

1. Vai nel tuo corso
2. **Amministrazione del corso** → **Modifica impostazioni**
3. Cerca: **"Dimensione massima dei file caricati"**
4. Seleziona: **100MB** (o il massimo disponibile)
5. **Salva e visualizza**

### ⚠️ Se non vedi 100MB come opzione...

Il limite di Moodle dipende dal limite PHP del server. Passa al **Livello 2**.

---

## 🎯 Livello 2: Configurazione PHP

Il limite PHP è spesso il vero problema. Devi modificare `php.ini`.

### Metodo A: Accesso cPanel / Plesk (Hosting Condiviso)

**Se hai cPanel:**

1. Accedi al **cPanel**
2. Cerca **"Select PHP Version"** o **"MultiPHP INI Editor"**
3. Seleziona il dominio/cartella di Moodle
4. Modifica questi valori:
   ```
   upload_max_filesize = 100M
   post_max_size = 100M
   max_execution_time = 300
   max_input_time = 300
   memory_limit = 256M
   ```
5. **Salva le modifiche**

**Se hai Plesk:**

1. Accedi a **Plesk**
2. Vai su **Siti Web & Domini** → tuo dominio → **Impostazioni PHP**
3. Modifica:
   ```
   upload_max_filesize = 100M
   post_max_size = 100M
   max_execution_time = 300
   memory_limit = 256M
   ```
4. **Applica**

### Metodo B: Accesso FTP/SSH (Server Dedicato/VPS)

**Trova il file php.ini:**

```bash
# Su Linux, cerca php.ini
php -i | grep php.ini

# Percorsi comuni:
# /etc/php/7.4/apache2/php.ini
# /etc/php.ini
# /usr/local/etc/php/php.ini
```

**Modifica php.ini:**

1. Apri `php.ini` con un editor (nano, vi, o via FTP)
2. Cerca e modifica queste righe:

```ini
; TROVA QUESTE RIGHE E MODIFICA I VALORI

upload_max_filesize = 100M
post_max_size = 100M
max_execution_time = 300
max_input_time = 300
memory_limit = 256M
max_file_uploads = 20
```

3. **Salva il file**
4. **Riavvia il web server:**

```bash
# Apache
sudo service apache2 restart
# oppure
sudo systemctl restart apache2

# Nginx con PHP-FPM
sudo service php7.4-fpm restart
sudo service nginx restart
```

### Metodo C: File .htaccess (Solo Apache)

Se non hai accesso a php.ini, prova a creare/modificare `.htaccess` nella root di Moodle:

1. Vai nella cartella principale di Moodle (via FTP)
2. Cerca il file `.htaccess` (potrebbe essere nascosto)
3. Apri o crea `.htaccess` e aggiungi:

```apache
# Aumenta limiti PHP
php_value upload_max_filesize 100M
php_value post_max_size 100M
php_value max_execution_time 300
php_value max_input_time 300
php_value memory_limit 256M
```

4. **Salva** e prova a ricaricare

⚠️ **Nota:** Questo metodo NON funziona sempre (dipende dalla configurazione del server).

---

## 🎯 Livello 3: Verifica le Modifiche

### Passo 1: Controlla Info PHP

Crea un file `phpinfo.php` nella root di Moodle:

```php
<?php
phpinfo();
?>
```

Aprilo nel browser: `https://tuosito.com/moodle/phpinfo.php`

Cerca queste voci:
- ✅ `upload_max_filesize` → deve essere ≥ 100M
- ✅ `post_max_size` → deve essere ≥ 100M
- ✅ `max_execution_time` → deve essere ≥ 300
- ✅ `memory_limit` → deve essere ≥ 256M

⚠️ **Elimina phpinfo.php dopo il controllo** (per sicurezza!)

### Passo 2: Prova l'Upload

1. Torna in Moodle
2. Vai in **Amministrazione del sito** → **Sicurezza** → **Politiche del sito**
3. Controlla se ora il menu mostra **100MB** come opzione
4. Se sì, selezionalo e **salva**
5. Prova a caricare il file video SCORM (52 MB)

---

## ✅ Soluzione Rapida (Se Non Hai Accesso)

Se **NON hai accesso amministratore** al server:

### Opzione 1: Contatta l'Admin
Invia questa email al tuo amministratore:

```
Oggetto: Richiesta Aumento Limite Upload Moodle

Salve,

Ho bisogno di caricare file SCORM di circa 50-100 MB nel corso Moodle.
Attualmente il limite è di [X] MB.

Potreste aumentare i seguenti parametri?

- upload_max_filesize = 100M
- post_max_size = 100M
- max_execution_time = 300
- memory_limit = 256M

Grazie!
```

### Opzione 2: Comprimi il Video

Ti creo uno script per comprimere il video da 52MB a circa 15-20MB:

```bash
# Usa ffmpeg per comprimere
ffmpeg -i Demistificare_l_IA.mp4 -vcodec h264 -crf 28 -preset fast Demistificare_l_IA_compressed.mp4
```

Vuoi che ti aiuti con la compressione?

### Opzione 3: Video Esterno (YouTube/Vimeo)

Carica il video su YouTube e creo un SCORM leggero (< 1MB) che lo incorpora.

---

## 📊 Valori Consigliati per Moodle

Per un Moodle performante con supporto file multimediali:

| Parametro | Valore Minimo | Valore Consigliato |
|-----------|---------------|-------------------|
| `upload_max_filesize` | 64M | 100M - 200M |
| `post_max_size` | 64M | 100M - 200M |
| `max_execution_time` | 300 | 600 |
| `max_input_time` | 300 | 600 |
| `memory_limit` | 128M | 256M - 512M |

---

## 🐛 Troubleshooting

### Problema: Modifiche non hanno effetto

**Soluzioni:**
1. Assicurati di aver modificato il file php.ini **corretto** (potrebbero essercene più di uno)
2. **Riavvia il web server** (Apache/Nginx)
3. **Svuota la cache** di Moodle: Amministrazione → Purge all caches
4. Verifica con `phpinfo()` che le modifiche siano attive

### Problema: Errore 500 dopo modifica .htaccess

**Soluzione:**
- Il server non supporta override PHP via .htaccess
- Rimuovi le righe aggiunte al `.htaccess`
- Devi modificare `php.ini` direttamente

### Problema: Upload si blocca/timeout

**Soluzione:**
- Aumenta `max_execution_time` e `max_input_time` a 600 o più
- Verifica la connessione internet (upload lento)
- Prova con file più piccolo per testare

---

## 📞 Hai Bisogno di Aiuto?

**Dimmi:**
1. Hai accesso amministratore al server? (Sì/No)
2. Che tipo di hosting usi? (cPanel, Plesk, VPS, Dedicato, Cloud)
3. Preferisci comprimere il video invece?

Posso aiutarti con qualsiasi metodo! 🚀
