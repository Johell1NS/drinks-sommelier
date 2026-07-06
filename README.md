# drinks-sommelier

<p align="center">
  <strong>Un sommelier nel taschino, sempre al tuo fianco.</strong><br>
  <em>Scaffali, menu, cantine: ovunque tu sia, lui sa cosa consigliarti.</em>
</p>

> **Una skill per agenti AI.** OpenClaw, Hermes Agent, OpenCode, Claude Code, Cursor e oltre.
> Un sommelier virtuale specializzato in birre e vini che impara i tuoi gusti
> personali e ti suggerisce la scelta migliore da qualsiasi scaffale, menu
> o lista. **Gratuita, open-source, auto-ospitata.**

---

## Perché esiste

Al ristorante, al pub, all'enoteca, al supermercato: il problema è sempre
lo stesso. **Decine di opzioni e nessuna certezza** su cosa prendere che sia
davvero adatto ai tuoi gusti.

Potresti chiedere al cameriere, aprire cinque schede sul telefono, o
sperare che il nome più bello sia anche il migliore. Oppure puoi chiedere
al tuo agente AI — e lui sa già cosa ti piace.

**drinks-sommelier** insegna a qualsiasi agente AI a fare da sommelier
personale. L'agente:

1. Impara le tue preferenze di gusto, una volta per tutte
2. Analizza qualsiasi input: foto di uno scaffale, menu digitali, liste
   di nomi scritte dall'utente
3. Cerca informazioni aggiornate su ogni prodotto
4. Confronta ogni prodotto con il tuo profilo gusti
5. Ti dice esattamente cosa prendere — e perché

Il tutto in modo trasparente, onesto, gratuito e senza inventare niente.

---

## Benefici

- **Impara i tuoi gusti nel tempo.** Più usi la skill, più l'agente
  conosce il tuo palato. Ogni interazione affina il profilo.

- **Birre e vini in una skill unica.** Non devi installare due skill
  separate. L'agente gestisce entrambe le categorie, riconoscendo
  automaticamente cosa sta analizzando.

- **Analisi da immagini e da testo.** Fotografa uno scaffale, un menu,
  una carta dei vini. Oppure scrivi una lista. L'agente estrae solo
  i prodotti pertinenti (birre e vini), ignorando tutto il resto.

- **Niente allucinazioni.** L'agente ha il divieto assoluto di usare
  le proprie conoscenze pre-addestramento. Ogni prodotto viene
  ricercato puntualmente sul web prima di essere valutato.

- **Indice di preferenza 0-100%.** Ogni suggerimento ha un punteggio
  chiaro che dice quanto un prodotto è adatto ai tuoi gusti. Niente
  mezze misure.

- **Profilo gusti persistente.** Le tue preferenze sono salvate in
  file di testo leggibili e modificabili. Non si perdono tra una
  sessione e l'altra.

- **Setup guidato dall'agente.** La prima volta, l'agente ti fa le
  domande giuste per capire i tuoi gusti, senza lasciarti davanti
  configurazioni manuali.

- **Open-source, licenza MIT.** Gratuito, senza abbonamenti, senza
  API key, senza limiti. Puoi usarlo, modificarlo, distribuirlo.

- **Funziona con qualsiasi agente AI.** Scritta per OpenCode, ma
  facilmente convertibile per OpenClaw, Hermes Agent, Claude Code, Cursor,
  GitHub Copilot e qualsiasi altro agente. Mostra questo README al tuo
  agente per una conversione semplice e automatica.

- **Completamente personalizzabile.** SKILL.md è un file di testo.
  Aggiungi regole, modifica i criteri, adattalo al tuo workflow.

---

## Come funziona

Il processo si articola in 5 fasi, eseguite in sequenza dall'agente ogni
volta che viene interrogato.

### Fase 1 — Configurazione del profilo gusti (una tantum)

La prima volta che la skill viene caricata, l'agente verifica se i
paragrafi "Gusti dell'utente per le birre" e "Gusti dell'utente per
i vini" in SKILL.md sono già stati compilati.

Se non lo sono, l'agente apre il file `data/SETUP.md` che contiene:
- Domande guida per raccogliere le preferenze (dolce/amaro, gradazione,
  stili graditi e non, ecc.)
- Esempi di paragrafi compilati correttamente
- Esempi di file `data/` popolati

L'agente ti fa le domande, raccoglie le risposte, e modifica
i due paragrafi dei gusti in SKILL.md. Se durante la
configurazione l'utente menziona prodotti specifici, l'agente
li registra nei file `data/` corrispondenti (operazione
facoltativa ma utile per affinare il profilo).

Puoi anche compilare i paragrafi a mano, se preferisci.

