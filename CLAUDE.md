# CLAUDE.md · Global Future Expo 2035

> Documento di riferimento del progetto. Caricato automaticamente da Claude Code in ogni sessione. Contiene concept educativo, architettura dei file, regole operative e cose da non fare.

---

## Contesto del progetto

Il **Global Future Expo 2035** è uno **strumento formativo proprietario di ETN School** (ente accreditato MIM), non un kit replicabile da terzi. Le priorità sono quelle che lo rendono **certificabile e difendibile in sede di accreditamento**: valutazione ancorata a framework ufficiali, evidenze tracciabili, attestato spendibile, sistema modulare anti-doppione, formato teleguidato per formatori inesperti.

**Stack:** sito statico HTML + CSS + JS inline. Nessun build, nessuna dipendenza npm, nessuna variabile d'ambiente. Deploy su Netlify (la radice serve `index.html`).

---

## Mappa dei file

| File | Stato | Cosa contiene |
|------|-------|---------------|
| [index.html](index.html) | homepage | Pagina studenti · sistema modulare, glossario, valutazione studente, indice Event File. **Il nome `index.html` è obbligatorio** per Netlify, non rinominare. |
| [admin-docenti.html](admin-docenti.html) | guida docenti | Guida operativa teleguidata, valutazione formatore, rubrica MIM. Protetta da lock-screen con token. |
| [attestato.html](attestato.html) | certificato | Certificato A4 stampabile con 6 competenze e scala MIM. |
| [event-file.html](event-file.html) | template dossier | Template dossier compilabile (`contenteditable`) e stampabile, 10 capitoli. |
| [CLAUDE.md](CLAUDE.md) | questo file | Concept + regole operative del progetto. |
| [CHANGELOG-claude-code.md](CHANGELOG-claude-code.md) | log | Cronologia delle sessioni di sviluppo con Claude Code. |

---

# Concept del progetto

## Descrizione generale

Ecosistema laboratoriale interdisciplinare per scuola secondaria di primo grado:

# GLOBAL FUTURE EXPO 2035

L'idea è trasformare i laboratori scolastici in un'esperienza immersiva, narrativa e collaborativa, in cui tutti i gruppi lavorano verso un unico obiettivo comune:

> organizzare e presentare una grande esposizione mondiale del futuro ambientata nel 2035.

L'intero progetto è orchestrato tramite strumenti di Intelligenza Artificiale generativa come **ChatGPT**, **Gemini**, **NotebookLM**.

## Obiettivi pedagogici

- aumentare motivazione e coinvolgimento
- creare interdisciplinarità reale
- favorire cooperative learning
- introdurre **AI literacy**
- sviluppare creatività e problem solving
- migliorare comunicazione e public speaking
- far usare l'AI come strumento operativo, non come curiosità

## Concept narrativo

Gli studenti diventano il **"Future Creators Team"** e ricevono la missione di costruire il **Global Future Expo 2035**. Ogni laboratorio ha una missione specifica, ma tutti i contenuti confluiscono nel dossier ufficiale dell'evento (**Event File**).

## Storytelling introduttivo

Anno 2035.

Una città europea è stata scelta per ospitare il **Global Future Expo**, il più importante evento internazionale dedicato al futuro. Per alcune settimane arriveranno delegazioni, scuole, ricercatori, artisti, sportivi, robot, traduttori digitali, cittadini e visitatori da tutto il mondo.

Ma c'è un problema: l'Expo non è ancora pronto.

I padiglioni devono essere progettati. Le lingue devono dialogare. I dati devono diventare decisioni. Le storie devono emozionare. Le tecnologie devono funzionare. Gli spazi devono accogliere culture diverse. La cerimonia di apertura deve far capire al mondo che questa città non è solo un luogo, ma una promessa.

Per questo siete stati scelti voi. Da questo momento siete il **Future Creators Team**.

