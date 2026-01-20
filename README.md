# Actions-Giaffreda

## Spiegazione del workflow GitHub Actions

Qui trovi una spiegazione didattica del file [`.github/workflows/github_actions_demo.yaml`](.github/workflows/github_actions_demo.yaml) presente nel repository.

Obiettivo: illustrare le principali sezioni del file YAML, cosa fanno e la loro sintassi, con esempi tratti dal workflow.

**Nome e descrizione**
- **`name`**: nome leggibile del workflow (es. "GitHub Actions Demo").
- **`run-name`**: stringa opzionale che appare nelle esecuzioni; può includere espressioni `${{ ... }}` per inserire valori dinamici (es. `${{ github.actor }}`).

**Trigger**
- **`on`**: definisce quando il workflow viene eseguito. Nel file di esempio è `push`, quindi il workflow parte ogni volta che viene effettuato un push sul repository.

**Jobs**
- **`jobs`**: contenitore di uno o più job (unità di lavoro eseguite su runner separati). Ogni job ha un identificatore (es. `Explore-GitHub-Actions`).
- All'interno di un job:
	- **`runs-on`**: specifica il tipo di runner (es. `ubuntu-latest`).
	- **`steps`**: lista di passi (step) eseguiti sequenzialmente.

**Steps (passi)**
- Ogni elemento in `steps` può avere:
	- **`name`**: descrizione leggibile dello step.
	- **`uses`**: richiama un'azione pubblica o locale (es. `actions/checkout@v4`). La sintassi è `owner/action@version`.
	- **`run`**: comandi shell eseguiti sulrunner. Può essere una singola riga o un blocco multilinea usando `|`.

Esempio pratico dal file:
- `Display trigger info` (step con `run` multilinea): stampa informazioni dinamiche usando espressioni come `${{ github.event_name }}`, `${{ runner.os }}`, `${{ github.ref }}` e `${{ github.repository }}`.
- `Check out repository code` usa `actions/checkout@v4` per clonare il codice nel runner.
- `List files on the repository` esegue `ls ${{ github.workspace }}` per mostrare il contenuto della cartella di lavoro.

**Espressioni e variabili contestuali**
- La sintassi `${{ ... }}` valuta espressioni e inserisce valori runtime. Alcuni esempi utili dal workflow:
	- `${{ github.actor }}`: utente che ha scatenato l'evento.
	- `${{ github.event_name }}`: tipo di evento (es. `push`).
	- `${{ runner.os }}`: sistema operativo del runner.
	- `${{ github.ref }}`: riferimento git (es. branch o tag).
	- `${{ github.repository }}`: repository in formato `owner/repo`.
	- `${{ github.workspace }}`: path locale alla cartella di lavoro sul runner.
	- `${{ job.status }}`: stato corrente del job (utile per messaggi finali).

**Sintassi YAML importante**
- Indentazione: YAML è sensibile agli spazi; usa due spazi per livello (seguire lo stile del file).
- Liste: elementi preceduti da `-` (es. gli `steps`).
- Blocchi multilinea: usare `|` per i comandi `run` su più righe.

**Come leggere il flusso del workflow**
- 1) GitHub riceve un evento `push`.
- 2) Il workflow `GitHub Actions Demo` parte (nome e `run-name` mostrano informazioni dinamiche).
- 3) Viene eseguito il job `Explore-GitHub-Actions` sul runner `ubuntu-latest`.
- 4) Gli `steps` vengono eseguiti in ordine: stampa info, checkout del repo, messaggi, elenco file, e stampa dello stato finale.

Se vuoi, posso:
- integrare esempi aggiuntivi sulle espressioni `${{ }}` o
- tradurre questa spiegazione in un formato più didattico (slide o snippet con commenti riga per riga).
