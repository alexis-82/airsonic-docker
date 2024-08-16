# Installazione di Airsonic con Docker Compose

Questa guida ti aiuterà a configurare e avviare un'istanza di Airsonic utilizzando Docker Compose.

## Prerequisiti

- Docker installato sul sistema [Guida Installazione Docker](https://docs.docker.com/get-docker/)
- Docker Compose installato [Guida Installazione Docker Compose](https://docs.docker.com/compose/install/)

## Passaggi per l'Installazione

### 1. Crea la struttura delle cartelle

Crea le cartelle necessarie per i volumi di Airsonic. Questo include la cartella dove verranno salvate le configurazioni, la musica, le playlist e i podcast.

```bash
mkdir -p /path/to/airsonic/data
mkdir -p /path/to/airsonic/musica
mkdir -p /path/to/airsonic/playlists
mkdir -p /path/to/airsonic/podcasts
```

Sostituisci `/path/to/airsonic/` con il percorso desiderato sul tuo sistema.

### 2. Crea un file `docker-compose.yml`

Crea un file chiamato `docker-compose.yml` nella directory in cui vuoi configurare Airsonic. Puoi utilizzare il seguente contenuto come base:

```yaml
services:
  airsonic:
    image: airsonic/airsonic
    container_name: airsonic
    volumes:
      - /path/to/airsonic/data:/airsonic/data
      - /path/to/airsonic/musica:/airsonic/music
      - /path/to/airsonic/playlists:/airsonic/playlists
      - /path/to/airsonic/podcasts:/airsonic/podcasts
    ports:
      - "4040:4040"
    restart: unless-stopped

volumes:
  data:
  playlists:
  podcasts:
```

### 3. Configura i Permessi

Assicurati che le directory per la musica, le playlist e i podcast abbiano i permessi corretti per essere accessibili dal contenitore Docker. Esempio:

```bash
chmod 755 /path/to/airsonic/musica
chmod 644 /path/to/airsonic/musica/*
```

### 4. Avvia Airsonic con Docker Compose

Posizionati nella directory dove si trova il file `docker-compose.yml` e avvia il servizio:

```bash
docker-compose up -d
```

Questo comando avvierà Airsonic in background.

### 5. Accedi a Airsonic

Una volta che il contenitore è in esecuzione, puoi accedere a Airsonic tramite il browser all'indirizzo:

```
http://localhost:4040
```

Se stai usando una macchina remota, sostituisci `localhost` con l'indirizzo IP o il nome del dominio della macchina.

### 6. Configurazione Iniziale

Al primo accesso, Airsonic ti guiderà attraverso la configurazione iniziale. Assicurati di specificare la cartella `/airsonic/music` per la libreria musicale durante la configurazione.

### 7. Gestione del Contenitore

Puoi gestire l'istanza di Airsonic con i seguenti comandi Docker Compose:

- **Avviare Airsonic**: `docker-compose up -d`
- **Fermare Airsonic**: `docker-compose down`
- **Visualizzare i log**: `docker-compose logs -f`

### 8. Aggiornamenti

Per aggiornare Airsonic all'ultima versione:

```bash
docker-compose pull
docker-compose up -d
```

### Risoluzione dei Problemi

- **Errore "Folder not found"**: Assicurati che le directory locali siano montate correttamente e che i permessi siano corretti.
- **Accesso al contenitore**: Per eseguire il debug all'interno del contenitore, usa il comando:
  
  ```bash
  docker exec -it airsonic /bin/bash
  ```

---

# Installazione di Airsonic con Docker Compose V2

Questa guida ti mostrerà come installare Airsonic su Ubuntu 24.04 utilizzando Docker Compose V2. Sono inclusi i passaggi necessari per configurare l'ambiente Docker specificamente su Ubuntu 24.04.

## Prerequisiti

- Ubuntu 24.04 installato.
- Accesso root o privilegi `sudo`.
- Docker e Docker Compose installati.

## 1. Aggiorna il Sistema

Assicurati che il tuo sistema sia aggiornato:

```bash
sudo apt update && sudo apt upgrade -y
```

## 2. Installa Docker Compose V2

Ubuntu 24.04 potrebbe avere una versione leggermente diversa di Docker rispetto a versioni precedenti. Installa Docker seguendo questi passaggi:

1. Installa Docker:

    ```bash
    sudo apt install docker.io docker-compose-v2
    ```

6. Verifica l'installazione di Docker:

    ```bash
    sudo systemctl status docker
    ```

## 3. Verifica installazione Docker Compose V2

Verifica l'installazione di Docker Compose:

```bash
docker compose version
```

## 4. Configura le Cartelle per Airsonic

Crea le cartelle necessarie per i volumi di Airsonic:

```bash
mkdir -p /path/to/airsonic/data
mkdir -p /path/to/airsonic/musica
mkdir -p /path/to/airsonic/playlists
mkdir -p /path/to/airsonic/podcasts
```

Assicurati che i permessi siano corretti:

```bash
sudo chmod 755 /path/to/airsonic/musica
sudo chown -R $USER:$USER /path/to/airsonic/airsonic/
```

## 5. Crea un file `docker-compose.yml`

Nella directory `/path/to/airsonic/airsonic`, crea un file `docker-compose.yml`:

```yaml
services:
  airsonic:
    image: airsonic/airsonic
    container_name: airsonic
    volumes:
      - /path/to/airsonic/data:/airsonic/data
      - /path/to/airsonic/musica:/airsonic/music
      - /path/to/airsonic/playlists:/airsonic/playlists
      - /path/to/airsonic/podcasts:/airsonic/podcasts
    ports:
      - "4040:4040"
    restart: unless-stopped

volumes:
  data:
  playlists:
  podcasts:
```

## 6. Avvia Airsonic con Docker Compose

Spostati nella directory dove si trova il file `docker-compose.yml` ed esegui il comando per avviare Airsonic:

```bash
cd /path/to/airsonic/airsonic
sudo docker compose up -d
```

Questo comando avvierà Airsonic in background.

## 7. Configura il Firewall

Ubuntu 24.04 ha `ufw` abilitato di default. Consenti il traffico sulla porta 4040:

```bash
sudo ufw allow 4040/tcp
```

## 8. Accedi a Airsonic

Una volta che il contenitore è in esecuzione, apri il browser e vai all'indirizzo:

```
http://localhost:4040
```

Oppure, sostituisci `localhost` con l'indirizzo IP del tuo server se stai lavorando su una macchina remota.

## 9. Configurazione Iniziale

Al primo accesso, Airsonic ti guiderà attraverso la configurazione iniziale. Specifica `/airsonic/music` come percorso per la tua libreria musicale.

## 10. Gestione di Airsonic

- **Avviare Airsonic**: `sudo docker compose up -d`
- **Fermare Airsonic**: `sudo docker compose down`
- **Visualizzare i log**: `sudo docker compose logs -f`

## 11. Aggiornamento di Airsonic

Per aggiornare Airsonic:

```bash
cd /path/to/airsonic/airsonic
sudo docker compose pull
sudo docker compose up -d
```