Il vostro obiettivo comune è creare l'**Event File ufficiale del Global Future Expo 2035**: il dossier che dimostrerà che la città è pronta ad accogliere il mondo.

La sfida è chiara:

> trasformare una città immaginaria in un'esperienza credibile, collaborativa e presentabile al mondo. E farlo con la vostra voce.

## Tab narrative del progetto

### Tab 1 · Missione
Progettare il Global Future Expo 2035 come un vero evento internazionale. Il risultato finale è un unico prodotto condiviso: l'**Event File**.

### Tab 2 · Cosa creeremo
Visione narrativa della città · slogan e messaggi ufficiali · mappe e percorsi · testi descrittivi e storytelling · materiali in inglese e lingue comunitarie · dati e grafici · contenuti digitali · assistente AI dell'Expo · speech e scaletta dell'Opening Ceremony.

### Tab 3 · Come lo faremo
Brainstorming, ricerca guidata, scrittura collaborativa, revisione, public speaking, strumenti di AI generativa. L'AI è assistente operativo, non sostituto.

### Tab 4 · Il contributo dei laboratori
- **Intelligenza Artificiale** · assistente AI dell'Expo + regole d'uso responsabile
- **Competenze Digitali** · materiali digitali, elementi interattivi, struttura Event File
- **Inglese** · accoglienza ai visitatori internazionali
- **Italiano** · voce narrativa dell'Expo (manifesto, storytelling)
- **Matematica** · dati e grafici per credibilità delle scelte
- **Lingue Comunitarie** · contenuti multilingue per delegazioni straniere
- **Comunicazione efficace** · pitch, public speaking, regia Opening Ceremony

### Tab 5 · Il risultato finale · Opening Ceremony
Tutto il lavoro confluisce nell'Opening Ceremony. Ogni gruppo ha il proprio spazio ma il pubblico percepisce un unico grande progetto.

Domanda guida:
> che cosa può diventare una città quando persone, culture, tecnologie e conoscenze lavorano insieme?

### Tab 6 · Perché conta
Le discipline non sono materie separate ma strumenti per risolvere una sfida complessa. La città del futuro è la prova di quello che si può costruire lavorando insieme.

---

# Architettura del percorso

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

## Laboratori coinvolti

7 macro-laboratori: Intelligenza Artificiale · Competenze Digitali · Inglese · Italiano · Matematica · Lingue Comunitarie · Comunicazione efficace.

## Fasi del percorso

1. **Launch Event** — introduzione narrativa, assegnazione team, identità dei gruppi
2. **Design** — brainstorming con AI, progettazione idee, definizione output
3. **Build** — produzione contenuti, materiali digitali, storytelling, mappe, badge, speech, AI assistant, grafici
4. **Refine** — revisione, miglioramento con AI, organizzazione materiali in NotebookLM
5. **Opening Ceremony** — presentazione finale, simulazione inaugurazione Expo

---

# Sistema modulare anti-doppione

> ⚠️ **Regola d'oro del contenuto.** Sostituisce il vecchio modello "stesso deliverable a 3 livelli di difficoltà" (Base/Intermedio/Avanzato), che produceva versioni sovrapposte della stessa cosa.

Ogni laboratorio = **1 output unico diviso in N moduli complementari**, uno per gruppo reale. La classe stabilisce **quale modulo**, non il livello di difficoltà. Senza un modulo, l'output del lab è incompleto.

| Lab | Output unico | Moduli |
|-----|--------------|--------|
| Intelligenza Artificiale | 1 Assistente AI | 1ª Identità · 2ª FAQ · 3ª Promptbook |
| Competenze Digitali | 1 sistema orientamento visitatori | 1ª Mappa · 2ª Home+QR+badge · 3ª User journey |
| Inglese | 1 kit comunicazione internazionale | 1ª Welcome kit · 2ª Speech+slogan · 3ª Press kit |
| Matematica | 1 cruscotto dati | 1ª Stima visitatori · 2ª Budget+spazi · 3ª Dashboard |
| Italiano | 1 voce narrativa | 2ª Manifesto+giornale · 3ª Storytelling 2035 |
| Comunicazione | 1 regia Opening Ceremony | 2ª Script+stampa · 3ª Scaletta+regia |
| Lingue Comunitarie | 1 kit accoglienza europea | 2ª (6) Passport · gruppo misto (3) Dialoghi |

