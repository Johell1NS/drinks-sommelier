# drinks-sommelier

<p align="center">
  <img src="../img/drinks-sommelier-logo.png" alt="drinks-sommelier" width="600">
</p>

<p align="center"><a href="../README.md">English</a> · <a href="README.zh-CN.md">简体中文</a> · <a href="README.es.md">Español</a> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.pt-BR.md">Português (Brasil)</a> · <a href="README.fr.md">Français</a> · <b>Deutsch</b> · <a href="README.ru.md">Русский</a> · <a href="README.ar.md">العربية</a> · <a href="README.hi.md">हिन्दी</a> · <a href="README.it.md">Italiano</a></p>

<p align="center">
  <strong>Ein Sommelier in deiner Tasche, immer an deiner Seite.</strong><br>
  <em>Regale, Speisekarten, Weinkeller: wo immer du bist, er weiß, was er empfehlen soll.</em>
</p>

> **Eine Skill für KI-Agenten.** OpenClaw, Hermes Agent, OpenCode, Claude Code, Cursor und mehr.
> Ein virtueller Sommelier, spezialisiert auf Biere und Weine, der deine
> persönlichen Vorlieben lernt und die beste Wahl aus jedem Regal, jeder Speisekarte
> oder jeder Liste vorschlägt. **Kostenlos, Open-Source, selbst gehostet.**

---

## Warum es das gibt

Im Restaurant, in der Kneipe, im Weinhandel, im Supermarkt: Das Problem ist immer
das gleiche. **Dutzende Optionen und keine Gewissheit**, was wirklich
zu deinem Geschmack passt.

Du könntest den Kellner fragen, fünf Tabs auf dem Handy öffnen oder
hoffen, dass der schönste Name auch der beste ist. Oder du fragst
deinen KI-Agenten – und er weiß bereits, was du magst.

**drinks-sommelier** bringt jedem KI-Agenten bei, als persönlicher
Sommelier zu agieren. Der Agent:

1. Lernt deine Geschmacksvorlieben ein für alle Mal
2. Analysiert jede Eingabe: Foto eines Regals, digitale Speisekarten, vom
   Benutzer geschriebene Namenslisten
3. Sucht aktuelle Informationen zu jedem Produkt
4. Vergleicht jedes Produkt mit deinem Geschmacksprofil
5. Sagt dir genau, was du nehmen sollst – und warum

Alles transparent, ehrlich, kostenlos und ohne etwas zu erfinden.

---

## Vorteile

- **Lernt deinen Geschmack mit der Zeit.** Je öfter du die Skill nutzt, desto besser
  kennt der Agent deinen Gaumen. Jede Interaktion verfeinert das Profil.

- **Biere und Weine in einer einzigen Skill.** Du musst nicht zwei separate
  Skills installieren. Der Agent verarbeitet beide Kategorien und erkennt
  automatisch, was er analysiert.

- **Analyse von Bildern und Text.** Mache ein Foto von einem Regal, einer Speisekarte,
  einer Weinkarte. Oder schreibe eine Liste. Der Agent extrahiert nur
  die relevanten Produkte (Biere und Weine) und ignoriert alles andere.

- **Keine Halluzinationen.** Der Agent hat das absolute Verbot, sein
  eigenes Vorwissen zu verwenden. Jedes Produkt wird
  umgehend im Internet recherchiert, bevor es bewertet wird.

- **Präferenzindex 0–100 %.** Jede Empfehlung hat eine klare
  Bewertung, die angibt, wie gut ein Produkt zu deinem Geschmack passt. Keine
  halben Sachen.

- **Beständiges Geschmacksprofil.** Deine Vorlieben werden in lesbaren
  und bearbeitbaren Textdateien gespeichert. Sie gehen nicht zwischen
  einer Sitzung und der nächsten verloren.

- **Agent-geführte Einrichtung.** Beim ersten Mal stellt dir der Agent die
  richtigen Fragen, um deinen Geschmack zu verstehen, ohne dich vor
  manuelle Konfigurationen zu setzen.

- **Open-Source, MIT-Lizenz.** Kostenlos, keine Abonnements, keine
  API-Schlüssel, keine Grenzen. Du kannst es nutzen, modifizieren, verbreiten.

- **Funktioniert mit jedem KI-Agenten.** Geschrieben für OpenCode, aber
  einfach konvertierbar für OpenClaw, Hermes Agent, Claude Code, Cursor,
  GitHub Copilot und jeden anderen Agenten. Zeige dieses README deinem
  Agenten für eine einfache und automatische Konvertierung.

