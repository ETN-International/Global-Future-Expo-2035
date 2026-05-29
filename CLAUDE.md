# CLAUDE.md · Global Future Expo 2035

> Documento di contesto del progetto per Claude Code.
> Aggiornato al 29 maggio 2026 — riflette lo stato dopo la sessione documentata in `CHANGELOG-claude-code.md`.

---

## Identità del progetto

**Global Future Expo 2035** è uno **strumento formativo proprietario di ETN School** (ente accreditato dal Ministero dell'Istruzione e del Merito), **non** un kit replicabile da terzi.

Le priorità che guidano ogni decisione sono quelle che lo rendono **certificabile e difendibile in sede di accreditamento**:

- valutazione ancorata a framework ufficiali (DigComp 2.2, AI literacy, Competenze chiave europee, Educazione civica digitale)
- evidenze tracciabili per audit
- attestato spendibile (scala MIM)
- sistema modulare anti-doppione
- formato teleguidato per formatori inesperti

---

## File del progetto

| File | Ruolo |
|------|-------|
| [index.html](index.html) | Pagina studenti · esperienza interattiva completa |
| [admin-docenti.html](admin-docenti.html) | Guida docenti teleguidata · rubrica MIM · griglia osservazione |
| [attestato.html](attestato.html) | Certificato stampabile · 6 competenze su scala MIM |
| [event-file.html](event-file.html) | Template dossier finale compilabile · 10 capitoli |
| [CLAUDE.md](CLAUDE.md) | Questo documento |
| [CHANGELOG-claude-code.md](CHANGELOG-claude-code.md) | Log dettagliato della sessione di sviluppo |

**Accesso admin:** token `GFE2035-DOCENTI-18` (handoff via querystring dalla pagina principale e dal certificato; sblocco persistente in `localStorage`). Protezione "morbida": il token è leggibile nel sorgente, per una vera protezione servirebbe un backend.

---

## Concept narrativo

Gli studenti diventano il **"Future Creators Team"** e ricevono la missione di costruire il **Global Future Expo 2035**: un'esposizione mondiale del futuro ambientata nel 2035.

Anno 2035. Una città europea è stata scelta per ospitare l'Expo. Padiglioni da progettare, lingue da far dialogare, dati da trasformare in decisioni, storie da emozionare. Ogni laboratorio riceve una missione diversa, ma nessuna è sufficiente da sola: il futuro nasce dall'unione di idee, competenze, creatività e collaborazione.

Tutti i contenuti confluiscono nell'**Event File ufficiale**: il dossier che dimostra che la città è pronta ad accogliere il mondo.

> Trasformare una città immaginaria in un'esperienza credibile, collaborativa e presentabile al mondo. E farlo con la propria voce.

---

## Obiettivi pedagogici

- aumentare motivazione e coinvolgimento
- creare interdisciplinarità reale
- favorire cooperative learning
- introdurre **AI literacy** come cuore del percorso
- sviluppare creatività e problem solving
- migliorare comunicazione e public speaking
- usare l'AI come strumento operativo, non come curiosità

Strumenti AI usati: **ChatGPT**, **Gemini**, **NotebookLM** (archivio e cervello centrale del progetto).

---

## Architettura modulare (anti-doppione)

**Principio:** per ogni laboratorio, **1 output unico diviso in N moduli complementari**, uno per gruppo reale. Senza un modulo, l'output del lab è incompleto.

Questa è la differenza chiave rispetto alla logica "stesso deliverable a 3 livelli" — qui i gruppi non producono versioni sovrapposte della stessa cosa, ma pezzi diversi e necessari di un unico prodotto.

### Distribuzione reale dei 18 gruppi

| Lab | Gruppi | Classi presenti |
|-----|--------|-----------------|
| Intelligenza Artificiale | 3 | 1ª · 2ª · 3ª |
| Competenze Digitali | 3 | 1ª · 2ª · 3ª |
| Inglese | 3 | 1ª · 2ª · 3ª |
| Matematica | 3 | 1ª · 2ª · 3ª |
| Italiano | 2 | 2ª · 3ª (no 1ª) |
| Comunicazione Efficace | 2 | 2ª · 3ª (no 1ª) |
| Lingue Comunitarie | 2 | 2ª (6 studenti) + gruppo misto 1ª/3ª/superiori (3) |

### Output unici e moduli

| Lab | Output unico | Moduli |
|-----|--------------|--------|
| Intelligenza Artificiale | 1 Assistente AI dell'Expo | 1ª Identità · 2ª FAQ · 3ª Promptbook |
| Competenze Digitali | 1 sistema orientamento visitatori | 1ª Mappa · 2ª Home+QR+badge · 3ª User journey |
| Inglese | 1 kit comunicazione internazionale | 1ª Welcome kit · 2ª Speech+slogan · 3ª Press kit |
| Matematica | 1 cruscotto dati dell'Expo | 1ª Stima visitatori · 2ª Budget+spazi · 3ª Dashboard |
| Italiano | 1 voce narrativa dell'Expo | 2ª Manifesto+giornale · 3ª Storytelling 2035 |
| Comunicazione | 1 regia Opening Ceremony | 2ª Script+stampa · 3ª Scaletta+regia |
| Lingue Comunitarie | 1 kit accoglienza europea | 2ª Passport · misto Dialoghi |

**Numeri:** 18 moduli totali · 7 laboratori · 105 studenti · 18 docenti.

---

## Logica didattica a due step (in `index.html`)

Per evitare confusione tra deliverable e operatività, ogni laboratorio espone:

- **Step 1 · Moduli per gruppo** — *cosa consegnare* (il modulo di competenza del gruppo, con badge dell'anno)
- **Step 2 · Come si fa** — *come costruirlo* (le 4 task operative, da adattare al modulo scelto)

Le 4 task operative restano integralmente preservate e collegate ai modal di dettaglio (~40 popup totali, allineati al linguaggio `Modulo N · Nome (classe)`).

---

## Guida docenti in formato teleguidato (`admin-docenti.html`)

Tutti i 18 moduli sono riscritti con la struttura richiesta da formatori inesperti:

- 🎯 **Cosa devi fare** — l'obiettivo concreto del modulo
- 🧰 **Strumenti da utilizzare** — quali tool (ChatGPT, Gemini, NotebookLM, Canva, Fogli Google, QR generator, carta…)
- 🪜 **Come procedere** — 6 passi numerati, da seguire in ordine

In più, per ogni lab, un **Prompt docente pronto** copia-incolla.

Validazione: 18 moduli × 3 blocchi = 54 blocchi teleguidati, 0 residui del vecchio formato Base/Intermedio/Avanzato per la conduzione (la scala MIM resta invece per la valutazione).

---

## Sistema di valutazione (accreditation-grade)

ETN School eroga il percorso direttamente come ente accreditato dal MIM. La valutazione deve quindi:

1. dimostrare risultati di apprendimento
2. rilasciare un attestato spendibile
3. reggere un audit con evidenze tracciabili

### Framework di riferimento

- **DigComp 2.2** — spina dorsale digitale
- **AI literacy** — cuore del percorso
- **Competenze chiave europee** — collaborazione/comunicazione
- **Educazione civica digitale** — etica/privacy

### Scala

Quella ufficiale della **Certificazione delle competenze MIM**: Iniziale · Base · Intermedio · Avanzato.

### Dove vive la valutazione

- **`admin-docenti.html`** → sezione *Valutazione & Certificazione*: rubrica 6 competenze × 4 livelli, griglia di osservazione del formatore, principio di equità (si valuta il percorso, non il talento di partenza).
- **`index.html`** → sezione *07 · Valutazione*: autovalutazione cliccabile + valutazione tra gruppi ("una cosa bella + un consiglio").
- **`attestato.html`** → certificato stampabile A4, branding ETN School · Ente accreditato MIM, 6 competenze su 4 livelli da spuntare, firma del formatore.

**Privacy-by-design:** i nomi degli studenti non sono nel codice (compilati a stampa).

---

## Event File (dossier finale)

Chiude il cerchio dell'architettura modulare: tutti i 18 moduli confluiscono in un unico dossier.

- **Indice ufficiale** in `index.html`: 10 capitoli, ognuno con cosa contiene e da quali moduli arriva. Funziona come **mappa delle integrazioni**.
- **Come si assembla in 5 passi**: naming dei file (`GFE_05_AI_2A_FAQ`), NotebookLM come archivio, impaginazione, controllo coerenza, export PDF.
- **`event-file.html`**: dossier light stampabile A4/PDF, copertina + 10 capitoli, aree `contenteditable` direttamente nel browser. Le modifiche non si salvano (è un template, non un editor con DB) → stampare o copiare alla fine.

**Validazione critica:** tutti i 18 moduli hanno un capitolo di destinazione — nessun output resta orfano.

---

## Glossario degli output

Sezione `#glossario` in `index.html` con **39 termini** in 6 categorie, scritti in linguaggio adatto a studenti delle medie:

- 🤖 AI & assistente — Chatbot, Prompt, Promptbook, FAQ, Dialogo
- ✍️ Testi & comunicazione — Manifesto, Articolo, Storytelling, Speech, Slogan, Welcome message, Press kit, Intervista, Captions, Script, Conferenza stampa/Q&A, Scaletta, Pitch
- 🎨 Digitale & visual — Mappa, Legenda, Home page, Mockup, QR code, Badge, User journey, Storyboard, Prototipo
- 📊 Dati & numeri — Tabella, Grafico, Budget, Percentuale, Dashboard/Cruscotto, Indicatore/Soglia
- 🌍 Lingue & accoglienza — Passaporto, Scheda paese, Role-play
- 📦 Parole del progetto — Output, Modulo, Event File

**Giro di navigazione completo:**
1. Sidebar → "06 · Glossario output"
2. Popup task → pulsante "📖 Glossario" (chiude e scorre lì)
3. Fine glossario → pulsante "↑ Torna su"

---

## Architettura della pagina studenti (`index.html`)

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

Stile: **Dark Cyber Editorial** con sidebar fissa, navigazione interna, scrollspy, progress bar generica (non hardcoded sulle sezioni), checklist interattive, ~40 modal di dettaglio.

---

## Struttura didattica (5 fasi)

1. **Launch Event** — introduzione narrativa, assegnazione team, identità gruppi
2. **Design** — brainstorming con AI, progettazione idee, definizione output
3. **Build** — produzione contenuti (mappe, badge, speech, AI assistant, grafici, storytelling)
4. **Refine** — revisione, miglioramento con AI, organizzazione in NotebookLM
5. **Opening Ceremony** — presentazione finale, simulazione inaugurazione Expo

---

## Filosofia d'uso dell'AI

L'AI è: assistente creativo · tutor · supporto brainstorming · editor · traduttore · simulatore · organizzatore.

Gli studenti devono:

- chiedere alternative
- confrontare output
- verificare informazioni
- riscrivere con parole proprie

> L'AI non deve sostituire il pensiero umano ma aiutarlo.

---

## Prossimi passi consigliati (in ordine di valore per l'accreditamento)

1. **Uso sicuro & privacy dei minori** — policy esplicita (no dati personali nell'AI, supervisione, nota famiglie). È il più vicino a "obbligatorio" per un ente accreditato.
2. **Inclusione (BES/DSA) & accessibilità** — differenziazione + leggibilità (testi piccoli, alto contrasto, focus styles, skip-link).
3. **Misurazione d'impatto** — questionario pre/post (motivazione, AI literacy, fiducia public speaking) per documentare gli esiti.

---

## Possibili evoluzioni future del format

- Smart Labs ETN
- AI Future Skills Labs
- Future Makers Experience
- Expo scolastici permanenti
- format Erasmus+
- laboratori STEAM immersivi

---

## Autore

**Luciano Marino** — Axonforce / ETN International

*Design system: Carta & Inchiostro · Workflow: Vibe Coding con Claude Code*