**Italiano, Comunicazione e Lingue hanno 2 moduli (non 3).** Non aggiungere card-modulo per classi mancanti.

## Distribuzione gruppi reale

- **3 moduli:** AI · Digitale · Inglese · Matematica
- **2 moduli:** Italiano (2ª+3ª) · Comunicazione (2ª+3ª) · Lingue (2ª da 6 + gruppo misto 1ª/3ª da 3)
- Totale: 18 laboratori, 18 docenti, 105 studenti

---

# Utilizzo dell'AI

L'AI è concepita come: assistente creativo · tutor · supporto brainstorming · editor · traduttore · simulatore · organizzatore.

Gli studenti devono: chiedere alternative · confrontare output · verificare informazioni · riscrivere con parole proprie.

> L'AI non deve sostituire il pensiero umano ma aiutarlo.

---

# Event File

Dossier ufficiale del Global Future Expo 2035. **Tutti e 18 i moduli convergono qui** — nessun output resta orfano.

Contiene: slogan · mappe · assistente AI · welcome speech · dati e grafici · manifesto · storytelling · materiali digitali · scaletta finale.

**Template compilabile:** [event-file.html](event-file.html) — copertina + 10 capitoli in ordine, ogni capitolo dichiara quali moduli lo riempiono e ha un'area `contenteditable`. Pulsante "🖨 Esporta / Stampa" per A4/PDF. Le modifiche non si salvano (è un template, non un editor con database) → stampare o copiare alla fine.

**Naming dei file:** `GFE_<NN>_<LAB>_<CLASSE>_<MODULO>` (es. `GFE_05_AI_2A_FAQ`).

**Archivio centrale:** NotebookLM come "cervello" del progetto.

---

# Sistema di valutazione (accreditation-grade)

Serve a (a) dimostrare risultati di apprendimento, (b) rilasciare un attestato spendibile, (c) reggere un audit con evidenze tracciabili.

## Framework di riferimento

- **DigComp 2.2** — spina dorsale digitale
- **AI literacy** — cuore del percorso
- **Competenze chiave europee** — collaborazione/comunicazione
- **Educazione civica digitale** — etica/privacy

## Scala MIM

Ufficiale della Certificazione delle competenze del Ministero: **Iniziale · Base · Intermedio · Avanzato**.

> ⚠️ "Base/Intermedio/Avanzato" è linguaggio della **scala MIM degli esiti**. Non riutilizzarlo per descrivere livelli di difficoltà delle task — quello era il modello pre-modulare ormai sostituito.

## Cosa si valuta

- 6 competenze etichettate col framework di riferimento
- Rubrica 6×4 in [admin-docenti.html](admin-docenti.html) (sezione "Valutazione & Certificazione")
- Griglia di osservazione del formatore (evidenza tracciabile per audit)
- Autovalutazione studente + valutazione tra gruppi in [index.html](index.html) (sezione "07 · Valutazione")
- Principio di equità: si valuta il percorso, non il talento di partenza

## Attestato

[attestato.html](attestato.html) · certificato stampabile A4, tema chiaro, branding **ETN School · Ente accreditato dal Ministero dell'Istruzione e del Merito**. Campi: nome, lab/classe/modulo, 6 competenze con 4 livelli da spuntare, luogo/data, firma del formatore.

**Privacy-by-design:** i nomi degli studenti non sono nel codice (compilati a stampa).

---

# Guida docenti teleguidata