- **Vollständig anpassbar.** SKILL.md ist eine Textdatei.
  Füge Regeln hinzu, ändere Kriterien, passe sie an deinen Workflow an.

---

⭐ **Gefällt dir drinks-sommelier?** Gib einen Stern, folge dem Projekt
und hilf mit, es wachsen zu lassen. Die besten Empfehlungen sind die,
die man teilt — Vorschläge und Beiträge sind immer willkommen.

---

## Wie es funktioniert

Der Prozess ist in 5 Phasen unterteilt, die vom Agenten bei jeder
Anfrage nacheinander ausgeführt werden.

### Phase 1 – Geschmacksprofil einrichten (einmalig)

Beim ersten Laden der Skill prüft der Agent, ob die
Absätze „Geschmack des Benutzers für Biere" und „Geschmack des Benutzers für
Weine" in der SKILL.md bereits ausgefüllt sind.

Falls nicht, öffnet der Agent die Datei `data/SETUP.md`, die Folgendes enthält:
- Leitfragen zur Ermittlung der Vorlieben (süß/bitter, Alkoholgehalt,
  gemochte und nicht gemochte Stile usw.)
- Beispiele für korrekt ausgefüllte Absätze
- Beispiele für befüllte `data/`-Dateien

Der Agent stellt dir die Fragen, sammelt die Antworten und ändert
die beiden Geschmacksabsätze in der SKILL.md. Wenn der Benutzer während
der Einrichtung bestimmte Produkte erwähnt, zeichnet der Agent
sie in den entsprechenden `data/`-Dateien auf (optionaler
Vorgang, aber nützlich zur Verfeinerung des Profils).

Du kannst die Absätze auch von Hand ausfüllen, wenn du möchtest.

Die Dateien `data/known-preferred-beers.md` und `data/known-preferred-wines.md`
sind optional und enthalten bestimmte Produkte, die du bereits in der
Vergangenheit bewertet hast. Je vollständiger sie sind, desto besser versteht der Agent
deine Nuancen.

### Phase 2 – Eingabeanalyse

Der Agent ermittelt, was dir vorliegt und in welchem Format:

- **Text**: Extrahiert die Namen von Bieren und Weinen aus einer geschriebenen Liste
- **Bild**: Analysiert das Foto (Regal, Speisekarte, Weinkarte) und
  erkennt nur Produkte, die Biere oder Weine sind.
  Vollständig ignoriert werden: Spirituosen, Liköre, Snacks, Gerichte,
  Desserts, Softdrinks, Zubehör. Alles, was kein Bier oder Wein ist.
- **Gemischt**: Wenn du sowohl Text als auch Bilder sendest, analysiert er alles.

Wenn die Eingabe nicht klar ist, fragt der Agent nach, bevor er fortfährt.

### Phase 3 – Internetrecherche (Anti-Halluzination)

Der Agent hat das **absolute Verbot**, sein eigenes
Vorwissen zur Bewertung eines Produkts zu verwenden. Es könnte veraltet,
ungenau oder schlimmer noch: erfunden sein. Aus diesem Grund führt er eine gezielte Internetsuche
zu jedem einzelnen identifizierten Produkt durch.

Was der Agent sucht:

| Kategorie | Gesammelte Informationen |
|---|---|
| **Biere** | Stil, Alkoholgehalt, Süße, Bitterkeit (IBU), Körper, Aromen, Zutaten |
| **Weine** | Rebsorte, Herkunftsbezeichnung, Anbaugebiet, Jahrgang, Körper, Säure, Tannine, Alkoholgehalt, Süßnoten |

Wenn ein Produkt online nicht auffindbar ist, gibt der Agent dies ehrlich an
und erfindet keine Eigenschaften.

### Phase 4 – Bewertung

Der Agent vergleicht jedes Produkt mit deinem Geschmacksprofil, das
zwei verschiedene Ebenen hat:

1. **Geschmacksregeln** – die allgemeinen Richtlinien, die du in den
   Geschmacksabsätzen festgehalten hast (z. B. „süße Biere", „nicht zu
   süße Weine", „Alkoholgehalt ≤ 9 %"). Sie sind verbindlich.
