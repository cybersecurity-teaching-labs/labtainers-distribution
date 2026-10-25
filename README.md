# Labtainers Modern — istruzioni per gli studenti

Queste istruzioni si applicano alla **VM ufficiale Labtainers** fornita per il corso. Non occorre installare Docker separatamente, compilare immagini o autenticarsi su GitHub Container Registry (GHCR).

## Laboratorio disponibile

- `bufoverflow-modern`: esercitazione di buffer overflow, basata su Ubuntu 24.04.5, con GDB 15.1, pwndbg e Pwntools.
- Release del modulo di installazione: **v1.0.1**.
- Immagine Docker pubblica: `ghcr.io/cybersecurity-teaching-labs/bufoverflow-modern.bufoverflow.student:latest`.

## Installazione (una volta sola)

Aprire un terminale nella VM ufficiale e lanciare:

```bash
cd ~/labtainer/trunk/scripts/labtainer-student
./bin/imodule https://github.com/cybersecurity-teaching-labs/labtainers-distribution/releases/download/v1.0.1/bufoverflow-modern-imodule-v1.0.1.tar
```

Il comando scarica le configurazioni del laboratorio. Al primo avvio, Labtainers scarica l'immagine Docker pubblica da GHCR: è necessaria una connessione Internet.

## Avvio

```bash
cd ~/labtainer/trunk/scripts/labtainer-student
./bin/labtainer bufoverflow-modern
```

Seguire le istruzioni dell'esercitazione nella finestra del container `ubuntu@bufoverflow`. Le esercitazioni si svolgono esclusivamente nell'ambiente didattico predisposto.

## Chiusura e salvataggio della consegna

Uscire dalla shell del laboratorio:

```bash
exit
```

Nel terminale della VM ufficiale:

```bash
cd ~/labtainer/trunk/scripts/labtainer-student
./bin/stoplab
```

Il sistema stampa il percorso dei risultati, normalmente:

```text
/home/student/labtainer_xfer/bufoverflow-modern
```

Verificare il file di consegna:

```bash
ls -lh ~/labtainer_xfer/bufoverflow-modern/*.lab
```

**Consegnare il file `.lab`** secondo la modalità indicata dal docente. Non consegnare lo ZIP interno e non rinominare o modificare il contenuto dell'archivio.

## Problemi comuni

- `Unable to reach DockerHub` / `Could not find image info`: controllare la connessione e che `start.config` riporti `REGISTRY ghcr.io/cybersecurity-teaching-labs` all'interno della sezione `CONTAINER bufoverflow`. Segnalare al docente se il problema persiste.
- `stoplab` non trova `instr_config/results.config`: l'IModule è mancante o non aggiornato; reinstallare la release v1.0.1 o contattare il docente.
- Non appare un file `.lab`: non cancellare il container; conservare l'errore completo e contattare il docente.
- Non lanciare `stoplab` da una directory arbitraria: utilizzare `~/labtainer/trunk/scripts/labtainer-student`.

## Aggiornamenti

Utilizzare soltanto l'URL e la release comunicati dal docente. La presenza di tag Docker `latest` non garantisce l'immutabilità dell'immagine.