[admin-docenti.html](admin-docenti.html) è il copione passo-passo per docenti inesperti. Tutti e 7 i laboratori sono riscritti in **18 moduli**, ognuno con tre blocchi obbligatori (**non cambiare lo schema**):

- 🎯 **Cosa devi fare** — l'obiettivo concreto del modulo
- 🧰 **Strumenti da utilizzare** — quali tool (ChatGPT, Gemini, NotebookLM, Canva, Fogli Google, QR generator, carta…)
- 🪜 **Come procedere** — 6 passi numerati, da seguire in ordine

In più, per ogni lab, un **Prompt docente pronto** copia-incolla.

Le altre sezioni: "Prima di iniziare" · "Ruolo docente" · "Timeline" · "AI for dummies" · "Moduli" (come funzionano + box per i lab a 2 moduli) · "Problemi" · "Chiusura" · "Valutazione & Certificazione".

---

# Glossario degli output

Sezione `#glossario` in [index.html](index.html) con **39 termini** in 6 categorie:

- 🤖 **AI & assistente** — Chatbot, Prompt, Promptbook, FAQ, Dialogo
- ✍️ **Testi & comunicazione** — Manifesto, Articolo, Storytelling, Speech, Slogan, Press kit, Captions, Script, Scaletta, Pitch
- 🎨 **Digitale & visual** — Mappa, Legenda, Home page, Mockup, QR code, Badge, User journey, Storyboard
- 📊 **Dati & numeri** — Tabella, Grafico, Budget, Percentuale, Dashboard, Indicatore
- 🌍 **Lingue & accoglienza** — Passaporto, Scheda paese, Role-play
- 📦 **Parole del progetto** — Output, Modulo, Event File

Ogni voce: definizione breve in linguaggio adatto a studenti delle medie, più un tag che indica in quale laboratorio si usa.

Il link "📖 Glossario" è inserito una sola volta nel footer del modale dei task → appare in tutti i ~40 popup senza modificare le singole schede. Pulsante "↑ Torna su" in fondo alla sezione.

---

# Accesso admin · convenzioni operative

