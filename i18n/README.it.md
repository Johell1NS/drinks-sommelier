# drinks-sommelier

<p align="center">
  <img src="../img/drinks-sommelier-logo.png" alt="drinks-sommelier" width="600">
</p>

<p align="center"><a href="../README.md">English</a> · <a href="README.zh-CN.md">简体中文</a> · <b>Italiano</b> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.pt-BR.md">Português (Brasil)</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.ru.md">Русский</a> · <a href="README.ar.md">العربية</a> · <a href="README.hi.md">हिन्दी</a> · <a href="README.it.md">Italiano</a></p>

<p align="center">
  <strong>Un sommelier in tasca, sempre al tuo fianco.</strong><br>
  <em>Scaffali, menu, enoteche: ovunque tu sia, sa cosa consigliarti.</em>
</p>

> **Una skill per agenti AI.** OpenClaw, Hermes Agent, OpenCode, Claude Code, Cursor e oltre.
> Un sommelier virtuale specializzato in birre e vini che impara i tuoi gusti
> personali e suggerisce la scelta migliore da qualsiasi scaffale, menu
> o lista. **Gratuita, open-source, self-hosted.**

---

## Perché esiste

Al ristorante, al pub, in enoteca, al supermercato: il problema è sempre
lo stesso. **Decine di opzioni e nessuna certezza** su cosa scegliere che sia
veramente adatto ai tuoi gusti.

Potresti chiedere al cameriere, aprire cinque schede sul telefono, o
sperare che il nome più bello sia anche il migliore. Oppure puoi chiedere
al tuo agente AI — e lui sa già cosa ti piace.

**drinks-sommelier** insegna a qualsiasi agente AI a comportarsi come un
sommelier personale. L'agente:

1. Impara le tue preferenze di gusto, una volta per tutte
2. Analizza qualsiasi input: foto di uno scaffale, menu digitali, elenchi
   di nomi scritti dall'utente
3. Cerca informazioni aggiornate su ogni prodotto
4. Confronta ogni prodotto con il tuo profilo di gusto
5. Ti dice esattamente cosa scegliere — e perché

Il tutto in modo trasparente, onesto, gratuito e senza inventare nulla.

---

## Vantaggi

- **Impara i tuoi gusti nel tempo.** Più usi la skill, più l'agente
  conosce il tuo palato. Ogni interazione perfeziona il profilo.

- **Birre e vini in un'unica skill.** Non devi installare due skill
  separate. L'agente gestisce entrambe le categorie, riconoscendo automaticamente
  cosa sta analizzando.

- **Analisi da immagini e testo.** Scatta una foto di uno scaffale, un menu,
  una lista vini. Oppure scrivi un elenco. L'agente estrae solo
  i prodotti rilevanti (birre e vini), ignorando tutto il resto.

- **Niente allucinazioni.** L'agente ha il divieto assoluto di usare
  la propria conoscenza di pre-addestramento. Ogni prodotto viene
  prontamente cercato sul web prima di essere valutato.

- **Indice di preferenza 0-100%.** Ogni suggerimento ha un punteggio
  chiaro che indica quanto un prodotto si adatta ai tuoi gusti. Niente
  mezze misure.

- **Profilo di gusto persistente.** Le tue preferenze sono salvate in
  file di testo leggibili e modificabili. Non si perdono tra
  una sessione e l'altra.

- **Configurazione guidata dall'agente.** La prima volta, l'agente ti fa le
  domande giuste per capire i tuoi gusti, senza lasciarti davanti a
  configurazioni manuali.

- **Open-source, licenza MIT.** Gratuita, senza abbonamenti, senza
  chiavi API, senza limiti. Puoi usarla, modificarla, distribuirla.

- **Funziona con qualsiasi agente AI.** Scritta per OpenCode, ma
  facilmente convertibile per OpenClaw, Hermes Agent, Claude Code, Cursor,
  GitHub Copilot e qualsiasi altro agente. Mostra questo README al tuo
  agente per una conversione semplice e automatica.

- **Completamente personalizzabile.** SKILL.md è un file di testo.
  Aggiungi regole, modifica criteri, adattala al tuo flusso di lavoro.

---

⭐ **Ti piace drinks-sommelier?** Metti una stella, segui il progetto
e aiuta a farlo crescere. Le migliori raccomandazioni sono quelle
che si condividono — suggerimenti e contributi sono sempre graditi.

---

## Come funziona

Il processo è diviso in 5 fasi, eseguite in sequenza dall'agente ogni
volta che viene interrogato.

### Fase 1 — Impostazione del profilo di gusto (una tantum)

La prima volta che la skill viene caricata, l'agente verifica se i
paragrafi "Gusti dell'utente per le birre" e "Gusti dell'utente per i
vini" in SKILL.md sono già stati compilati.

Se non lo sono, l'agente apre il file `data/SETUP.md` che contiene:
- Domande guida per raccogliere le preferenze (dolce/amaro, gradazione alcolica,
  stili graditi e non graditi, ecc.)
