# drinks-sommelier

<p align="center">
  <img src="../img/drinks-sommelier-logo.png" alt="drinks-sommelier" width="600">
</p>

<p align="center"><a href="../README.md">English</a> · <a href="README.zh-CN.md">简体中文</a> · <b>Français</b> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.pt-BR.md">Português (Brasil)</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.ru.md">Русский</a> · <a href="README.ar.md">العربية</a> · <a href="README.hi.md">हिन्दी</a> · <a href="README.it.md">Italiano</a></p>

<p align="center">
  <strong>Un sommelier dans votre poche, toujours à vos côtés.</strong><br>
  <em>Rayons, menus, caves à vin : où que vous soyez, il sait quoi recommander.</em>
</p>

> **Une skill pour agents d'IA.** OpenClaw, Hermes Agent, OpenCode, Claude Code, Cursor et au-delà.
> Un sommelier virtuel spécialisé en bières et vins qui apprend vos goûts
> personnels et suggère le meilleur choix parmi n'importe quel rayon, menu
> ou liste. **Gratuit, open-source, auto-hébergé.**

---

## Pourquoi ça existe

Au restaurant, au pub, à la cave à vin, au supermarché : le problème est toujours
le même. **Des dizaines d'options et aucune certitude** sur ce qu'il faut choisir qui soit
véritablement adapté à vos goûts.

Vous pourriez demander au serveur, ouvrir cinq onglets sur votre téléphone, ou
espérer que le plus joli nom soit aussi le meilleur. Ou vous pouvez demander
à votre agent d'IA — et il sait déjà ce que vous aimez.

**drinks-sommelier** apprend à n'importe quel agent d'IA à agir comme un
sommelier personnel. L'agent :

1. Apprend vos préférences gustatives, une fois pour toutes
2. Analyse toute entrée : photo d'un rayon, menus numériques, listes
   de noms écrites par l'utilisateur
3. Recherche des informations à jour sur chaque produit
4. Compare chaque produit à votre profil gustatif
5. Vous dit exactement quoi choisir — et pourquoi

Le tout de manière transparente, honnête, gratuite et sans rien inventer.

---

## Avantages

- **Apprend vos goûts avec le temps.** Plus vous utilisez la skill, plus l'agent
  connaît votre palais. Chaque interaction affine le profil.

- **Bières et vins dans une seule skill.** Pas besoin d'installer deux skills
  séparées. L'agent gère les deux catégories, en reconnaissant automatiquement
  ce qu'il analyse.

- **Analyse à partir d'images et de texte.** Prenez une photo d'un rayon, d'un menu,
  d'une carte des vins. Ou écrivez une liste. L'agent extrait uniquement
  les produits pertinents (bières et vins), en ignorant tout le reste.

- **Pas d'hallucinations.** L'agent a l'interdiction absolue d'utiliser
  ses propres connaissances de pré-entraînement. Chaque produit est
  rapidement recherché sur le web avant d'être évalué.

- **Indice de préférence 0-100 %.** Chaque suggestion a un score
  clair qui indique à quel point un produit correspond à vos goûts. Pas
  de demi-mesures.

- **Profil gustatif persistant.** Vos préférences sont enregistrées dans
  des fichiers texte lisibles et modifiables. Elles ne sont pas perdues entre
  une session et la suivante.

- **Configuration guidée par l'agent.** La première fois, l'agent vous pose les
  bonnes questions pour comprendre vos goûts, sans vous laisser devant des
  configurations manuelles.

- **Open-source, licence MIT.** Gratuit, sans abonnement, sans
  clé API, sans limites. Vous pouvez l'utiliser, le modifier, le distribuer.

- **Fonctionne avec n'importe quel agent d'IA.** Écrit pour OpenCode, mais
  facilement convertible pour OpenClaw, Hermes Agent, Claude Code, Cursor,
  GitHub Copilot et tout autre agent. Montrez ce README à votre
  agent pour une conversion simple et automatique.

