# drinks-sommelier — Initial Setup Guide

This guide is used by the agent **only** when the skill is loaded for the first time and the taste paragraphs have not yet been filled in. After the first setup, this file is no longer needed.

---

## What the agent must do

1. Briefly explain to the user that the skill needs to know their tastes in order to work
2. Ask targeted questions to fill in the taste paragraphs, proceeding from general to specific
3. After collecting the preferences, **modify ONLY the paragraphs** "User's tastes for beers" and "User's tastes for wines" in the `SKILL.md` file, replacing the text "Enter your preferences here" with what has been learned. Do not alter any other section of the file.
4. **Before modifying**, carefully re-read `SKILL.md` to precisely identify the lines to replace
5. (Optional) Populate the `data/` files with the specific products the user mentions
6. Verify that you have understood correctly before proceeding

---

## Examples for filling in the taste paragraphs

### Example — "User's tastes for beers" paragraph (filled in)

```
I prefer sweet and not bitter beers.
They must not exceed 9° alcohol by volume.
I like Belgian styles (blond, tripel, witbier), fruity beers, and sours.
I dislike IPAs, stouts, and beers that are too hoppy or bitter.
I prefer medium-light bodies and medium carbonation.
```

### Example — "User's tastes for wines" paragraph (filled in)

```
I prefer red wines that are not too sweet, full-bodied but balanced.
For whites, I prefer vermentino, sauvignon, and fiano.
I like wines with good acidity and freshness.
I dislike wines that are too sweet, passito, or fortified.
I prefer Italian wines, particularly from the center-south.
```

---

## Examples for filling in the data/ files

### Example — `data/known-preferred-beers.md`

```markdown
# LIKED BEERS
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

# DISLIKED BEERS
- Any IPA
- Stout
- Beers with alcohol content above 9°
```

### Example — `data/known-preferred-wines.md`

```markdown
# LIKED WINES
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

# DISLIKED WINES
- Passito wines
- Fortified wines
- Wines that are too sweet in general
```

---

## Guiding questions for the agent

If the user does not know where to start, the agent can ask these questions in order:

**For beers:**
1. "Do you prefer sweet or bitter beers?"
2. "What is the maximum alcohol content you prefer?"
3. "Are there beer styles you particularly like? (e.g. blond, red, fruity, spiced)"
4. "Are there styles you cannot stand? (e.g. IPA, stout, bitter)"
5. "Do you have any specific beer you already know you like?"

**For wines:**
1. "Do you prefer red, white, or both?"
2. "For reds, do you prefer them drier or softer?"
3. "Do you have preferred grape varieties? (e.g. vermentino, syrah, fiano)"
4. "Do you have geographic preferences? (e.g. Italian, French wines, from a specific region)"
5. "Do you have any specific wine you already know you like?"

---

## Final check

Before considering the setup complete, make sure that:
- [ ] The "User's tastes for beers" paragraph in `SKILL.md` contains at least 2-3 pieces of information (e.g. sweet/bitter, alcohol content)
- [ ] The "User's tastes for wines" paragraph in `SKILL.md` contains at least 2-3 pieces of information (e.g. red/white, dry/sweet)
- [ ] (Optional) The `data/` files contain at least the products eventually mentioned by the user
- [ ] The user has confirmed that the profile is correct

If even a single guideline is present, the skill can start working. The details will be refined with use.