- Esempi di paragrafi compilati correttamente
- Esempi di file `data/` popolati

L'agente ti fa le domande, raccoglie le risposte e modifica
i due paragrafi sui gusti in SKILL.md. Se durante la
configurazione l'utente menziona prodotti specifici, l'agente
li registra nei corrispondenti file `data/` (operazione
opzionale ma utile per affinare il profilo).

Puoi anche compilare i paragrafi a mano, se preferisci.

I file `data/known-preferred-beers.md` e `data/known-preferred-wines.md`
sono opzionali e contengono prodotti specifici che hai già valutato
in passato. Più sono completi, più l'agente capisce le tue sfumature.

### Fase 2 — Analisi dell'input

L'agente identifica cosa hai a disposizione e in quale formato:

- **Testo**: estrae i nomi di birre e vini da un elenco scritto
- **Immagine**: analizza la foto (scaffale, menu, lista vini) e
  riconosce solo i prodotti che sono birre o vini.
  Ignora completamente: superalcolici, liquori, snack, pasti,
  dessert, bibite, accessori. Qualsiasi cosa non sia birra o vino.
- **Misto**: se invii sia testo che immagini, analizza tutto.

Se l'input non è chiaro, l'agente chiede prima di procedere.

### Fase 3 — Ricerca web (anti-allucinazione)

L'agente ha il **divieto assoluto** di usare la propria
conoscenza di pre-addestramento per valutare un prodotto. Potrebbe essere obsoleta,
imprecisa, o peggio: inventata. Per questo motivo, effettua una ricerca web mirata
su ogni singolo prodotto identificato.

Cosa cerca l'agente:

| Categoria | Informazioni raccolte |
|---|---|
| **Birre** | Stile, gradazione alcolica, dolcezza, amaro (IBU), corpo, note aromatiche, ingredienti |
| **Vini** | Vitigno, denominazione, zona di produzione, annata, corpo, acidità, tannicità, gradazione alcolica, note di dolcezza |

Se un prodotto non è reperibile online, l'agente lo dichiara onestamente
e non inventa caratteristiche.

### Fase 4 — Valutazione

L'agente confronta ogni prodotto con il tuo profilo di gusto, che ha
due livelli distinti:

1. **Regole di gusto** — le linee guida generali che hai scritto
   nei paragrafi sui gusti (es. "birre dolci", "vini non troppo
   dolci", "gradazione alcolica ≤ 9°"). Sono vincolanti.
2. **Prodotti nei file data/** — esempi concreti di birre e vini
   che ti sono piaciuti o non piaciuti. Servono a calibrare le
   regole di gusto (es. se ami la birra X e odi la Y, l'agente
   capisce cosa intendi per "dolce" e "amaro").

L'agente assegna un **indice di preferenza da 0 a 100%**:

| Indice | Significato |
|---|---|
| 90-100% | Prodotto perfetto per i tuoi gusti |
| 70-89% | Eccellente, lievi discrepanze |
| 50-69% | Accettabile, ma non ottimale |
| 30-49% | Poco adatto ai tuoi gusti |
| 0-29% | Da evitare |

Se hai indicato un contesto alimentare, l'agente valuta anche
l'abbinamento (priorità secondaria).

### Fase 5 — Raccomandazione

L'agente struttura la risposta in modo chiaro:

1. **Prima scelta**: il prodotto migliore con indice di preferenza
   e spiegazione del perché è adatto ai tuoi gusti
2. **Alternative** (se presenti): in ordine decrescente di preferenza
3. **Abbinamenti**: suggerimenti di abbinamento per i prodotti
4. **Prodotti da evitare**: quelli che chiaramente non rispettano
   i tuoi gusti, con spiegazione

---

## Struttura del progetto

```
drinks-sommelier/
├── README.md                ← Questo file
├── LICENSE                  ← Licenza MIT
├── .gitignore
├── img/                     ← Logo e risorse grafiche
├── i18n/                    ← Traduzioni
└── skills/
    └── drinks-sommelier/    ← La skill vera e propria
        ├── SKILL.md         ← Istruzioni complete per l'agente
        │                      (frontmatter, gusti, operatività,
        │                       casi limite, best practices, esempi,
        │                       aggiornamenti delle preferenze)
        └── data/
            ├── SETUP.md                   ← Guida configurazione iniziale
            │                                (usata solo al primo avvio)
            ├── known-preferred-beers.md   ← Birre apprezzate e non apprezzate
            │                                (da compilare con l'uso)
            └── known-preferred-wines.md   ← Vini apprezzati e non apprezzati
                                              (da compilare con l'uso)
```

---

## Installazione

Puoi installare la skill in due modi:

### Con npx skills (consigliato)

```bash
npx skills add Johell1NS/drinks-sommelier --skill drinks-sommelier
```

### Con git clone

```bash
git clone https://github.com/Johell1NS/drinks-sommelier.git
```

> **Nota:** a differenza di `npx skills add`, git clone non sa dove
> sono salvate le skill del tuo agente. Devi posizionare la skill nel percorso
> corretto per il tuo agente (es. OpenCode usa `~/.config/opencode/skills/`,
> altri agenti potrebbero differire). Una volta lì, l'agente la rileva
> automaticamente.

---

## Configurazione

La skill ha bisogno di conoscere i tuoi gusti per funzionare. Puoi
configurarla in due modi:

### Configurazione guidata (consigliata)

Dopo aver installato la skill, chiedi al tuo agente qualcosa come
"Aiutami a configurare la skill drinks-sommelier". L'agente caricherà
SKILL.md, troverà i paragrafi sui gusti ancora da compilare e ti
guiderà attraverso la configurazione iniziale usando `data/SETUP.md`.

In alternativa, chiedi semplicemente un consiglio su birra o vino:
l'agente rileverà automaticamente che la skill non è inizializzata
e ti farà le domande giuste.

### Configurazione manuale

Apri `SKILL.md` e compila i paragrafi:

**Gusti dell'utente per le birre**
```
Preferisco birre dolci e non amare.
Non devono superare i 9° di gradazione alcolica.
Mi piacciono gli stili belga e le birre fruttate.
Non mi piacciono le IPA, le stout e le birre troppo amare.
```

**Gusti dell'utente per i vini**
```
Preferisco vini rossi non troppo dolci.
Per i bianchi, preferisco vermentino e sauvignon.
Mi piacciono vini con buona acidità e freschezza.
Non mi piacciono i vini passiti o liquorosi.
```

Puoi anche popolare i file `data/known-preferred-beers.md` e
`data/known-preferred-wines.md` con prodotti specifici che hai già
provato e valutato. Questa parte è opzionale ma utile
per affinare il profilo.

**Esempio — `data/known-preferred-beers.md`**
```
# BIRRE APPREZZATE
- Kwak
- Triple Karmeliet
- La Trappe Blond
- Flea Margherita

# BIRRE NON APPREZZATE
- Qualsiasi IPA
- Stout
- Birre con gradazione alcolica superiore a 9°
```

**Esempio — `data/known-preferred-wines.md`**
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

Ogni volta che esprimi un giudizio su un prodotto ("Questo mi piace",
"Questo non mi piace"), l'agente aggiorna automaticamente i
file `data/`. Le regole di gusto nei paragrafi di SKILL.md, invece,
vengono aggiornate solo con la tua conferma esplicita, perché
sono vincolanti per le valutazioni future.

---

## Esempi di utilizzo

### Scenario 1 — Scaffale di vini (immagine)
Scatti una foto di uno scaffale di un'enoteca. L'agente identifica i vini,
li cerca tutti sul web, li confronta con il tuo profilo. Ti dice
quale scegliere, perché e con cosa abbinarlo.

### Scenario 2 — Menu di birre (immagine)
Scatti una foto del menu delle birre di un pub. L'agente ignora cocktail,
superalcolici, ecc... analizza solo le birre, cerca informazioni su
ciascuna. Suggerisce la birra più adatta ai tuoi gusti.

### Scenario 3 — Elenco di testo misto
Scrivi "Ho questi vini: Chianti Classico, Vermentino Costamolino,
Amarone. E queste birre: Kwak, IPA artigianale locale, Leffe Blonde."
L'agente valuta entrambe le categorie e ti dice qual è la scelta
migliore in assoluto.

### Scenario 4 — Richiesta senza elenco
"Devo prendere un vino per una cena, cosa mi consigli?" L'agente
non inventa. Chiede cosa hai a disposizione, che tipo di cena
e se hai già qualche vino in mente.

### Scenario 5 — Nuova preferenza espressa
Dopo un suggerimento dici "Quella birra mi è piaciuta molto".
L'agente la aggiunge ai tuoi preferiti e aggiorna il profilo
per essere ancora più preciso la prossima volta.

---

## Cosa questa skill NON fa

- **Non fornisce valutazioni di degustazione professionali.** I
  suggerimenti si basano su dati oggettivi (stile, gradazione alcolica,
  amaro) e sulle preferenze dichiarate. Non sostituisce un
  sommelier umano in contesti formali.

- **Non gestisce altre bevande.** Superalcolici, cocktail, liquori,
  bibite, bevande analcoliche — qualsiasi cosa non sia birra o vino viene
  ignorata.

---

## Suggerimenti (opzionale)

**drinks-sommelier** funziona con qualsiasi strumento di ricerca web che il tuo agente
supporti nativamente. Se il tuo agente ha già capacità di ricerca web affidabili,
non ti serve altro.

Tuttavia, se vuoi garantire ricerche approfondite e resistenti agli antibot
ogni volta (particolarmente utile quando le pagine dei prodotti sono dietro sistemi antibot),
considera l'installazione della skill complementare
**[browser-search](https://github.com/Johell1NS/browser-search)**.
Cerca decine di motori simultaneamente e aiuta l'agente a trovare
informazioni sui prodotti anche quando gli strumenti standard faticano.

---

## Licenza
MIT
