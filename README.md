# Labtainers Modern — istruzioni per gli studenti

Questo repository distribuisce laboratori modernizzati per il corso di **Cyber Security e Digital Forensics**, utilizzabili sulla **VM ufficiale Labtainers** fornita agli studenti.

I laboratori sono basati su Ubuntu 24.04 e includono strumenti aggiornati per l'analisi delle vulnerabilità e la sicurezza dei sistemi.

Non è necessario installare Docker separatamente, compilare immagini Docker o disporre di un account GitHub.

## Laboratori disponibili

| Laboratorio | Argomento | Release IModule |
|---|---|---|
| `bufoverflow-modern` | Buffer overflow, analisi della memoria e tecniche di exploit | `v1.0.1` |
| `buf64-modern` | Buffer overflow su architettura x86-64 ed esecuzione di shellcode | `buf64-modern-v1.0.1` |

### bufoverflow-modern

Laboratorio dedicato allo studio delle vulnerabilità di buffer overflow e delle tecniche di analisi e sfruttamento della memoria.

**Ambiente:** Ubuntu 24.04.5 LTS, GCC 13, GDB 15.1, pwndbg e Pwntools.

**Immagine Docker pubblica:**

`ghcr.io/cybersecurity-teaching-labs/bufoverflow-modern.bufoverflow.student:latest`

### buf64-modern

Laboratorio dedicato allo sfruttamento di buffer overflow su architettura x86-64, con l'obiettivo di eseguire shellcode e ottenere una shell non privilegiata.

**Ambiente:** Ubuntu 24.04 LTS, GCC 13, GDB 15.1, pwndbg, Pwntools e NASM.

La dimensione del buffer vulnerabile è parametrizzata individualmente da Labtainers.

**Immagine Docker pubblica:**

`ghcr.io/cybersecurity-teaching-labs/buf64-modern.buf64.student:latest`

## 1. Installazione dei laboratori

L'installazione deve essere effettuata una sola volta per ciascun laboratorio.

Aprire un terminale nella VM ufficiale Labtainers e posizionarsi nella directory:

```bash
cd ~/labtainer/trunk/scripts/labtainer-student
```

### Installazione di bufoverflow-modern

**1. Installare l'IModule:**

```bash
./bin/imodule https://github.com/cybersecurity-teaching-labs/labtainers-distribution/releases/download/v1.0.1/bufoverflow-modern-imodule-v1.0.1.tar
```

**2. Scaricare l'immagine Docker:**

```bash
docker pull ghcr.io/cybersecurity-teaching-labs/bufoverflow-modern.bufoverflow.student:latest
```

### Installazione di buf64-modern

**1. Installare l'IModule:**

```bash
./bin/imodule https://github.com/cybersecurity-teaching-labs/labtainers-distribution/releases/download/buf64-modern-v1.0.1/buf64-modern-imodule-v1.0.1.tar
```

**2. Scaricare l'immagine Docker:**

```bash
docker pull ghcr.io/cybersecurity-teaching-labs/buf64-modern.buf64.student:latest
```

### Note sull'installazione

Le immagini Docker sono pubbliche e non richiedono autenticazione a GitHub Container Registry.

Il download può richiedere alcuni minuti, a seconda della velocità della connessione e delle immagini già presenti sulla VM.

**Il comando `docker pull` è necessario per garantire la compatibilità con la versione di Labtainers fornita per il corso**, che potrebbe non individuare automaticamente le immagini ospitate su GHCR.

Dopo il primo download, non è necessario ripetere l'operazione per ogni avvio del laboratorio.

Non utilizzare `docker build`, `docker login` o altri comandi di configurazione Docker, salvo indicazione esplicita del docente.

## 2. Avvio dei laboratori

Aprire un terminale nella VM ufficiale:

```bash
cd ~/labtainer/trunk/scripts/labtainer-student
```

### Avvio di bufoverflow-modern

```bash
./bin/labtainer bufoverflow-modern
```

Si aprirà il terminale del container `ubuntu@bufoverflow`.

### Avvio di buf64-modern

```bash
./bin/labtainer buf64-modern
```

Si aprirà il terminale del container `ubuntu@buf64`.

Seguire le istruzioni disponibili nel manuale dell'esercitazione.

Tutte le attività devono essere svolte esclusivamente nell'ambiente didattico predisposto.

## 3. Svolgimento delle esercitazioni

Ogni laboratorio contiene programmi e strumenti necessari allo svolgimento dell'attività.

Per consultare la documentazione, utilizzare il manuale reso disponibile da Labtainers all'avvio.

### Strumenti disponibili