- **Entièrement personnalisable.** SKILL.md est un fichier texte.
  Ajoutez des règles, modifiez des critères, adaptez-le à votre flux de travail.

---

⭐ **Vous aimez drinks-sommelier ?** Mettez une étoile, suivez le projet
et aidez-le à grandir. Les meilleures recommandations sont celles
que l'on partage — suggestions et contributions sont toujours les bienvenues.

---

## Comment ça fonctionne

Le processus est divisé en 5 phases, exécutées en séquence par l'agent à chaque
fois qu'il est interrogé.

### Phase 1 — Configuration du profil gustatif (unique)

La première fois que la skill est chargée, l'agent vérifie si les
paragraphes « Goûts de l'utilisateur pour les bières » et « Goûts de l'utilisateur pour les
vins » dans SKILL.md ont déjà été remplis.

S'ils ne l'ont pas été, l'agent ouvre le fichier `data/SETUP.md` qui contient :
- Questions guidées pour recueillir les préférences (sucré/amer, teneur en alcool,
  styles aimés et non aimés, etc.)
- Exemples de paragraphes correctement remplis
- Exemples de fichiers `data/` renseignés

L'agent vous pose les questions, recueille les réponses et modifie
les deux paragraphes de goûts dans SKILL.md. Si pendant la
configuration l'utilisateur mentionne des produits spécifiques, l'agent
les enregistre dans les fichiers `data/` correspondants (opération
facultative mais utile pour affiner le profil).

Vous pouvez aussi remplir les paragraphes à la main, si vous préférez.

Les fichiers `data/known-preferred-beers.md` et `data/known-preferred-wines.md`
sont facultatifs et contiennent des produits spécifiques que vous avez déjà évalués
par le passé. Plus ils sont complets, plus l'agent comprend vos nuances.

### Phase 2 — Analyse de l'entrée

L'agent identifie ce que vous avez à disposition et sous quel format :

- **Texte** : extrait les noms de bières et de vins d'une liste écrite
- **Image** : analyse la photo (rayon, menu, carte des vins) et
  reconnaît uniquement les produits qui sont des bières ou des vins.
  Ignore complètement : spiritueux, liqueurs, snacks, plats,
  desserts, sodas, accessoires. Tout ce qui n'est pas bière ou vin.
- **Mixte** : si vous envoyez à la fois du texte et des images, il analyse tout.

Si l'entrée n'est pas claire, l'agent demande avant de procéder.

### Phase 3 — Recherche web (anti-hallucination)

L'agent a **l'interdiction absolue** d'utiliser ses propres
connaissances de pré-entraînement pour évaluer un produit. Elles pourraient être obsolètes,
imprécises, ou pire : inventées. Pour cette raison, il effectue une recherche web ciblée
sur chaque produit identifié.

Ce que l'agent recherche :

| Catégorie | Informations collectées |
|---|---|
| **Bières** | Style, teneur en alcool, sucrosité, amertume (IBU), corps, notes aromatiques, ingrédients |
| **Vins** | Cépage, appellation, région de production, millésime, corps, acidité, tanins, teneur en alcool, notes de sucrosité |

Si un produit est introuvable en ligne, l'agent le dit honnêtement
et n'invente pas de caractéristiques.

### Phase 4 — Évaluation

L'agent compare chaque produit à votre profil gustatif, qui comporte
deux niveaux distincts :

1. **Règles gustatives** — les directives générales que vous avez écrites
   dans les paragraphes de goûts (ex. « bières sucrées », « vins pas trop
   sucrés », « teneur en alcool ≤ 9° »). Elles sont contraignantes.
