# Labtainers Modern — istruzioni per gli studenti

Queste istruzioni si applicano alla **VM ufficiale Labtainers** fornita per il corso di Cyber Security e Digital Forensics.

Non occorre installare Docker separatamente, compilare immagini o autenticarsi su GitHub Container Registry (GHCR).

I laboratori utilizzano immagini Docker pubbliche, scaricate automaticamente da Labtainers al primo avvio.

## Laboratori disponibili

### 1. bufoverflow-modern

Esercitazione sul buffer overflow e sulle tecniche di sfruttamento delle vulnerabilità della memoria.

**Ambiente:**
- Ubuntu 24.04.5 LTS
- GCC 13, GDB 15.1
- pwndbg e Pwntools

**Release IModule:** `v1.0.1`

**Immagine Docker:**
`ghcr.io/cybersecurity-teaching-labs/bufoverflow-modern.bufoverflow.student:latest`

### 2. buf64-modern

Esercitazione sullo sfruttamento di un buffer overflow su architettura x86-64, finalizzata all'esecuzione di shellcode e all'ottenimento di una shell non privilegiata.

**Ambiente:**
- Ubuntu 24.04 LTS
- GCC 13, GDB 15.1
- pwndbg e Pwntools
- NASM
- Dimensione del buffer parametrizzata individualmente

**Release prevista IModule:** `buf64-modern-v1.0.1`

**Immagine Docker:**
`ghcr.io/cybersecurity-teaching-labs/buf64-modern.buf64.student:1.0.1`

## Installazione dei laboratori

L'installazione di ciascun laboratorio deve essere effettuata **una sola volta** sulla VM ufficiale Labtainers.

Aprire un terminale e posizionarsi nella directory:

```bash
cd ~/labtainer/trunk/scripts/labtainer-student
```

### Installazione di bufoverflow-modern

```bash
./bin/imodule https://github.com/cybersecurity-teaching-labs/labtainers-distribution/releases/download/v1.0.1/bufoverflow-modern-imodule-v1.0.1.tar
```

### Installazione di buf64-modern

*Da utilizzare dopo la pubblicazione dell'IModule v1.0.1.*

```bash
./bin/imodule https://github.com/cybersecurity-teaching-labs/labtainers-distribution/releases/download/buf64-modern-v1.0.1/buf64-modern-imodule-v1.0.1.tar
```

L'installazione scarica le configurazioni e la documentazione del laboratorio.

Al primo avvio Labtainers scarica automaticamente l'immagine Docker pubblica da GHCR. **È necessaria una connessione Internet.**

Non è richiesta alcuna compilazione locale delle immagini Docker.

## Avvio dei laboratori

Aprire un terminale nella VM ufficiale:

```bash
cd ~/labtainer/trunk/scripts/labtainer-student
```

Per avviare **bufoverflow-modern**:

```bash
./bin/labtainer bufoverflow-modern
```

Per avviare **buf64-modern**:

```bash
./bin/labtainer buf64-modern
```

Seguire le istruzioni dell'esercitazione nella finestra del relativo container.

In particolare:

- `bufoverflow-modern` utilizza il container `ubuntu@bufoverflow`.
- `buf64-modern` utilizza il container `ubuntu@buf64`.

I laboratori devono essere svolti esclusivamente nell'ambiente didattico predisposto.

## Chiusura e salvataggio della consegna

Al termine dell'esercitazione, uscire dalla shell del laboratorio, se necessario:

```bash
exit
```

Nel terminale della VM ufficiale eseguire:

```bash
cd ~/labtainer/trunk/scripts/labtainer-student
./bin/stoplab
```

Labtainers arresta il laboratorio e salva automaticamente i risultati.

Il percorso viene comunicato al termine dell'operazione.

Per **bufoverflow-modern**, normalmente:

```text
/home/student/labtainer_xfer/bufoverflow-modern
```

Per **buf64-modern**, normalmente:

```text
/home/student/labtainer_xfer/buf64-modern
```

Verificare la presenza del file di consegna.

Per `bufoverflow-modern`:

```bash
ls -lh ~/labtainer_xfer/bufoverflow-modern/*.lab
```

Per `buf64-modern`:

```bash
ls -lh ~/labtainer_xfer/buf64-modern/*.lab
```

**Consegnare il file `.lab`** attraverso la modalità indicata dal docente.

Non consegnare gli archivi ZIP interni e non rinominare o modificare il contenuto del file `.lab`.

## Problemi comuni

### Impossibile scaricare l'immagine Docker

Messaggi possibili:

```text
Unable to reach DockerHub
Could not find image info
unauthorized
```

Verificare la connessione Internet della VM.

I laboratori utilizzano GHCR e non richiedono credenziali GitHub. Se l'errore persiste, contattare il docente riportando il messaggio completo.

### Il laboratorio non viene riconosciuto

Verificare che il relativo IModule sia stato installato correttamente e che il nome del laboratorio sia scritto esattamente come indicato.

Se necessario, reinstallare l'IModule utilizzando l'URL della release comunicata dal docente.

### Errore relativo a instr_config/results.config

Se `stoplab` segnala l'assenza di `instr_config/results.config`, l'IModule potrebbe essere incompleto o non aggiornato.

Reinstallare la versione prevista per il laboratorio oppure contattare il docente.

### Non viene generato un file .lab

Non eliminare manualmente il container né modificare gli archivi di Labtainers.

Conservare il messaggio d'errore completo e contattare il docente.

### Comportamento anomalo del terminale

I terminali Labtainers possono gestire in modo particolare alcuni comandi multilinea e le sessioni interattive.

Quando possibile, impartire i comandi singolarmente, seguendo le istruzioni del laboratorio.

### Chiusura del laboratorio

Eseguire `./bin/stoplab` dalla directory:

```text
~/labtainer/trunk/scripts/labtainer-student
```

Non eseguirlo da directory arbitrarie.

## Aggiornamenti e versioni

Ogni laboratorio viene distribuito attraverso un IModule e un'immagine Docker associata.

Utilizzare **esclusivamente le versioni e gli URL comunicati dal docente**.

Non aggiornare autonomamente i container, gli strumenti di sviluppo o le dipendenze utilizzate durante l'esercitazione.

La presenza del tag Docker `latest` non garantisce che l'immagine rimanga invariata nel tempo.

## Note sull'ambiente didattico

Le esercitazioni prevedono programmi intenzionalmente vulnerabili e configurazioni di sicurezza predisposte per lo studio delle vulnerabilità.

Le tecniche illustrate devono essere utilizzate soltanto nei container e negli ambienti autorizzati per il corso.