- **Token:** `GFE2035-DOCENTI-18`, hardcoded in JS di [admin-docenti.html:884](admin-docenti.html#L884). Protezione **"morbida"** (il token è leggibile nel sorgente HTML); per sicurezza vera servirebbe un backend.
- **Un solo cancello attivo:** la lock-screen di `admin-docenti.html`. Lo sblocco viene memorizzato in `localStorage` con chiave `gfeAdminUnlocked`. Una volta entrato, qualsiasi visita successiva apre direttamente la guida.
- Il link "Admin" dalla home punta direttamente ad `admin-docenti.html` (niente modale intermedio nella home).
- [attestato.html:197](attestato.html#L197) usa `admin-docenti.html?token=GFE2035-DOCENTI-18` per handoff comodo — non è un secondo gate, è solo un auto-unlock.
- **Non reintrodurre** un modale token nella home: era esattamente il "doppio modale" eliminato.

---

# Deploy

- **Hosting:** Netlify (drop della cartella o repo Git collegato).
- **Nessuna variabile d'ambiente** necessaria. Il token admin è in chiaro nel JS — non passa da env var.
- **Radice del sito:** Netlify cerca `index.html` alla radice → questo è il motivo per cui il file principale ha quel nome (rinominato da "Global Future Expo 2035.html").
- **Modifiche locali:** servono commit + push (deploy git-connesso) o re-drag della cartella (deploy manuale) per andare online.
- **Cache browser:** se al deploy non vedi le novità → hard refresh (Cmd+Shift+R).

---

# Test rapidi

- **Servire localmente:** aprire i `.html` direttamente nel browser, oppure `python3 -m http.server 8000` dalla cartella.
- **Resettare il lock admin:** in DevTools console → `localStorage.removeItem('gfeAdminUnlocked')`.
- **Verificare la stampa:** pulsanti "🖨" su `attestato.html` e `event-file.html` → CSS già ottimizzato per A4.

---

# Cose da non fare

- **Non rinominare `index.html`** → Netlify cerca quel nome alla radice.
- **Non rimuovere** `[hidden] { display: none !important; }` da [admin-docenti.html](admin-docenti.html) → previene il flash di contenuto riservato e il bug originale in cui la regola `.locked { display: flex }` sovrascriveva l'attributo `hidden`.
- **Non aggiungere `target="_blank"`** ai link interni che attraversano l'accesso admin → rompe la persistenza dello sblocco fra schede (era il bug del certificato → admin, risolto migrando a `localStorage`).
- **Non reintrodurre** le task per livello "Base/Intermedio/Avanzato" come 3 livelli di difficoltà delle attività → sostituite dai moduli per classe.
- **Non aggiungere card-modulo** per classi che non hanno gruppi reali (es. 1ª media in Italiano/Comunicazione/Lingue).
- **Non reintrodurre** un secondo modale token nella home.
- **Non mettere nomi di studenti nel codice** → privacy-by-design, compilare a stampa.

---

# Modal interattivi (struttura tecnica)

Per ogni task di ogni laboratorio sono presenti **modal dettagliati** in `index.html` con:
- spiegazione della task
- obiettivo
- istruzioni passo-passo
- prompt AI suggerito
- output atteso
- regole d'uso dell'AI
- link "📖 Glossario" nel footer (inserito una sola volta, condiviso da tutti)

Implementati con HTML dedicato, CSS custom (`.modal`, `.modal-content`, `.modal-prompt`, `.modal-tip`, `.modal-glossary-link`), JavaScript esplicito, apertura tramite click sulle card `.task`.

---

# Visione metodologica

Il progetto non è:
- una semplice lezione sull'AI
- un laboratorio isolato
- un'esercitazione tradizionale

ma un **Ecosistema collaborativo AI-native** in cui tutte le discipline cooperano, ogni gruppo produce valore, gli studenti costruiscono un'esperienza condivisa, la narrativa aumenta immersione e motivazione.

---

# Roadmap aperta

Da [CHANGELOG-claude-code.md](CHANGELOG-claude-code.md) — prossimi passi consigliati in ordine di valore per l'accreditamento:

1. **Uso sicuro & privacy dei minori** — policy esplicita (no dati personali nell'AI, supervisione, nota famiglie). Il più vicino a "obbligatorio" per un ente accreditato.
2. **Inclusione (BES/DSA) & accessibilità** — differenziazione + leggibilità (testi piccoli, alto contrasto, focus styles, skip-link).
3. **Misurazione d'impatto** — questionario pre/post (motivazione, AI literacy, fiducia public speaking) per documentare gli esiti.

---

# Possibili evoluzioni future

Smart Labs ETN · AI Future Skills Labs · Future Makers Experience · Expo scolastici permanenti · format Erasmus+ · laboratori STEAM immersivi.

---

# Storico delle sessioni di sviluppo

Per il log dettagliato delle modifiche fatte con Claude Code, vedere [CHANGELOG-claude-code.md](CHANGELOG-claude-code.md). Riepilogo:

**27 maggio 2026 · Sessione 1** — Fix accesso admin, sistema modulare anti-doppione, riscrittura admin in formato teleguidato, sistema di valutazione accreditation-grade, template dell'Event File, certificato MIM, glossario degli output. Da "esperienza didattica" a "kit formativo accreditation-grade".

**28 maggio 2026 · Sessione 2** — Fix deploy Netlify (rinomina `Global Future Expo 2035.html` → `index.html` + correzione link interni), semplificazione accesso admin (rimosso doppio modale, ora cancello unico sulla lock-screen di admin), trasformazione `Progetto.md` → `CLAUDE.md`.

---

# Autore del concept

**Luciano Marino** · Axonforce / ETN International

---

*Design system: Carta & Inchiostro · Dark Cyber Editorial (studenti) + tema chiaro (documenti stampabili)*