I file `data/birre-note-preferite.md` e `data/vini-noti-preferiti.md`
sono facoltativi e contengono prodotti specifici che hai già valutato
in passato. Più sono completi, più l'agente capisce le tue sfumature.

### Fase 2 — Analisi dell'input

L'agente identifica cosa hai a disposizione e in che formato:

- **Testo**: estrae i nomi di birre e vini da una lista scritta
- **Immagine**: analizza la foto (scaffale, menu, carta vini) e
  riconosce solo i prodotti che sono birre o vini.
  Ignora completamente: liquori, superalcolici, snack, pasti,
  dessert, bibite, accessori. Qualsiasi cosa non sia birra o vino.
- **Misto**: se mandi sia testo che immagini, analizza tutto.

Se l'input non è chiaro, l'agente chiede prima di procedere.

### Fase 3 — Ricerca web (anti-allucinazione)

L'agente ha il **divieto assoluto** di usare le proprie conoscenze
pre-addestramento per valutare un prodotto. Potrebbero essere obsolete,
imprecise, o peggio: inventate. Per questo, esegue una ricerca web
puntuale su ogni singolo prodotto identificato.

Cosa cerca l'agente:

| Categoria | Informazioni raccolte |
|---|---|
| **Birre** | Stile, gradazione alcolica, dolcezza, amarezza (IBU), corpo, note aromatiche, ingredienti |
| **Vini** | Vitigno, denominazione, zona di produzione, annata, corpo, acidità, tannicità, grado alcolico, note di dolcezza |

Se un prodotto non è reperibile online, l'agente lo dichiara
onestamente e non inventa caratteristiche.

### Fase 4 — Valutazione

L'agente confronta ogni prodotto con il tuo profilo gusti, che ha
due livelli distinti:

1. **Regole di gusto** — le linee guida generali che hai scritto
   nei paragrafi dei gusti (es. "birre dolci", "vini non troppo
   dolci", "gradazione ≤ 9°"). Sono vincolanti.
2. **Prodotti nei file data/** — esempi concreti di birre e vini
   che hai apprezzato o non apprezzato. Servono a calibrare le
   regole di gusto (es. se ami la birra X e odi la Y, l'agente
   capisce cosa intendi per "dolce" e "amaro").

L'agente assegna un **indice di preferenza da 0 a 100%**:

| Indice | Significato |
|---|---|
| 90-100% | Prodotto perfetto per i tuoi gusti |
| 70-89% | Ottimo, lievi discrepanze |
| 50-69% | Accettabile, ma non ottimale |
| 30-49% | Poco adatto ai tuoi gusti |
| 0-29% | Da evitare |

Se hai indicato un contesto alimentare, l'agente valuta anche
l'abbinamento con il cibo (priorità secondaria).

### Fase 5 — Raccomandazione

L'agente struttura la risposta in modo chiaro:

1. **Prima scelta**: il prodotto migliore con indice di preferenza
   e spiegazione del perché è adatto ai tuoi gusti
2. **Alternative** (se presenti): in ordine di preferenza decrescente
3. **Abbinamenti**: suggerimenti gastronomici per i prodotti
4. **Prodotti da evitare**: quelli che chiaramente non rispettano
   i tuoi gusti, con spiegazione

---

## Struttura del progetto

```
drinks-sommelier/
├── SKILL.md                 ← Istruzioni complete per l'agente
│                              (frontmatter, gusti, operatività,
│                               edge case, best practices, esempi,
│                               aggiornamento preferenze)
├── README.md                ← Questo file
├── LICENSE                  ← Licenza MIT
└── data/
    ├── SETUP.md             ← Guida alla configurazione iniziale
    │                          (usata solo il primo avvio)
    ├── birre-note-preferite.md  ← Birre apprezzate e non
    │                               (da compilare con l'uso)
    └── vini-noti-preferiti.md   ← Vini apprezzati e non
                                    (da compilare con l'uso)
```

---

## Installazione

### Unico passo

```bash
npx skills add Johell1NS/drinks-sommelier
```

### Verifica

Dopo l'installazione, controlla che la cartella della skill contenga tutti i file necessari:

```
drinks-sommelier/
├── SKILL.md
├── README.md
├── LICENSE
└── data/
    ├── SETUP.md
    ├── birre-note-preferite.md
    └── vini-noti-preferiti.md
```

Su alcuni sistemi (noto su Windows) `npx skills add` potrebbe copiare solo SKILL.md. In tal caso, clona il repository direttamente nella cartella della skill:

```bash
# Sostituisci <PATH_AGENTE> con la cartella skills del tuo agente
# Esempio su Windows (OpenCode):
cd C:\Users\Utente\.agents\skills
# Esempio su Linux/Mac:
cd ~/.agents/skills

# Se la cartella drinks-sommelier esiste già, eliminala
rmdir /s drinks-sommelier   # Windows
# rm -rf drinks-sommelier   # Linux/Mac

# Clona nel posto giusto
git clone https://github.com/Johell1NS/drinks-sommelier.git
```

Ora hai tutti i file. La skill è pronta all'uso.

**Non serve installare nulla.** Nessun Docker, nessun npm package,
nessuna dipendenza esterna. La skill è puramente testuale — istruzioni
che l'agente segue. Le uniche dipendenze sono le capacità dell'agente
stesso (analisi immagini, ricerca web).

---

## Configurazione

La skill ha bisogno di conoscere i tuoi gusti per funzionare. Puoi
configurarla in due modi:

### Configurazione guidata (consigliata)

Dopo aver installato la skill, chiedi al tuo agente qualcosa come
"Aiutami a configurare la skill drinks-sommelier". L'agente caricherà
SKILL.md, troverà i paragrafi dei gusti ancora da compilare, e ti
guiderà attraverso la configurazione iniziale usando `data/SETUP.md`.

In alternativa, chiedi semplicemente un consiglio su birre o vini:
l'agente rileverà automaticamente che la skill non è inizializzata
e ti farà le domande giuste.

### Configurazione manuale

Apri `SKILL.md` e compila i paragrafi:

**Gusti dell'utente per le birre**
```
Preferisco birre dolci e non amare.
Non devono superare i 9° di gradazione alcolica.
Mi piacciono gli stili belga e le birre fruttate.
Non mi piacciono IPA, stout e birre troppo amare.
```

**Gusti dell'utente per i vini**
```
Preferisco vini rossi non troppo dolci.
Per i bianchi, prediligo vermentino e sauvignon.
Mi piacciono vini con buona acidità e freschezza.
Non mi piacciono vini passiti o liquorosi.
```

Puoi anche popolare i file `data/birre-note-preferite.md` e
`data/vini-noti-preferiti.md` con prodotti specifici che hai
già provato e valutato. Questa parte è facoltativa ma utile
per affinare il profilo.

**Esempio — `data/birre-note-preferite.md`**
```
# BIRRE APPREZZATE
- Kwak
- Triple Karmeliet
- La Trappe Blond
- Flea Margherita

# BIRRE NON APPREZZATE
- Qualsiasi IPA
- Stout
- Birre con gradazione superiore a 9°
```

**Esempio — `data/vini-noti-preferiti.md`**
```
# VINI APPREZZATI
- Vermentino Costamolino
- Syrah Soraia Casale Valle Chiesa
- Rebeca Firriato

# VINI NON APPREZZATI
- Vini passiti
- Vini liquorosi
```

### Aggiornamento nel tempo

Ogni volta che esprimi un giudizio su un prodotto ("questa mi piace",
"questo non mi piace"), l'agente aggiorna automaticamente i file
`data/`. Le regole di gusto nei paragrafi di SKILL.md invece
vengono aggiornate solo con la tua conferma esplicita, perché
sono vincolanti per le valutazioni future.

---

## Esempi di utilizzo

### Scenario 1 — Scaffale vini (immagine)
Fotografi uno scaffale di un'enoteca. L'agente identifica i vini,
li cerca tutti sul web, li confronta con il tuo profilo. Ti dice
quale prendere, perché, e con cosa abbinarlo.

### Scenario 2 — Menu birre (immagine)
Fotografi il menu birre di un pub. L'agente ignora cocktail,
superalcolici, ecc... analizza solo le birre, cerca informazioni su
ciascuna. Ti suggerisce la birra più adatta ai tuoi gusti.

### Scenario 3 — Lista testuale mista
Scrivi "Ho questi vini: Chianti Classico, Vermentino Costamolino,
Amarone. E queste birre: Kwak, IPA artigianale locale, Leffe Blonde."
L'agente valuta entrambe le categorie e ti dice qual è la scelta
migliore in assoluto.

### Scenario 4 — Richiesta senza lista
"Devo prendere un vino per una cena, cosa mi consigli?" L'agente
non inventa. Chiede cosa hai a disposizione, che tipo di cena,
e se hai già dei vini in mente.

### Scenario 5 — Nuova preferenza espressa
Dopo un suggerimento dici "Quella birra mi è piaciuta molto".
L'agente la aggiunge ai tuoi preferiti e aggiorna il profilo
per essere ancora più preciso la prossima volta.

---

## Cosa questa skill NON fa

- **Non fornisce valutazioni professionali di degustazione.** I
  suggerimenti si basano su dati oggettivi (stile, gradazione,
  amarezza) e sulle preferenze dichiarate. Non sostituisce un
  sommelier umano in contesti formali.

- **Non gestisce altre bevande.** Liquori, cocktail, superalcolici,
  bibite, analcolici — tutto ciò che non è birra o vino viene
  ignorato.

---

## Licenza
MIT