2. **Produkte in den data/-Dateien** – konkrete Beispiele für Biere und Weine,
   die du gemocht oder nicht gemocht hast. Sie dienen dazu, die
   Geschmacksregeln zu kalibrieren (z. B. wenn du Bier X liebst und Y hasst,
   versteht der Agent, was du mit „süß" und „bitter" meinst).

Der Agent weist einen **Präferenzindex von 0 bis 100 %** zu:

| Index | Bedeutung |
|---|---|
| 90–100 % | Perfektes Produkt für deinen Geschmack |
| 70–89 % | Ausgezeichnet, geringfügige Abweichungen |
| 50–69 % | Akzeptabel, aber nicht optimal |
| 30–49 % | Kaum geeignet für deinen Geschmack |
| 0–29 % | Zu vermeiden |

Wenn du einen Essenskontext angegeben hast, bewertet der Agent auch
die Speisenbegleitung (zweitrangige Priorität).

### Phase 5 – Empfehlung

Der Agent strukturiert die Antwort klar:

1. **Erste Wahl**: das beste Produkt mit Präferenzindex
   und Erklärung, warum es zu deinem Geschmack passt
2. **Alternativen** (falls vorhanden): in absteigender Reihenfolge der Präferenz
3. **Begleitung**: Speisenbegleitungsvorschläge für die Produkte
4. **Zu vermeidende Produkte**: diejenigen, die deinen Geschmack eindeutig
   nicht respektieren, mit Erklärung

---

## Projektstruktur

```
drinks-sommelier/
├── README.md                ← Diese Datei
├── LICENSE                  ← MIT-Lizenz
├── .gitignore
├── img/                     ← Logo und Grafikressourcen
├── i18n/                    ← Übersetzungen
└── skills/
    └── drinks-sommelier/    ← Die eigentliche Skill
        ├── SKILL.md         ← Vollständige Anweisungen für den Agenten
        │                      (Frontmatter, Geschmäcker, Abläufe,
        │                       Edge Cases, Best Practices, Beispiele,
        │                       Präferenzaktualisierungen)
        └── data/
            ├── SETUP.md                   ← Leitfaden zur Ersteinrichtung
            │                                (nur beim ersten Start verwendet)
            ├── known-preferred-beers.md   ← Gemochte und nicht gemochte Biere
            │                                (wird mit der Nutzung befüllt)
            └── known-preferred-wines.md   ← Gemochte und nicht gemochte Weine
                                              (wird mit der Nutzung befüllt)
```

---

## Installation

Du kannst die Skill auf zwei Arten installieren:

### Mit npx skills (empfohlen)

```bash
npx skills add Johell1NS/drinks-sommelier --skill drinks-sommelier
```

### Mit git clone

```bash
git clone https://github.com/Johell1NS/drinks-sommelier.git
```

> **Hinweis:** Im Gegensatz zu `npx skills add` weiß git clone nicht, wo
> die Skills deines Agenten gespeichert sind. Du musst die Skill in den richtigen
> Pfad für deinen Agenten legen (z. B. verwendet OpenCode `~/.config/opencode/skills/`,
> andere Agenten können abweichen). Ist sie erst einmal dort, erkennt sie der Agent
> automatisch.

---

## Konfiguration

Die Skill muss deine Vorlieben kennen, um zu funktionieren. Du kannst
sie auf zwei Arten konfigurieren:

### Geführte Konfiguration (empfohlen)

Nach der Installation der Skill bitte deinen Agenten etwa mit
„Hilf mir, die drinks-sommelier-Skill zu konfigurieren". Der Agent lädt
SKILL.md, findet die noch auszufüllenden Geschmacksabsätze und
führt dich mit Hilfe von `data/SETUP.md` durch die Ersteinrichtung.

Alternativ bitte einfach um eine Bier- oder Weinempfehlung:
Der Agent erkennt automatisch, dass die Skill nicht initialisiert ist,
und stellt dir die richtigen Fragen.

### Manuelle Konfiguration

Öffne `SKILL.md` und fülle die Absätze aus:

**Geschmack des Benutzers für Biere**
```
Ich bevorzuge süße und nicht bittere Biere.
Sie dürfen 9 Vol.-% Alkohol nicht überschreiten.
Ich mag belgische Stile und fruchtige Biere.
Ich mag keine IPAs, Stouts und zu bittere Biere.
```

**Geschmack des Benutzers für Weine**
```
Ich bevorzuge Rotweine, die nicht zu süß sind.
Bei Weißweinen bevorzuge ich Vermentino und Sauvignon.
Ich mag Weine mit guter Säure und Frische.
Ich mag keine Passito- oder Likörweine.
```

