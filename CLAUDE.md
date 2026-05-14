# Per Tina — contesto del progetto

Questo è un piccolo sito-regalo per una persona di nome **Tina** (yoga, incensi, attualmente in India). L'obiettivo: ogni giorno il sito mostra un mood musicale diverso, scelto in modo deterministico dalla data, con un link che apre la corrispondente Infinite Mixtape di NTS Radio.

L'intero progetto è **un solo file**: `index.html`. Niente build, niente dipendenze, niente framework. Va pubblicato su GitHub Pages.

## Decisioni di design già prese (non rimettere in discussione senza ragione)

- **Estetica**: morbida, soft, ispirata a Dia browser e Perplexity. Pastelli, eleganza minimale, niente immagini AI.
- **Sfondo**: crema `#F5F2E8` (non bianco puro).
- **Font**: tutto Instrument Serif (Google Fonts), incluso il nome del mood in grande. Considerato anche sans+serif misto, scartato — Tina è un regalo personale, il serif uniforme dà un tono "lettera scritta a mano".
- **Layout**: tutto allineato al centro.
- **Saluto**: `"Ciao Tina, è il [data] e il mood di oggi è:"` con la data formattata in italiano (es. "14 maggio 2026"). Senza giorno della settimana per evitare la ripetizione di "oggi".
- **Mood centrale**: in grande, con un gradiente radiale dietro come "alone". Il gradiente usa `closest-side` per evitare bordi a gradino, e una variabile `DILUTION = 0.15` per ammorbidire i colori mescolandoli col crema dello sfondo.
- **Link**: testo discreto "ascolta ora →" sotto la descrizione. Niente menzioni di NTS in modo pubblicitario.
- **Sotto**: griglia 3×3 degli altri 9 mood disponibili (esclude quello del giorno), come piccola gallery cromatica. Ognuno cliccabile.

## Mood selezionati (10 totali)

Solo Infinite Mixtapes coerenti con l'estetica pastello + spirito Tina. **Esclusi consapevolmente**: The Pit (metal), Labyrinth (psichedelia oscura), Otaku (anime/videogiochi), Rap House (trap/drill), Sweat (party music — troppo club per Tina), The Tube (post-punk industrial).

I 10 inclusi:
1. poolside
2. slow focus
3. low key (slug NTS legacy: `100-percent-hip-hop`)
4. memory lane
5. 4 to the floor
6. island time
7. sheet music
8. feelings
9. expansions
10. field recordings

## Logica di rotazione

```
seed = anno × 10000 + mese × 100 + giorno
mood_del_giorno = moods[seed % 10]
```

Deterministico: chiunque visiti il sito nello stesso giorno solare (nel proprio fuso orario) vede lo stesso mood. **Limitazione nota e accettata dall'utente**: il pattern si ripete ogni 10 giorni in modo prevedibile. L'utente ha esplicitamente detto di non risolverlo.

## Struttura del file

`index.html` contiene tutto in tre sezioni:
- `<head>` con CSS inline e import Google Fonts
- `<body>` con il markup HTML
- `<script>` in fondo con: array `moods[]` (la fonte di verità per dati + palette), helper `dilute()` e `buildGradient()`, e funzione `render()` che popola il DOM

Per **aggiungere/togliere/modificare un mood**, edita solo l'array `moods` nello script. Ogni voce ha:
- `name`, `slug` (parte dopo `/infinite-mixtapes/` nell'URL NTS), `desc`
- `text` (colore scuro per il testo)
- `swatch` (sfondo del riquadrino in basso)
- `stops` (4 hex per il gradiente radiale, dal più saturo al più diluito)

## Deploy

GitHub Pages, repo pubblico, branch main, root. URL finale: `https://[utente].github.io/[reponame]/`.

## Regole per Claude Code

- **Non aggiungere dipendenze**. Il vincolo di "un solo file" è una scelta, non una limitazione.
- **Non sostituire Instrument Serif**. È stato deliberatamente scelto.
- **Non riscrivere o "modernizzare" la logica di seed**. Funziona ed è stata accettata così com'è.
- Se si tocca il gradiente: ricordati che `closest-side` è essenziale per evitare il gradino al bordo, e che `DILUTION` controlla l'intensità globale.
- Se serve aggiungere immagini, animazioni elaborate, o "feature": chiedi prima. Lo spirito del progetto è minimalismo intenzionale.
