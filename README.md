# 🏐 Scout Volley

Web app per fare lo scout delle partite di pallavolo da iPad: azioni dei giocatori, punteggio, rotazioni, report con grafici e analisi nel tempo.

**App online:** https://manuelguatto.github.io/scout-volley/

Funziona offline (in palestra senza wifi) e non richiede account né server: i dati restano sul dispositivo.

## Installazione su iPad

1. Apri il link qui sopra in **Safari** (non Chrome).
2. Condividi → **Aggiungi alla schermata Home**.
3. Aprila una volta con internet: da lì in poi funziona anche offline.

Usa sempre l'icona sulla Home: l'app installata e Safari hanno archivi dati separati.

## Come si usa

### Squadra
Roster con numero, nome e ruolo (Palleggiatore, Banda, Opposto, Centrale, Libero). Il roster della squadra è già precaricato.

### Partita
1. **Nuova partita**: avversaria, data, casa/trasferta.
2. **Formazione** a inizio set: posizioni P1–P6, palleggiatore e chi batte per primo. La formazione titolare è già proposta.
3. **Scout**: 3 tocchi per azione → *giocatore* → *fondamentale* → *valutazione*.

| Valutazione | Significato |
|---|---|
| `#` | perfetto / punto |
| `+` | positivo |
| `!` | sufficiente |
| `-` | scarso |
| `/` | murato / slash |
| `=` | errore |

Il punto viene assegnato in automatico:
- **a noi**: ace (Battuta `#`), Attacco `#`, Muro `#`
- **agli avversari**: qualsiasi `=`, Attacco `/` (murato)

Per i punti senza azione registrata ci sono i tasti **+1 NOI** (errore avversario) e **+1 LORO** (punto avversario).

**Rotazioni**: indicate dalla posizione del palleggiatore (P1–P6). L'app ruota da sola sul side-out; i tasti *Ruota* e *Cambia battuta* servono per correzioni manuali.

**Libero**: si sceglie a inizio set ed entra in automatico al posto del centrale in seconda linea (P5 e P6); in P1 il centrale resta in campo per battere.

**Cambi** (anche del libero): 🔁 Cambio → tocca chi esce in campo → tocca chi entra dalla panchina.

**↶ Annulla** torna indietro di un'azione.

### Report (per partita)
- Statistiche individuali per fondamentale (positività ricezione, efficienza attacco, ace, muri…)
- Rendimento per rotazione: punti fatti/subiti, % side-out, % break, grafici a torta
- Settetti (6 di base + libero): quale combinazione subisce più e meno punti
- Attacchi e punti in attacco per ruolo
- Break subiti (3+ punti avversari di fila) con le rotazioni coinvolte
- Andamento del punteggio set per set

**Salva PDF / Stampa** genera il PDF del report.

### Analisi (più partite)
Andamento nel tempo di ricezione, attacco, side-out e break (squadra o singolo giocatore), rotazioni e settetti sull'intera stagione, totali per giocatore.

## Dati e backup

- **Salvataggio automatico**: ogni tocco viene salvato subito sul dispositivo. Se l'app si chiude, alla riapertura la partita riprende da dove era. L'orario dell'ultimo salvataggio è nel tabellone.
- **Backup su file (CSV)**: generato in automatico a *Fine set* (parziale) e *Fine partita* (completo), oppure in qualsiasi momento con 💾 *Backup*. Su iPad si salva in File / iCloud Drive.
- **Archivio**: esporta tutte le partite in CSV o importa un CSV (le partite già presenti vengono saltate). Serve anche per spostare i dati tra dispositivi.

⚠️ I dati vivono nel browser: cancellando i dati del sito si perdono. Il CSV è il vero backup — salvarlo dopo ogni partita.

### Formato CSV
Una riga per evento (`action`, `point`, `sub`):

```
match_id, date, opponent, venue, type, set, score_us, score_them, rotation, serve,
player_num, player_name, skill, grade, winner, sub_in_num, sub_in_name, lineup, ts
```

`lineup` = numeri dei 6 di base e del libero, es. `25-5-20-22-26-28+L42`.

## Struttura del progetto

| File | Contenuto |
|---|---|
| `index.html` | tutta l'app (HTML, CSS, JavaScript, nessuna dipendenza) |
| `sw.js` | service worker per l'uso offline |

Per aggiornare l'app basta modificare `index.html` e fare push su `main`: GitHub Pages pubblica la nuova versione e l'iPad la scarica alla prima apertura con internet, mantenendo i dati.