Du kannst auch die Dateien `data/known-preferred-beers.md` und
`data/known-preferred-wines.md` mit bestimmten Produkten befüllen, die du
bereits probiert und bewertet hast. Dieser Teil ist optional, aber nützlich,
um das Profil zu verfeinern.

**Beispiel – `data/known-preferred-beers.md`**
```
# LIKED BEERS
- Kwak
- Triple Karmeliet
- La Trappe Blond
- Flea Margherita

# DISLIKED BEERS
- Any IPA
- Stout
- Beers with alcohol content above 9°
```

**Beispiel – `data/known-preferred-wines.md`**
```
# LIKED WINES
- Vermentino Costamolino
- Syrah Soraia Casale Valle Chiesa
- Rebeca Firriato

# DISLIKED WINES
- Passito wines
- Fortified wines
```

### Aktualisierung im Laufe der Zeit

Jedes Mal, wenn du ein Urteil zu einem Produkt abgibst („Das mag ich",
„Das mag ich nicht"), aktualisiert der Agent automatisch die
`data/`-Dateien. Die Geschmacksregeln in den SKILL.md-Absätzen hingegen werden
nur mit deiner ausdrücklichen Bestätigung aktualisiert, da
sie für zukünftige Bewertungen verbindlich sind.

---

## Anwendungsbeispiele

### Szenario 1 – Weinregal (Bild)
Du machst ein Foto von einem Weinregal im Geschäft. Der Agent identifiziert die Weine,
recherchiert sie alle im Internet und vergleicht sie mit deinem Profil. Er sagt dir,
welchen du nehmen sollst, warum und wozu er passt.

### Szenario 2 – Bierkarte (Bild)
Du machst ein Foto von der Bierkarte einer Kneipe. Der Agent ignoriert Cocktails,
Spirituosen usw. ... analysiert nur die Biere, sucht Informationen zu
jedem einzelnen. Er schlägt das Bier vor, das am besten zu deinem Geschmack passt.

### Szenario 3 – Gemischte Textliste
Du schreibst: „Ich habe diese Weine: Chianti Classico, Vermentino Costamolino,
Amarone. Und diese Biere: Kwak, lokales Craft-IPA, Leffe Blonde."
Der Agent bewertet beide Kategorien und sagt dir, welche insgesamt die
beste Wahl ist.

### Szenario 4 – Anfrage ohne Liste
„Ich brauche einen Wein für ein Abendessen, was empfiehlst du?" Der Agent
erfindet nichts. Er fragt, was du zur Verfügung hast, um was für ein Abendessen
es sich handelt und ob du bereits bestimmte Weine im Kopf hast.

### Szenario 5 – Neue Vorliebe geäußert
Nach einem Vorschlag sagst du: „Dieses Bier hat mir wirklich gut gefallen."
Der Agent fügt es deinen Favoriten hinzu und aktualisiert das Profil,
damit es beim nächsten Mal noch präziser ist.

---

## Was diese Skill NICHT tut

- **Sie liefert keine professionellen Verkostungsbewertungen.** Die
  Empfehlungen basieren auf objektiven Daten (Stil, Alkoholgehalt,
  Bitterkeit) und auf erklärten Vorlieben. Sie ersetzt keinen
  menschlichen Sommelier in formellen Kontexten.

- **Sie verarbeitet keine anderen Getränke.** Spirituosen, Cocktails, Liköre,
  Softdrinks, alkoholfreie Getränke – alles, was kein Bier oder Wein ist, wird
  ignoriert.

---

## Empfehlungen (optional)

**drinks-sommelier** funktioniert mit jedem Werkzeug zur Internetsuche, das dein Agent
nativ unterstützt. Wenn dein Agent bereits zuverlässige Suchfunktionen im Internet hat,
brauchst du nichts weiter.

Wenn du jedoch gründliche, Anti-Bot-resistente Suchen
jedes Mal sicherstellen möchtest (besonders nützlich, wenn Produktseiten hinter
Anti-Bot-Systemen liegen), solltest du die Begleit-Skill
**[browser-search](https://github.com/Johell1NS/browser-search)** installieren.
Sie durchsucht dutzende Suchmaschinen gleichzeitig und hilft dem Agenten,
Produktinformationen zu finden, selbst wenn Standardwerkzeuge Schwierigkeiten haben.

---

## Lizenz
MIT
