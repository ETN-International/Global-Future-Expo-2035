# Global Future Expo 2035 · Log di sviluppo con Claude Code

> Riepilogo strutturato del lavoro fatto sul progetto durante la sessione con Claude Code.
> Da "esperienza didattica" a "kit formativo accreditation-grade" per ETN School.

**Data sessione:** 27 maggio 2026
**Path progetto:** `~/Documents/GitHub/Global Future Expo 2035/`
**File del progetto:**
- `Global Future Expo 2035.html` · pagina studenti
- `admin-docenti.html` · guida docenti
- `attestato.html` · certificato finale (nuovo)
- `event-file.html` · template dossier (nuovo)
- `Progetto.md` · descrizione

---

## Indice degli interventi

1. [Fix accesso admin con token](#1-fix-accesso-admin-con-token)
2. [Pulsante di ritorno alla pagina principale](#2-pulsante-di-ritorno-alla-pagina-principale)
3. [Disambiguazione task: Step 1 / Step 2](#3-disambiguazione-task-step-1--step-2)
4. [Sistema modulare anti-doppione](#4-sistema-modulare-anti-doppione)
5. [Allineamento titoli popup ai moduli](#5-allineamento-titoli-popup-ai-moduli)
6. [Glossario degli output](#6-glossario-degli-output)
7. [Link al glossario dai popup](#7-link-al-glossario-dai-popup)
8. [Pulsante "Torna su" nel glossario](#8-pulsante-torna-su-nel-glossario)
9. [Riscrittura admin in formato teleguidato](#9-riscrittura-admin-in-formato-teleguidato)
10. [Sistema di valutazione accreditation-grade](#10-sistema-di-valutazione-accreditation-grade)
11. [Template dell'Event File](#11-template-dellevent-file)
12. [Fix ritorno dal certificato all'admin](#12-fix-ritorno-dal-certificato-alladmin)
13. [Micro-programma 10 ore per Lab](#13-micro-programma-10-ore-per-lab)

---

## 1. Fix accesso admin con token

**Problema riportato:** anche inserendo il token corretto (`GFE2035-DOCENTI-18`) l'accesso ad `admin-docenti.html` non funzionava.

**Diagnosi:** due bug combinati.

- `admin-docenti.html` conteneva il markup della schermata di blocco (`#locked`, input token, pulsante Entra, messaggio d'errore) ma **nessuno script JavaScript** che validasse il token o sbloccasse la pagina.
- Bug CSS: il `<div id="locked" hidden>` veniva sovrascritto dalla regola `.locked { display: flex }`, che ha priorità superiore al selettore `[hidden]{display:none}` dello user-agent. Risultato: la schermata "Token non valido" restava sempre visibile sopra il contenuto.

In più, nella pagina principale il token valido faceva solo comparire un link, **senza passare il token alla pagina admin**.

**Soluzione applicata:**

In `admin-docenti.html`:
- Aggiunta regola CSS `[hidden] { display: none !important; }` per forzare il rispetto dell'attributo `hidden`.
- `#content` impostato come `hidden` di default (per evitare flash di contenuto riservato).
- Aggiunto script di validazione che: sblocca con `?token=...` valido nell'URL (handoff dalla pagina principale), memorizza lo sblocco in `sessionStorage` (poi convertito in `localStorage`, vedi punto 12), collega pulsante "Entra" e tasto Invio alla validazione, normalizza il token (case-insensitive, ignora trattini e spazi).

In `Global Future Expo 2035.html`:
- Il link "Apri guida docenti" ora punta a `admin-docenti.html?token=GFE2035-DOCENTI-18`, così la guida si apre già sbloccata.

**Nota di sicurezza:** rimane una protezione "morbida" — il token è leggibile nel sorgente HTML. Per una protezione reale serve un backend.

---

## 2. Pulsante di ritorno alla pagina principale

**Richiesta:** aggiungere un pulsante ben visibile in admin per tornare al file principale.

**Soluzione:** pulsante "← Torna alla pagina principale" in cima alla guida docenti, sopra l'intestazione, riquadro pieno color ciano coerente con il tema. Apre nella stessa scheda (non accumula schede). Il link "Pagina studenti" nella barra di navigazione resta disponibile.

---

## 3. Disambiguazione task: Step 1 / Step 2

**Problema riportato:** nella sezione "Task per lab" coesistevano due gruppi di task — 3 card per classe (1ª/2ª/3ª media) e 4 task generiche — senza alcuna etichetta che ne spiegasse il rapporto. Risultato: confusione su a cosa si riferissero le 4 task sotto.

**Vincolo:** non eliminare task ma aggiungerne se serve.

**Soluzione:** trasformati i due blocchi in un percorso a due step, con etichette aggiunte in tutti e 7 i laboratori (14 etichette totali, inserite via `replace_all`).

- **Step 1 · Per classe** → le 3 card definiscono *cosa consegnare* (obiettivo per 1ª/2ª/3ª media).
- **Step 2 · Come si fa** → le 4 task sono i passaggi *operativi* per costruirlo, da adattare al livello scelto sopra.

Aggiunti gli stili `.group-label`, `.group-step`, `.group-title`, `.group-desc` (badge ciano in JetBrains Mono, coerenti col tema). Nessuna task rimossa, tutti i collegamenti `data-modal` preservati.

---

## 4. Sistema modulare anti-doppione

**Problema sollevato:** con l'impostazione "stesso deliverable a 3 livelli di difficoltà" le tre classi producevano versioni sovrapposte della stessa cosa (es. tre "assistenti AI", tre "mappe"). Non era garantito che il lavoro di ogni gruppo fosse necessario al prodotto finale.

**Vincolo dal PDF di distribuzione gruppi:** i 18 gruppi non coprono tutti le 3 classi.

| Lab | Gruppi | Classi presenti |
|-----|--------|-----------------|
| Intelligenza Artificiale | 3 | 1ª · 2ª · 3ª |
| Competenze Digitali | 3 | 1ª · 2ª · 3ª |
| Inglese | 3 | 1ª · 2ª · 3ª |
| Matematica | 3 | 1ª · 2ª · 3ª |
| Italiano | 2 | 2ª · 3ª (no 1ª) |
| Comunicazione Efficace | 2 | 2ª · 3ª (no 1ª) |
| Lingue Comunitarie | 2 | 2ª (6 studenti) + gruppo misto 1ª/3ª/superiori (3) |

**Soluzione scelta:** moduli di un unico output (architettura modulare).

Per ogni laboratorio: **1 output unico diviso in N moduli complementari**, uno per gruppo reale. Senza un modulo, l'output del lab è incompleto.

| Lab | Output unico | Moduli |
|-----|--------------|--------|
| Intelligenza Artificiale | 1 Assistente AI | 1ª Identità · 2ª FAQ · 3ª Promptbook |
| Competenze Digitali | 1 sistema orientamento visitatori | 1ª Mappa · 2ª Home+QR+badge · 3ª User journey |
| Inglese | 1 kit comunicazione internazionale | 1ª Welcome kit · 2ª Speech+slogan · 3ª Press kit |
| Matematica | 1 cruscotto dati | 1ª Stima visitatori · 2ª Budget+spazi · 3ª Dashboard |
| Italiano | 1 voce narrativa | 2ª Manifesto+giornale · 3ª Storytelling 2035 |
| Comunicazione | 1 regia Opening Ceremony | 2ª Script+stampa · 3ª Scaletta+regia |
| Lingue Comunitarie | 1 kit accoglienza europea | 2ª (6) Passport · gruppo misto (3) Dialoghi |

**Modifiche visive in ogni lab:**

- Card **"Output unico del lab"** (banner ciano) che dichiara il prodotto complessivo.
- **Step 1 · Moduli per gruppo**: ogni gruppo trova la propria card-modulo con badge dell'anno.
- **Numero di moduli allineato ai gruppi reali**: Italiano/Comunicazione hanno 2 moduli (no card fantasma); Lingue ha 2ª + gruppo misto.
- Step 2 riformulato: "le task operative compongono l'intero output del lab".

Aggiunti stili `.output-unico`, `.module-year`, `.two-modules`. Le 4 task operative restano integralmente preservate e collegate ai modal originali.

---

## 5. Allineamento titoli popup ai moduli

**Problema residuo:** i popup di dettaglio riportavano ancora "AI Lab · Base · 1a media" invece di "Modulo 1 · …".

**Soluzione:** aggiornati 18 titoli (tutti quelli effettivamente mostrati) con il nuovo linguaggio `Modulo N · Nome (classe)`. Le 3 definizioni modal residue (`ita-base`, `com-base`, `lin-base`) non sono mai mostrate (nessuna card le apre) — codice inerte, innocuo.

---

## 6. Glossario degli output

**Richiesta:** glossario sulla spiegazione di tutti gli output (chatbot, script, ecc.) con voce in sidebar.

**Soluzione:** nuova sezione `#glossario` con **39 termini** raggruppati in 6 categorie, voce "06 · Glossario output" in sidebar (Opening Ceremony rinumerata a 07).

- 🤖 **AI & assistente** — Chatbot/Assistente AI, Prompt, Promptbook, FAQ, Dialogo
- ✍️ **Testi & comunicazione** — Manifesto, Articolo, Storytelling, Speech, Slogan, Welcome message, Press kit, Intervista, Captions, Script, Conferenza stampa/Q&A, Scaletta, Pitch
- 🎨 **Digitale & visual** — Mappa, Legenda, Home page, Mockup, QR code, Badge, User journey, Storyboard, Prototipo
- 📊 **Dati & numeri** — Tabella, Grafico, Budget, Percentuale, Dashboard/Cruscotto, Indicatore/Soglia
- 🌍 **Lingue & accoglienza** — Passaporto, Scheda paese, Role-play
- 📦 **Parole del progetto** — Output, Modulo, Event File

Ogni voce: definizione breve in linguaggio adatto a studenti delle medie, più un tag che indica in quale laboratorio si usa. Layout a 2 colonne, 1 colonna su mobile. Lo scrollspy e la progress bar funzionano automaticamente (sono generici, non hardcoded sulle sezioni).

---

## 7. Link al glossario dai popup

**Richiesta:** un piccolo "📖 Glossario" dentro i popup dei task, così gli studenti arrivano al glossario mentre lavorano.

**Soluzione efficiente:** inserito una sola volta nel `<div class="modal-footer">` del `#taskModal`. Markup statico → appare in tutti i ~40 popup senza modificare le singole schede.

- Stile `.modal-glossary-link` (testo ciano, hover che riempie di ciano).
- Handler JS che chiama `closeModal()` prima di navigare all'ancora `#glossario`.

---

## 8. Pulsante "Torna su" nel glossario

**Richiesta:** pulsante per tornare in cima dopo aver letto il glossario.

**Soluzione:** pulsante centrato "↑ Torna su" in fondo alla sezione, in stile pillola ciano coerente col tema. Punta a `#intro`.

**Giro completo della navigazione:**
1. Sidebar → "06 · Glossario output"
2. Popup task → pulsante "📖 Glossario" (chiude e scorre lì)
3. Fine glossario → "↑ Torna su"

---

## 9. Riscrittura admin in formato teleguidato

**Richiesta chiave:** "Molti docenti sono inesperti quindi hanno bisogno di essere teleguidati. Logica del tipo: Cosa devi fare, Strumenti da utilizzare, Come procedere."

**Diagnosi incoerenze pre-intervento:**
- "Prima di iniziare" e Timeline parlavano di "assegnare il livello" (ma ora il modulo è fissato dalla classe).
- "Come gestire i tre livelli" presupponeva 3 classi ovunque (falso per Italiano/Comunicazione/Lingue).
- Le istruzioni per laboratorio usavano ancora Base/Intermedio/Avanzato senza il formato teleguidato.

**Soluzione applicata:**

**Allineamento ai moduli (ovunque):**
- Header: ogni lab = 1 output diviso in moduli, ogni docente conduce un gruppo = un modulo.
- Timeline: "assegna livello" → "spiega il modulo e assegna i ruoli".
- "Come gestire i tre livelli" → "Come funzionano i moduli": regola d'oro (niente doppioni) + box di avviso sui lab a 2 moduli.
- Nav: "Livelli" → "Moduli".

**Formato teleguidato (la struttura richiesta):**
Tutti e 7 i laboratori riscritti in **18 moduli**, ognuno con tre blocchi:

- 🎯 **Cosa devi fare** — l'obiettivo concreto del modulo
- 🧰 **Strumenti da utilizzare** — quali tool (ChatGPT, Gemini, NotebookLM, Canva, Fogli Google, QR generator, carta…)
- 🪜 **Come procedere** — 6 passi numerati, da seguire in ordine

In più, per ogni lab, un **Prompt docente pronto** copia-incolla.

**Risultato:** un docente inesperto trova il suo lab → la sua classe → e ha davanti esattamente cosa fare, con cosa e come, passo per passo.

Validazione: 18 moduli, 54 blocchi teleguidati (18×3), 0 residui del vecchio formato. Tag HTML perfettamente bilanciati (148/148 div, 8/8 section).

---

## 10. Sistema di valutazione accreditation-grade

**Contesto chiarito:** ETN School eroga il percorso direttamente come ente accreditato dal Ministero dell'Istruzione e del Merito. La valutazione deve quindi servire a (a) dimostrare risultati di apprendimento, (b) rilasciare un attestato spendibile, (c) reggere un audit con evidenze tracciabili.

**Soluzione: pacchetto completo su 3 file, ancorato a 4 framework ufficiali.**

**Framework di riferimento:**
- **DigComp 2.2** (spina dorsale digitale)
- **AI literacy** (cuore del percorso)
- **Competenze chiave europee** (collaborazione/comunicazione)
- **Educazione civica digitale** (etica/privacy)

**Scala:** ufficiale della Certificazione delle competenze MIM (Iniziale · Base · Intermedio · Avanzato).

### `admin-docenti.html` → nuova sezione "Valutazione & Certificazione"

- **Rubrica** per 6 competenze × 4 livelli, ognuna etichettata col framework di riferimento.
- Come assegnare il livello + principio di equità (si valuta il percorso, non il talento di partenza).
- **Griglia di osservazione del formatore** (evidenza tracciabile per audit).
- Link al modello di attestato.

### `Global Future Expo 2035.html` → nuova sezione "07 · Valutazione"

- Su cosa sei valutato (le 6 competenze in linguaggio studente).
- **Autovalutazione cliccabile** (6 voci, riusa l'handler esistente delle checklist).
- **Valutazione tra gruppi** (criteri + feedback "una cosa bella + un consiglio").

### `attestato.html` (nuovo file)

- Certificato stampabile, tema chiaro ottimizzato per A4.
- Branding **ETN School · Ente accreditato dal Ministero dell'Istruzione e del Merito**.
- Campi: nome, lab/classe/modulo, 6 competenze con 4 livelli da spuntare, luogo/data, firma del formatore.
- Pulsante "🖨 Stampa".

**Privacy-by-design:** i nomi degli studenti non sono nel codice (compilati a stampa).

---

## 11. Template dell'Event File

**Obiettivo:** chiudere il cerchio del sistema modulare. Far convergere davvero i 18 moduli in un unico dossier.

**Tre interventi:**

### `Global Future Expo 2035.html` → sezione Event File arricchita

- **Indice ufficiale** (tabella): 10 capitoli, ognuno con cosa contiene e da quali moduli arriva. Funziona anche da **mappa delle integrazioni**: ogni studente vede che il suo modulo è un pezzo necessario del dossier.
- **Come si assembla in 5 passi**: naming dei file (`GFE_05_AI_2A_FAQ`), NotebookLM come archivio, impaginazione, controllo coerenza, export PDF.
- Pulsante "📄 Apri il template dell'Event File".

### `event-file.html` (nuovo file)

- Dossier light, stampabile A4/PDF, con copertina + 10 capitoli nell'ordine dell'indice.
- Ogni capitolo dichiara **quali moduli lo riempiono** e ha un'area compilabile (`contenteditable`) direttamente nel browser.
- Pulsante "🖨 Esporta / Stampa".
- Nota onesta: le modifiche non si salvano (è un template, non un editor con database) → stampare o copiare alla fine.
- Footer con accreditamento ETN School · MIM.

### `admin-docenti.html` → rimando in sezione Chiusura

- Pannello "Dove finisce il lavoro: l'Event File" con naming + link al template.

**Validazione critica:** tutti e 18 i moduli dei 7 laboratori hanno un capitolo di destinazione nell'indice — nessun output resta orfano. La logica modulare regge fino al prodotto finale.

---

## 12. Fix ritorno dal certificato all'admin

**Problema riportato:** dal certificato, cliccando "Torna all'area docenti", l'admin richiedeva di nuovo il token.

**Causa:** il certificato si apriva in una nuova scheda (`target="_blank"`); in quella nuova scheda `sessionStorage` (per-scheda) non aveva il "ricordo" dello sblocco.

**Due fix:**

1. In `attestato.html` il link "← Torna all'area docenti" ora punta a `admin-docenti.html?token=GFE2035-DOCENTI-18` (stesso meccanismo di handoff della pagina principale).
2. In `admin-docenti.html` lo sblocco è migrato da `sessionStorage` (per-scheda) a **`localStorage`** (condiviso tra schede e persistente). Dopo il primo sblocco, qualsiasi visita all'admin resta sbloccata finché non si svuotano i dati del browser.

---

## 13. Micro-programma 10 ore per Lab

**Problema emerso dall'audit:** il progetto dichiara 10 ore di attività per ogni Lab. Nei lab i 2-3 moduli (uno per classe) lavorano **in parallelo** nelle stesse 10 ore: ogni docente conduce un gruppo dentro questo arco condiviso. Quindi "10h per Lab" = "10h per gruppo" = "10h per docente". Lo scaffolding esistente, però, copriva solo ~1,5 ore reali.

- `index.html` § `#programma` era una macro-timeline generica in 5 fasi (Launch / Design / Build / Refine / Show) senza distribuzione oraria sui task del singolo gruppo.
- `admin-docenti.html` § `#timeline` prescriveva una sessione singola da 90 minuti per modulo — quindi 1,5 ore per gruppo, non 10.
- Le 4 task operative dei lab si esauriscono realisticamente in 60-75 minuti di lavoro studenti.

Risultato: ~8,5 ore per gruppo erano non scaffoldate.

**Soluzione: micro-programma a 10 blocchi orari** che avvolge le 4 task esistenti. I blocchi 3-6 ospitano le 4 task del lab; gli altri 6 blocchi sono il nuovo scaffolding (brainstorm, peer review, iterazione, integrazione Event File, prove cerimonia).

### Struttura universale dei 10 blocchi

| # | Blocco | Durata | Output (evidenza tracciabile) |
|---|--------|--------|-------------------------------|
| 1 | Launch &amp; identità | 1h | Ruoli + taccuino |
| 2 | Brainstorm guidato | 1h | 3-5 direzioni scelte |
| 3 | Task 1 del lab | 1h | Bozza pezzo 1 |
| 4 | Task 2 + revisione AI | 1,5h | Bozza pezzo 2 |
| 5 | Task 3 + revisione AI | 1,5h | Bozza pezzo 3 |
| 6 | Task 4 → draft 1 | 1h | Deliverable modulo (draft 1) |
| 7 | Peer review | 1h | Feedback ricevuti |
| 8 | Iterazione &amp; polish | 1h | Deliverable finale |
| 9 | Integrazione Event File | 0,5h | Modulo nel dossier |
| 10 | Prove Opening Ceremony | 1h | Presentazione provata |

**Totale: 10 ore esatte.**

### Ricaduta nei file

- **`index.html`** § `#programma`: la vecchia tabella a 5 fasi è stata sostituita da una **timeline in 10 blocchi** (markup `.tenh-grid` + `.tenh-block`), linguaggio studente, link interni a `#valutazione` (blocco 7), `#eventfile` (9), `#finale` (10). Aggiunti stili CSS dedicati (`.tenh-*`).
- **`admin-docenti.html`**: nuova sezione `#programma10` con la struttura universale + box "promemoria accreditation-grade" che ricorda che ogni blocco produce un'evidenza tracciabile per audit MIM. Aggiunta voce nav "Programma 10h".
- **`admin-docenti.html`** § `#timeline`: riqualificato in **"Lezione tipo (90 min) dentro un blocco di esecuzione"** — non è il modulo intero ma la singola lezione dentro un blocco 3-6. Aggiornato anche il link nav da "Timeline" a "Lezione tipo".
- **`admin-docenti.html`** § `#laboratori`: per ognuno dei 7 lab aggiunto un box compatto **"Distribuzione delle 10 ore — [Lab]"** che istanzia i blocchi 3-6 con i nomi esatti delle 4 task (presi da `index.html`) e i tool concreti del lab. I blocchi 1-2 e 7-10 restano universali nella sezione `#programma10`.

### Ancoraggio accreditation-grade

Ogni blocco è etichettato con un'**evidenza tracciabile** (taccuino, bozza, feedback ricevuti, file nominato, registrazione delle prove). Questo è ciò che rende le 10 ore difendibili in sede di audit MIM, coerentemente col percorso accreditation-grade già definito in [§ 10](#10-sistema-di-valutazione-accreditation-grade).

### Riuso di componenti esistenti

- Griglia peer review (blocco 7) → linka alla sezione `#valutazione` già introdotta in § 10 (autovalutazione + griglia "una cosa bella + un consiglio"), niente duplicazione.
- Naming convenzionale Event File (blocco 9) → riusa lo schema `GFE_[capitolo]_[lab]_[classe]` documentato in § 11.
- Stile visivo coerente con il Dark Cyber Editorial (border-left ciano, badge JetBrains Mono come `.group-step`).

---

## Stato finale del progetto

### File modificati o creati

| File | Stato | Contenuto |
|------|-------|-----------|
| `Global Future Expo 2035.html` | modificato | Sistema modulare, glossario, valutazione studente, indice Event File |
| `admin-docenti.html` | modificato | Riscritta in formato teleguidato, valutazione formatore, rubrica MIM, fix token |
| `attestato.html` | **nuovo** | Certificato stampabile con 6 competenze e scala MIM |
| `event-file.html` | **nuovo** | Template dossier compilabile/stampabile con 10 capitoli |

### Architettura del percorso

```
La storia (#storia)
   ↓
Regole AI (#regole)
   ↓
Programma 10 ore (#programma)
   ↓
Event File · indice + 5 passi assemblaggio (#eventfile)
   ↓
Task per Lab · 7 laboratori × N moduli (#labs)
   ↓                        ↓
   ↓                    Glossario (#glossario) ← linkato dai popup
   ↓
Valutazione · autovalutazione + tra pari (#valutazione)
   ↓
Opening Ceremony (#finale)
```

### Distribuzione gruppi reale (rispettata)

- **3 moduli:** AI · Digitale · Inglese · Matematica
- **2 moduli:** Italiano (2ª+3ª) · Comunicazione (2ª+3ª) · Lingue (2ª da 6 + gruppo misto 1ª/3ª da 3)

### Sistema di valutazione · ancoraggio framework

- DigComp 2.2 · AI literacy · Competenze chiave europee · Educazione civica digitale
- Scala MIM: Iniziale · Base · Intermedio · Avanzato

---

## Prossimi passi consigliati (in ordine di valore per l'accreditamento)

1. **Uso sicuro & privacy dei minori** — policy esplicita (no dati personali nell'AI, supervisione, nota famiglie). È il più vicino a "obbligatorio" per un ente accreditato.
2. **Inclusione (BES/DSA) & accessibilità** — differenziazione + leggibilità (testi piccoli, alto contrasto, focus styles, skip-link).
3. **Misurazione d'impatto** — questionario pre/post (motivazione, AI literacy, fiducia public speaking) per documentare gli esiti.

---

## Nord del progetto (annotato in memoria di Claude Code)

> Il Global Future Expo 2035 è uno **strumento formativo proprietario di ETN School** (ente accreditato MIM), non un kit replicabile da terzi. Le priorità sono quelle che lo rendono **certificabile e difendibile in sede di accreditamento**: valutazione ancorata a framework ufficiali, evidenze tracciabili, attestato spendibile, sistema modulare anti-doppione, formato teleguidato per formatori inesperti.

---

*Sessione condotta con Claude Code · Vibe Coding Workflow™*
*Design system di riferimento: Carta & Inchiostro*