A seconda del laboratorio, sono disponibili:

- GCC per la compilazione dei programmi C.
- GDB e pwndbg per l'analisi dinamica e il debugging.
- Pwntools per lo sviluppo e l'analisi di exploit.
- NASM per l'assemblaggio di codice x86-64.

Le configurazioni dei laboratori sono predisposte per consentire lo studio controllato delle vulnerabilità.

Non modificare le impostazioni globali di sicurezza della VM, del kernel o di Docker.

## 4. Chiusura del laboratorio e salvataggio della consegna

Al termine dell'esercitazione, uscire dalla shell del laboratorio, se necessario:

```bash
exit
```

Tornare al terminale della VM ufficiale e posizionarsi nella directory:

```bash
cd ~/labtainer/trunk/scripts/labtainer-student
```

Eseguire:

```bash
./bin/stoplab
```

Labtainers arresta il laboratorio e salva automaticamente i risultati.

Il percorso dei risultati viene visualizzato al termine dell'operazione.

### Risultati di bufoverflow-modern

Directory:

```text
/home/student/labtainer_xfer/bufoverflow-modern
```

Verificare il file di consegna:

```bash
ls -lh ~/labtainer_xfer/bufoverflow-modern/*.lab
```

### Risultati di buf64-modern

Directory:

```text
/home/student/labtainer_xfer/buf64-modern
```

Verificare il file di consegna:

```bash
ls -lh ~/labtainer_xfer/buf64-modern/*.lab
```

### Consegna

**Consegnare il file con estensione `.lab`**, seguendo le istruzioni comunicate dal docente.

Non estrarre, rinominare o modificare il contenuto del file `.lab`.

Non consegnare gli archivi ZIP contenuti al suo interno.

## 5. Problemi comuni

### Il comando `labtainer` non trova l'immagine Docker

Messaggi possibili:

```text
Unable to reach DockerHub
Could not find image info
```

Verificare di avere eseguito il comando `docker pull` relativo al laboratorio.

Per controllare le immagini disponibili:

```bash
docker image ls
```

Se l'immagine manca, ripetere il download indicato nella sezione di installazione.

### Docker restituisce `unauthorized` oppure `denied`

Verificare la connessione Internet e che il nome dell'immagine sia stato copiato correttamente.

Le immagini distribuite per il corso sono pubbliche: non è necessario eseguire `docker login`.

Se il problema persiste, conservare il messaggio completo e contattare il docente.

### Il laboratorio non è riconosciuto

Verificare di avere installato l'IModule corretto.

Per visualizzare gli IModule registrati:

```bash
cd ~/labtainer/trunk/scripts/labtainer-student
./bin/imodule -l
```

Se necessario, reinstallare l'IModule utilizzando l'URL indicato nella sezione di installazione.

### `stoplab` segnala l'assenza di `instr_config/results.config`

L'IModule potrebbe essere incompleto o non aggiornato.

Reinstallare la versione indicata per il laboratorio e ripetere l'operazione.

### Non viene generato il file `.lab`

Verificare l'output di `stoplab` e la directory `~/labtainer_xfer/`.

Non eliminare manualmente i container e non modificare i risultati.

Conservare l'errore completo e contattare il docente.

### Problemi con GDB o pwndbg

Utilizzare gli strumenti già installati nel container.

Non reinstallare o aggiornare autonomamente pwndbg, GDB o le dipendenze Python.

Se GDB non si avvia correttamente, conservare il messaggio d'errore e segnalarlo al docente.

### Problemi con comandi multilinea

Il terminale Labtainers può interferire con particolari costruzioni della shell, inclusi alcuni here-document e comandi incollati su più righe.

Se un comando non viene interpretato correttamente, riprovare impartendo le istruzioni singolarmente.

## 6. Aggiornamenti

Utilizzare esclusivamente gli URL e le versioni comunicati dal docente.

Gli IModule sono distribuiti tramite release GitHub; le immagini Docker sono pubblicate su GitHub Container Registry.

Il tag Docker `latest` identifica la versione disponibile per l'utilizzo corrente, ma può cambiare nel tempo.

Non aggiornare autonomamente i laboratori durante lo svolgimento delle esercitazioni, salvo indicazione del docente.

## 7. Utilizzo autorizzato

I laboratori contengono programmi intenzionalmente vulnerabili e configurazioni appositamente predisposte per finalità didattiche.

Le tecniche di analisi e sfruttamento delle vulnerabilità devono essere utilizzate esclusivamente negli ambienti autorizzati del corso.

Non applicare queste tecniche a sistemi o servizi esterni senza esplicita autorizzazione.
