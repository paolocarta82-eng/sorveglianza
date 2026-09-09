# Copertura Rete — sorveglianza tecnica strade

PWA offline per la sorveglianza settimanale della rete stradale di Cagliari.
Il grafo (2.706 elementi, 593 km, UTM 32N) è incluso in `rete-grafo.js`.
Il GPS del telefono aggancia i punti agli elementi del grafo (map-matching a 25 m,
passaggio valido con l'80% delle celle da 40 m percorse) e li colora:
grigio = da rilevare, arancio = 1 passaggio su 2, verde = sorvegliato.

## Pubblicazione su GitHub Pages

1. Crea un repository (anche pubblico vuoto) e carica **il contenuto di questa cartella nella radice** del repo.
2. Settings → Pages → Source: `Deploy from a branch`, branch `main`, folder `/ (root)`.
3. Attendi la pubblicazione: l'indirizzo sarà `https://<utente>.github.io/<repo>/`.

HTTPS è obbligatorio: senza di esso Safari non concede la posizione.

## Installazione su iPhone

1. Apri l'indirizzo in **Safari** (non in altri browser).
2. Condividi → **Aggiungi alla schermata Home**.
3. Apri l'app dall'icona, premi **Avvia rilievo GPS** e concedi la posizione
   ("Consenti mentre usi l'app", precisione esatta attiva).
4. Tieni il telefono alimentato e l'app in primo piano: il blocco schermo viene
   richiesto automaticamente dove supportato.

## Dati

Tutto resta sul telefono (localStorage), suddiviso per settimana ISO.
Dalla schermata di chiusura giro esporti due CSV: copertura per elemento e anomalie.
"Chiudi la settimana e azzera" archivia la settimana e riparte da 0%.

## File

| file | ruolo |
|---|---|
| `index.html` | applicazione |
| `rete-grafo.js` | grafo stradale estratto dai GeoPackage |
| `support.js` | runtime di rendering |
| `sw.js` | service worker (cache offline `copertura-v4`) |
| `manifest.webmanifest`, `icona.png` | installazione come app |

Dopo ogni modifica a `index.html` incrementa `const C='copertura-vN'` in `sw.js`,
altrimenti i telefoni continuano a usare la versione in cache.
