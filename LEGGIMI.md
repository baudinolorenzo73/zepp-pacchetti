# Cyber Lollo v1.0 - quadrante per Amazfit T-Rex 3 Pro 44mm

by Lollo ®2026

Quadrante cyberpunk: orario verde fluo, tre anelli (passi, batteria, battito),
bussola in alto che ruota quando ti giri, data, direzione e altitudine in basso.
Guarda `anteprima.png` per vedere come deve venire.

## Cosa contiene

| File / cartella | A cosa serve |
|---|---|
| `app.json` | Identità del quadrante (nome, versione, dispositivi) |
| `app.alternativo.json` | Versione di riserva di `app.json` (vedi "Se `zeus` dà errore") |
| `watchface/index.js` | Il codice: legge i sensori e aggiorna lo schermo |
| `assets/default.r/` | Immagini: sfondo, cifre verdi, anello bussola, icona |
| `assets/t-rex3pro-44/` | Copia delle stesse immagini, serve solo con `app.alternativo.json` |

## Come installarlo sull'orologio (a ogni passo spiego cosa fa)

Servono: un computer con **Node.js**, l'app **Zepp** sul telefono con l'orologio collegato, e la modalità sviluppatore già attiva (come per le tue altre app).

1. Apri il terminale **dentro la cartella `watchface-cyberpunk-lollo`** (quella che contiene `app.json`).
   Se il comando successivo dice "file non trovato", sei nella cartella sbagliata.

2. Installa lo strumento Zepp, una volta sola:
   ```
   npm i -g @zeppos/zeus-cli
   ```
   *Cosa fa:* scarica `zeus`, il programma ufficiale che prepara i quadranti. Se lo hai già, salta questo passo.

3. Accedi con il tuo account Zepp, una volta sola:
   ```
   zeus login
   ```
   *Cosa fa:* apre il browser per il login. Dopo, il terminale scrive che sei dentro.

4. Genera il QR code:
   ```
   zeus preview
   ```
   *Cosa fa:* impacchetta il quadrante e mostra un **QR code** nel terminale.
   *Cosa aspettarti:* alcune righe di avanzamento e poi il QR. Se chiede di scegliere un dispositivo, scegli il T-Rex 3 Pro.

5. Scansiona il QR con l'app Zepp (la stessa funzione che usi per le altre tue app).
   Dopo l'installazione, sull'orologio tieni premuto il quadrante attuale, scorri fino a **Cyber Lollo** e toccalo.

## Se `zeus` dà errore

- **Errore su `app.json`** (per esempio "platforms" o "designWidth"): in questa cartella cancella `app.json`
  e rinomina `app.alternativo.json` in `app.json`, poi rilancia `zeus preview`.
  Se dà ancora errore, **incollami il messaggio completo** e lo correggo.
- **Il QR si genera ma l'app dice "non compatibile"**: forse hai il modello 48mm.
  Dimmelo e rifaccio le misure per 480×480.

## Cosa non ho potuto provare (sii preparato)

Non ho potuto provare il quadrante su un orologio vero. Queste parti vanno verificate da te:

- **Bussola:** si aggiorna una volta al secondo (`COMPASS_MS` in `watchface/index.js`).
  Se l'anello non gira, o gira al contrario, dimmelo.
- **Altitudine:** non ho trovato il nome del sensore nella documentazione.
  Se sul tuo orologio non risponde, vedrai `---` (il resto funziona).
- **Anelli:** partono dall'alto e vanno in senso orario. Se partono da un'altra posizione, dimmelo.
- **Font:** data e numeri piccoli usano il font dell'orologio, quindi saranno un po' diversi dall'anteprima.
  L'orario verde invece è disegnato da me e viene identico.

## Cosa puoi cambiare da solo

In cima a `watchface/index.js`:
- `COMPASS_MS`: ogni quanti millisecondi si aggiorna la bussola (1000 = 1 secondo). Più è basso, più consuma.
- `SLOW_MS`: ogni quanti ms si aggiornano passi, batteria, battito e data.
- `STEP_GOAL_FALLBACK`: obiettivo passi, usato se l'orologio non ne comunica uno.
- `HEART_MAX`: battito a cui l'anello giallo si riempie.

Il codice si ferma da solo quando lo schermo si spegne, per risparmiare batteria.
