# Diario di viaggio delle vacanze estive

Sviluppa una Web per la pianificazione e gestione del tuo viaggio.
Suddividi il viaggio in giornate in cui ogni giornata riporta le tappe da visitare.
Inserisci dettagli (titolo, descrizione, data etc), immagini, cibo, curiosità o qualsiasi altra info.
Le tappe del viaggio saranno anche visualizzate su mappa tramite un servizio a tua scelta.
Implementa una funzionalità per tenere traccia della progressione delle tappe del tuo viaggio (anche quando chiudi la pagina).
Aggiungi personalizzazioni e funzionalità a tuo piacimento.

## Svolgimento

Utilizzerò Laravel per l'intero svolgimento della web-app, sfruttando Blade per la visualizzazione utente.
La webapp sarà accessibile solo all'admin, momentaneamente non intendo gestire l'autenticazione di più utenti.
Il mio obiettivo (dopo aver effettuato l'accesso) sarà visualizzare una pagina di intereazione semplificata per leggere e navigare tra i contenuti.
Per la modifica o l'inserimento di nuovi viaggi inserirò una dashboard.

### Database

#### Tabelle

-   Travels (informazioni sui viaggi);
-   Days (giornate di un viaggio);
-   Stops (tappe di una giornata);
-   Notes (note aggiunte alle tappe);
-   Ratings (valutazioni delle tappe).

#### Relazioni

-   A travel has many days (un viaggio ha molte giornate);
-   A day has many stops (una giornata ha molte tappe);
-   A stop can have many notes and ratings (una tappa può avere molte note e valutazioni).

#### Struttura tabelle

##### 1. Travels (Viaggi)

| Campo         | Tipo         | Descrizione             |
| ------------- | ------------ | ----------------------- |
| `id`          | BIGINT       | Primary Key             |
| `title`       | VARCHAR(255) | Titolo del viaggio      |
| `description` | TEXT         | Descrizione del viaggio |
| `created_at`  | TIMESTAMP    | Data di creazione       |
| `updated_at`  | TIMESTAMP    | Data di aggiornamento   |

##### 2. Days (Giornate)

| Campo        | Tipo      | Descrizione            |
| ------------ | --------- | ---------------------- |
| `id`         | BIGINT    | Primary Key            |
| `travel_id`  | BIGINT    | Riferimento al viaggio |
| `date`       | DATE      | Data della giornata    |
| `created_at` | TIMESTAMP | Data di creazione      |
| `updated_at` | TIMESTAMP | Data di aggiornamento  |

##### 3. Stops (Tappe)

| Campo         | Tipo         | Descrizione               |
| ------------- | ------------ | ------------------------- |
| `id`          | BIGINT       | Primary Key               |
| `day_id`      | BIGINT       | Riferimento alla giornata |
| `title`       | VARCHAR(255) | Titolo della tappa        |
| `description` | TEXT         | Descrizione della tappa   |
| `latitude`    | DECIMAL(9,6) | Latitudine                |
| `longitude`   | DECIMAL(9,6) | Longitudine               |
| `created_at`  | TIMESTAMP    | Data di creazione         |
| `updated_at`  | TIMESTAMP    | Data di aggiornamento     |

##### 4. Notes (Note)

| Campo        | Tipo      | Descrizione            |
| ------------ | --------- | ---------------------- |
| `id`         | BIGINT    | Primary Key            |
| `stop_id`    | BIGINT    | Riferimento alla tappa |
| `content`    | TEXT      | Contenuto della nota   |
| `created_at` | TIMESTAMP | Data di creazione      |
| `updated_at` | TIMESTAMP | Data di aggiornamento  |

##### 5. Ratings (Valutazioni)

| Campo        | Tipo      | Descrizione            |
| ------------ | --------- | ---------------------- |
| `id`         | BIGINT    | Primary Key            |
| `stop_id`    | BIGINT    | Riferimento alla tappa |
| `rating`     | TINYINT   | Valutazione (1-5)      |
| `created_at` | TIMESTAMP | Data di creazione      |
| `updated_at` | TIMESTAMP | Data di aggiornamento  |
