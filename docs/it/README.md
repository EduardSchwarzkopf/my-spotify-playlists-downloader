# My Spotify Playlists Downloader

Esporta le informazioni delle tue playlist Spotify in file JSON per backup, analisi o migrazione.

---

## Descrizione

`my_spotify_playlists_downloader.py` è uno script Python da riga di comando progettato per aiutarti a esportare e fare
il backup delle tue playlist Spotify. Si connette al tuo account Spotify tramite OAuth e recupera tutte le tue playlist
insieme ai metadati dettagliati di ciascun brano. Puoi esportare le playlist come un singolo file JSON consolidato o
come file JSON individuali per ogni playlist.

Questo script è ideale per:

- Eseguire il backup dei dati della tua libreria musicale.
- Prepararti a migrare verso un altro servizio di musica.
- Analizzare le tue playlist per scopi personali o di ricerca.
- Imparare come integrare la Web API di Spotify usando Python.

Il progetto è rilasciato sotto licenza MIT ed è destinato a un uso educativo e personale.

---

## Funzionalità

- Esporta **tutte le playlist e i metadati dei brani**, inclusi nome, artisti, album, data di rilascio e altro.
- Opzione per **dividere l'output** in file JSON individuali per ogni playlist.
- Include **la posizione del brano nella playlist**, l'utente che lo ha aggiunto e la data di aggiunta.
- **Logging** sia su console che su file per la tracciabilità.
- **Portabile** – funziona su Windows, macOS e Linux.
- Configurazione semplice con dipendenze minime.

---

## Requisiti

- Python 3.7 o superiore
- Un [account sviluppatore Spotify](SPOTIFY_DEVELOPER_SETUP.md) per creare un'app e ottenere Client ID e Client Secret

Installa le dipendenze con:

```shell
pip install -r requirements.txt
```

---

## Configurazione

1. **Clona il repository**

    ```shell
    git clone https://github.com/yourusername/my_spotify_playlists_downloader.git
    cd my_spotify_playlists_downloader
    ```

2. **Crea il tuo file `.env`**

   Copia l'esempio fornito:

    ```shell
    cp .env.example .env
    ```

3. **Modifica `.env` e imposta le tue variabil**

   Obbligatorie:

    - `SPOTIFY_CLIENT_ID`
    - `SPOTIFY_CLIENT_SECRET`
    - `SPOTIFY_REDIRECT_URI` (deve corrispondere esattamente a quanto configurato nella tua app Spotify,
      es. <http://127.0.0.1:8888/callback>)

   Variabili opzionali:

    - `OUTPUT_DIR`: Directory dove verranno salvati gli output (default: ./playlists)
    - `OUTPUT_PREFIX_SPLIT`: Prefisso per i file in modalità divisa
    - `OUTPUT_PREFIX_SINGLE`: Prefisso per il file unico esportato
    - `LOG_DIR`: Directory dove verranno salvati i log (default: posizione dello script)
    - `LOG_LEVEL`: Livello di logging (default: INFO, può essere DEBUG, INFO, WARNING, ERROR, CRITICAL)

### Configurazione dell'account sviluppatore Spotify

Questo script richiede un account sviluppatore Spotify e le credenziali di un'app registrata.
Consulta [SPOTIFY_DEVELOPER_SETUP.md](SPOTIFY_DEVELOPER_SETUP.md) per istruzioni dettagliate.

---

## Utilizzo

### Esporta tutte le playlist in un singolo file JSON (default)

```shell
python my_spotify_playlists_downloader.py
```

### Esporta ogni playlist come file JSON individuale

```shell
python my_spotify_playlists_downloader.py --split
```

### Specifica una directory di output personalizzata

```shell
python my_spotify_playlists_downloader.py --output_dir ./my_exports
```

### Esporta solo una playlist specifica per nome

```shell
python my_spotify_playlists_downloader.py --playlist_name "Nome della mia playlist"
```

- Lo script esporterà solo la playlist il cui nome corrisponde (case-insensitive, normalizzato) al valore fornito.
- Se non ci sono corrispondenze, verrà registrato un errore e nessun file verrà esportato.

### Pulisci la cartella di output prima dell'esportazione

```shell
python my_spotify_playlists_downloader.py --clean_output
```

- Tutti i file JSON nella cartella di output verranno eliminati prima di esportare nuove playlist.
- Utile per evitare di mescolare esportazioni vecchie e nuove.

### Combina le opzioni

Puoi combinare queste opzioni secondo necessità. Ad esempio, per pulire la cartella di output ed esportare solo una
playlist specifica come file individuale:

```shell
python my_spotify_playlists_downloader.py --split --playlist_name "Nome della mia playlist" --clean_output
```

---

## Note aggiuntive

- I nomi delle playlist usati come nomi file vengono sanificati: caratteri non validi ed emoji vengono rimossi, ma si
  mantengono accenti e maiuscole/minuscole originali.
- Usando --playlist_name, lo script registra il filtro normalizzato e il numero di playlist da esportare.
- Usando --clean_output, lo script registra ogni file eliminato e conferma la pulizia della cartella.

---

## Esempio di Output

Ogni oggetto playlist esportato include:

- Nome playlist, ID, display name e username del proprietario, descrizione, snapshot_id
- Lista dei brani con:
  - Posizione nella playlist
  - Nome brano, artisti, album, data di rilascio dell'album
  - URL Spotify
  - Data di aggiunta alla playlist e utente che lo ha aggiunto

---

## Avviso

Questo script è fornito esclusivamente a scopo educativo.
Usalo responsabilmente con il tuo account Spotify.
L'autore non si assume alcuna responsabilità per un uso improprio o per eventuali perdite di dati causate dall'utilizzo.
Il codice è pulito e privo di componenti dannosi.

## Avviso sul Marchio Registrato

Spotify è un marchio registrato di Spotify AB.
Questo progetto **non è affiliato, sponsorizzato o approvato da Spotify** in alcun modo.
Tutti i riferimenti a Spotify sono effettuati esclusivamente a scopo informativo ed educativo.

Eventuali screenshot o immagini utilizzate in questa documentazione hanno solo scopo illustrativo per aiutare gli utenti
a configurare il proprio account sviluppatore e non implicano alcuna associazione con Spotify AB.

---

## Licenza

Questo progetto è rilasciato sotto [Licenza MIT](../../LICENSE).
