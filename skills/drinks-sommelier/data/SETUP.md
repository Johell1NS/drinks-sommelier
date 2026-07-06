# drinks-sommelier — Guida alla configurazione iniziale

Questa guida viene usata dall'agente **solo** quando la skill viene caricata per la prima volta e i paragrafi dei gusti non sono ancora stati compilati. Dopo la prima configurazione, questo file non serve più.

---

## Cosa deve fare l'agente

1. Spiegare brevemente all'utente che la skill ha bisogno di conoscere i suoi gusti per funzionare
2. Fare domande mirate per compilare i paragrafi dei gusti, partendo dal generale al particolare
3. Dopo aver raccolto le preferenze, **modifica ESCLUSIVAMENTE i paragrafi** "Gusti dell'utente per le birre" e "Gusti dell'utente per i vini" nel file `SKILL.md`, sostituendo il testo "Inserisci qui le preferenze" con quanto appreso. Non alterare nessun'altra sezione del file.
4. **Prima di modificare**, rileggi attentamente `SKILL.md` per individuare con precisione le righe da sostituire
5. (Facoltativo) Popolare i file `data/` con i prodotti specifici che l'utente menziona
6. Verificare di aver capito correttamente prima di procedere

---

## Esempi per compilare i paragrafi dei gusti

### Esempio — Paragrafo "Gusti dell'utente per le birre" (compilato)

```
Preferisco birre dolci e non amare.
Non devono superare i 9° di gradazione alcolica.
Mi piacciono gli stili belga (blond, tripel, witbier), le birre fruttate e le sour.
Non mi piacciono IPA, stout e birre troppo luppolate o amare.
Preferisco corpi medio-leggeri e carbonazione media.
```

### Esempio — Paragrafo "Gusti dell'utente per i vini" (compilato)

```
Preferisco vini rossi non troppo dolci, corposi ma equilibrati.
Per i bianchi, prediligo vermentino, sauvignon e fiano.
Mi piacciono vini con buona acidità e freschezza.
Non mi piacciono vini troppo dolci, passiti o liquorosi.
Preferisco vini italiani, in particolare del centro-sud.
```

---

## Esempi per compilare i file data/

### Esempio — `data/birre-note-preferite.md`

```markdown
# BIRRE APPREZZATE
- Kwak
- Super open Baladin
- Lisa Birra del Borgo
- Bloemenbier
- Denti Stretti Jungle Juice
- Flea Margherita
- Flea Violante
- Flea Bianca Lancia
- Ape Regina
- 60° north Shetland lager
- Cairngorm lager
- Triple Karmeliet
- La Trappe Blond
- Mastri Birrai Umbri Cotta 68
- Baladin Nazionale Blanche

# BIRRE NON APPREZZATE
- Qualsiasi IPA
- Stout
- Birre con gradazione superiore a 9°
```

### Esempio — `data/vini-noti-preferiti.md`

```markdown
# VINI APPREZZATI
- Vermentino Costamolino
- Alice Verdeca Produttori di Manduria
- Fiano Zin Produttori di Manduria
- Sauvignon Bosco della Donna
- Virtù Romane Tenuta Le Quinte
- Heredio Casale Valle Chiesa
- 15 Gradi Cantolio
- Camelot Firriato
- Rebeca Firriato
- Vulcano Donna Fugata
- Matermatuta Casale del Giglio
- Syrah Soraia Casale Valle Chiesa
- Rosso Bastardo Cesarini Sartori
- Mandonion Cantolio
- I 4 Mori Castel de Paolis

# VINI NON APPREZZATI
- Vini passiti
- Vini liquorosi
- Vini troppo dolci in generale
```

---

## Domande guida per l'agente

Se l'utente non sa da dove iniziare, l'agente può fare queste domande in ordine:

**Per le birre:**
1. "Preferisci birre dolci o amare?"
2. "Che gradazione alcolica massima preferisci?"
3. "Hai stili di birra che ti piacciono in particolare? (es. bionde, rosse, fruttate, speziate)"
4. "Ci sono stili che non sopporti? (es. IPA, stout, amare)"
5. "Hai qualche birra specifica che sai già di apprezzare?"

**Per i vini:**
1. "Preferisci vini rossi, bianchi, o entrambi?"
2. "Per i rossi, li preferisci più secchi o più morbidi?"
3. "Hai vitigni preferiti? (es. vermentino, syrah, fiano)"
4. "Hai preferenze geografiche? (es. vini italiani, francesi, di una regione specifica)"
5. "Hai qualche vino specifico che sai già di apprezzare?"

---

## Verifica finale

Prima di considerare la configurazione completata, assicurati che:
- [ ] Il paragrafo "Gusti dell'utente per le birre" in `SKILL.md` contenga almeno 2-3 informazioni (es. dolce/amaro, gradazione)
- [ ] Il paragrafo "Gusti dell'utente per i vini" in `SKILL.md` contenga almeno 2-3 informazioni (es. rosso/bianco, secco/dolce)
- [ ] (Facoltativo) I file `data/` contengano almeno i prodotti eventualmente citati dall'utente
- [ ] L'utente abbia confermato che il profilo è corretto

Se anche solo una linea guida è presente, la skill può iniziare a funzionare. I dettagli si perfezioneranno con l'uso.