2. **Produits dans les fichiers data/** — des exemples concrets de bières et de vins
   que vous avez aimés ou non. Ils servent à calibrer les
   règles gustatives (ex. si vous aimez la bière X et détestez la Y, l'agent
   comprend ce que vous voulez dire par « sucré » et « amer »).

L'agent attribue un **indice de préférence de 0 à 100 %** :

| Indice | Signification |
|---|---|
| 90-100 % | Produit parfait pour vos goûts |
| 70-89 % | Excellent, légères divergences |
| 50-69 % | Acceptable, mais pas optimal |
| 30-49 % | Peu adapté à vos goûts |
| 0-29 % | À éviter |

Si vous avez indiqué un contexte alimentaire, l'agent évalue également
l'accord mets-boissons (priorité secondaire).

### Phase 5 — Recommandation

L'agent structure la réponse clairement :

1. **Premier choix** : le meilleur produit avec l'indice de préférence
   et une explication de pourquoi il correspond à vos goûts
2. **Alternatives** (si présentes) : par ordre décroissant de préférence
3. **Accords** : suggestions d'accords mets-boissons pour les produits
4. **Produits à éviter** : ceux qui ne respectent clairement pas
   vos goûts, avec explication

---

## Structure du projet

```
drinks-sommelier/
├── README.md                ← Ce fichier
├── LICENSE                  ← Licence MIT
├── .gitignore
├── img/                     ← Logo et ressources graphiques
├── i18n/                    ← Traductions
└── skills/
    └── drinks-sommelier/    ← La skill elle-même
        ├── SKILL.md         ← Instructions complètes pour l'agent
        │                      (frontmatter, goûts, opérations,
        │                       cas limites, bonnes pratiques, exemples,
        │                       mises à jour des préférences)
        └── data/
            ├── SETUP.md                   ← Guide de configuration initiale
            │                                (utilisé seulement au premier lancement)
            ├── known-preferred-beers.md   ← Bières aimées et non aimées
            │                                (à remplir avec l'usage)
            └── known-preferred-wines.md   ← Vins aimés et non aimés
                                              (à remplir avec l'usage)
```

---

## Installation

Vous pouvez installer la skill de deux manières :

### Avec npx skills (recommandé)

```bash
npx skills add Johell1NS/drinks-sommelier --skill drinks-sommelier
```

### Avec git clone

```bash
git clone https://github.com/Johell1NS/drinks-sommelier.git
```

> **Note :** contrairement à `npx skills add`, git clone ne sait pas où
> sont stockées les skills de votre agent. Vous devez placer la skill dans le chemin
> correct pour votre agent (ex. OpenCode utilise `~/.config/opencode/skills/`,
> d'autres agents peuvent différer). Une fois qu'elle y est, l'agent la détecte
> automatiquement.

---

## Configuration

La skill a besoin de connaître vos goûts pour fonctionner. Vous pouvez
la configurer de deux manières :

### Configuration guidée (recommandée)

Après avoir installé la skill, demandez à votre agent quelque chose comme
« Aide-moi à configurer la skill drinks-sommelier ». L'agent chargera
SKILL.md, trouvera les paragraphes de goûts encore à remplir, et vous
guidera à travers la configuration initiale en utilisant `data/SETUP.md`.

Sinon, demandez simplement une recommandation de bière ou de vin :
l'agent détectera automatiquement que la skill n'est pas initialisée
et vous posera les bonnes questions.

### Configuration manuelle

Ouvrez `SKILL.md` et remplissez les paragraphes :

**Goûts de l'utilisateur pour les bières**
```
Je préfère les bières sucrées et non amères.
Elles ne doivent pas dépasser 9° d'alcool par volume.
J'aime les styles belges et les bières fruitées.
Je n'aime pas les IPA, les stouts et les bières trop amères.
```

**Goûts de l'utilisateur pour les vins**
```
Je préfère les vins rouges pas trop sucrés.
Pour les blancs, je préfère le vermentino et le sauvignon.
J'aime les vins avec une bonne acidité et de la fraîcheur.
Je n'aime pas les vins passito ou les vins fortifiés.
```

Vous pouvez également renseigner les fichiers `data/known-preferred-beers.md` et
`data/known-preferred-wines.md` avec des produits spécifiques que vous avez déjà
goûtés et évalués. Cette partie est facultative mais utile
pour affiner le profil.

**Exemple — `data/known-preferred-beers.md`**
```
# BIÈRES AIMÉES
- Kwak
- Triple Karmeliet
- La Trappe Blond
- Flea Margherita

# BIÈRES NON AIMÉES
- Toute IPA
- Stout
- Bières avec une teneur en alcool supérieure à 9°
```

**Exemple — `data/known-preferred-wines.md`**
```
# VINS AIMÉS
- Vermentino Costamolino
- Syrah Soraia Casale Valle Chiesa
- Rebeca Firriato

# VINS NON AIMÉS
- Vins passito
- Vins fortifiés
```

### Mise à jour au fil du temps

Chaque fois que vous exprimez un jugement sur un produit (« Celui-ci me plaît »,
« Celui-ci ne me plaît pas »), l'agent met automatiquement à jour les
fichiers `data/`. Les règles gustatives dans les paragraphes de SKILL.md, en revanche,
ne sont mises à jour qu'avec votre confirmation explicite, car
elles sont contraignantes pour les évaluations futures.

---

## Exemples d'utilisation

### Scénario 1 — Rayon de vins (image)
Vous prenez une photo d'un rayon de cave à vin. L'agent identifie les vins,
les recherche tous sur le web, les compare à votre profil. Il vous dit
lequel choisir, pourquoi, et avec quoi l'accorder.

### Scénario 2 — Menu de bières (image)
Vous prenez une photo du menu de bières d'un pub. L'agent ignore les cocktails,
les spiritueux, etc... analyse uniquement les bières, recherche des informations sur
chacune. Il suggère la bière la plus adaptée à vos goûts.

### Scénario 3 — Liste textuelle mixte
Vous écrivez « J'ai ces vins : Chianti Classico, Vermentino Costamolino,
Amarone. Et ces bières : Kwak, IPA artisanale locale, Leffe Blonde. »
L'agent évalue les deux catégories et vous dit quel est le meilleur
choix globalement.

### Scénario 4 — Demande sans liste
« J'ai besoin d'un vin pour un dîner, que me recommandez-vous ? » L'agent
n'invente pas. Il demande ce que vous avez à disposition, quel type de dîner,
et si vous avez déjà des vins en tête.

### Scénario 5 — Nouvelle préférence exprimée
Après une suggestion, vous dites « J'ai vraiment aimé cette bière ».
L'agent l'ajoute à vos favoris et met à jour le profil
pour être encore plus précis la prochaine fois.

---

## Ce que cette skill ne fait PAS

- **Elle ne fournit pas d'évaluations de dégustation professionnelles.** Les
  suggestions sont basées sur des données objectives (style, teneur en alcool,
  amertume) et sur les préférences déclarées. Elle ne remplace pas un
  sommelier humain dans des contextes formels.

- **Elle ne gère pas d'autres boissons.** Spiritueux, cocktails, liqueurs,
  sodas, boissons non alcoolisées — tout ce qui n'est pas bière ou vin est
  ignoré.

---

## Suggestions (facultatif)

**drinks-sommelier** fonctionne avec n'importe quel outil de recherche web que votre agent
prend en charge nativement. Si votre agent a déjà des capacités de recherche web fiables,
vous n'avez besoin de rien d'autre.

Cependant, si vous souhaitez garantir des recherches approfondies et résistantes aux antibots
à chaque fois (particulièrement utile lorsque les pages produits sont derrière des systèmes antibot),
envisagez d'installer la skill complémentaire
**[browser-search](https://github.com/Johell1NS/browser-search)**.
Elle interroge des dizaines de moteurs simultanément et aide l'agent à trouver
des informations sur les produits même lorsque les outils standard peinent.

---

## Licence
MIT
