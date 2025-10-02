---
titre: LeetCode 2399. Vérifier les distances Entre les mêmes lettres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2399 – Distances de contrôle Entre les mêmes lettres
> **Le Bon, le Mauvais et l'Ugly – Un guide pratique pour les candidats prêts à l'entrevue* *

---

### TL;DR

- **Problème**: Chaque lettre minuscule apparaît **exactement deux fois** dans une chaîne `s`.
Pour chaque lettre `i` (`a' → 0`, ..., `'z' → 25`) le tableau `distance[i]` indique combien de **autres** lettres devraient se trouver entre ses deux occurrences.
Retour `true` si `s` satisfait à toutes les distances données.

- **Solution**:
1. **Track‐First** – Entreposez le premier index de chaque lettre, puis validez sur la seconde apparence.
2. **Deuxième** – Lorsque vous voyez une lettre, examinez immédiatement les étapes `distance + 1` et comparez; définissez l'entrée `-1` pour éviter une double vérification.

- **Complexité**:
- Heure: < < O > >
- Espace: `O(26)` (constante)

- **Pourquoi ça compte**:
Le modèle est courant dans les questions d'entrevue à cordes et à oreilles. La maîtrise montre que vous pouvez gérer la logique *two-pass*, l'utilisation des cartes et la sécurité des caisses.

---

Récapitulation des problèmes

Texte
Entrée
- Oui.
s – chaîne (longueur 2‐52, toutes minuscules)
distance – int[26] (0-basé pour 'a'...'z')

Produit
- Oui.
booléen – true iff s est une chaîne de caractères «well‐spaced»
«» "

*exemple*

«» "
s = "abaccbe"
distance = [1,3,0,5,...] // seulement a,b,c matière
Résultat: true
«» "

---

Deux approches gagnantes

L'approche d'Idea d'Idea d'Idea
- C'est quoi ?
**Track-First**=Rappelez-vous le premier index; sur le second index calculez `i - firstIndex - 1`.= Simple, clair.== Nécessite un drapeau =first‐seen=; utilise un tableau de 26 int. Autres
**Check-Deuxième** Lors de la première occurrence, regardez directement « i + distance + 1 ». Marquer comme traité (`-1`). Un seul passage; pas besoin de tableau d'affichage séparé. Un peu plus difficile à comprendre; utilise le tableau `distance` mutablement. Autres

Vous trouverez ci-dessous des implémentations **Java, Python et C++** pour les deux méthodes pour choisir celle qui correspond à votre style.

---

# # # # # # Code Snippets

> **Astuce:** Toutes les solutions supposent que les contraintes garantissent que chaque lettre apparaît *exactement deux fois*, de sorte qu'aucune validation supplémentaire n'est requise au-delà des contrôles liés.

#### 3.1 Java

"Java
// ----------------------------------------------
// Java – Track‐First (basé sur HashMap)
// ----------------------------------------------
solution de classe publique {
contrôle public du booléen Distances(String s, int[] distance) {
Carte<Caractère, entier> premierPos = nouveau HashMap<>();
pour (int i = 0; i < s.longueur(); i++) {
char ch = s.charAt(i);
si (firstPos.contientKey(ch)) {
int diff = i - firstPos.get(ch) - 1;
si (diff != distance[ch - 'a']) retourner faux;
} autre {
premierPos.put(ch, i);
}
}
retour vrai;
}
}

// ----------------------------------------------
// Java – Vérification-deuxième (en place)
// ----------------------------------------------
solution de classe publique {
contrôle public du booléen Distances(String s, int[] distance) {
pour (int i = 0; i < s.longueur(); i++) {
int d = distance[s.charAt(i) - 'a'];
// si la deuxième occurrence ou hors limites → échoue
si (i + d + 1 >= s.longueur()== s.charAt(i + d + 1) != s.charAt(i))
retourner faux;
distance[s.charAt(i) - 'a'] = -1; // marque traitée
}
retour vrai;
}
}
«» "

3.2 Python

'`python
♪ ----------------------------------------------
# Python – Première piste
♪ ----------------------------------------------
Contrôle Distance(s): str, distance: list[int] -> C'est vrai.
premier = {}
pour i, ch dans le(s) énuméré(s):
si ch en premier:
i - premier[ch] - 1 != distance[ord(ch) - 97]:
Retour Faux
Sinon:
premier[ch] = i
retour Vrai

♪ ----------------------------------------------
# Python – Deuxième chèque
♪ ----------------------------------------------
Contrôle Distance(s): str, distance: list[int] -> C'est vrai.
pour i, ch dans le(s) énuméré(s):
d = distance[ord(ch) - 97]
si i + d + 1 >= len(s) ou s[i + d + 1] != Ch:
Retour Faux
distance[ord(ch) - 97] = -1 # marque traitée
retour Vrai
«» "

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// ----------------------------------------------
// C++ – Piste‐Première
// ----------------------------------------------
Contrôle des bools Distances(chaîne s, vecteur<int> et distance) {
vecteur <int> premier(26, -1);
pour (int i = 0; i < (int)s.zize(); ++i) {
int idx = s[i] - 'a';
si (premier [idx] != -1) {
si (i - premier[idx] - 1 != distance[idx]) retourner faux;
} autre {
premier[idx] = i;
}
}
retour vrai;
}

// ----------------------------------------------
// C++ – Deuxième contrôle
// ----------------------------------------------
Contrôle des bools Distances(chaîne s, vecteur<int> et distance) {
pour (int i = 0; i < (int)s.zize(); ++i) {
int d = distance [s[i] - 'a'];
si (i + d + 1 >= (int)s.size()="s[i + d + 1] != s[i]) retournent faux;
distance[s[i] - 'a'] = -1; // traité
}
retour vrai;
}
«» "

> **Choisissez le style qui vous semble le plus naturel. **
> *Track‐First* est idéal pour les entrevues qui valent **suivi explicite de l'état**.
> *Check‐Second* démontre **une logique optimisée à un passage** et une compréhension plus approfondie des indices de tableau.

---

Analyse de complexité

Opération de la piste – Première comptabilisation Vérification – Deuxième comptabilisation
- C'est quoi ?
Temps `O(n)` – un scan, recherche de cartes à temps constant
Espace "O(26)" (carte des premiers indices) – réutilise le tableau d'entrée

Tous deux répondent aux contraintes de LeetCode confortablement (max `n = 52`).

---

## 5-- Pièges communs

Pourquoi il échoue
- C'est quoi ?
**Utiliser `i - firstIndex` au lieu de `i - firstIndex - 1`**. Soustraire 1 pour exclure les paramètres. Autres
**Vérifier les limites de manière incorrecte (`i + d < n` au lieu de `i + d + 1 < n`)**. Rappelez-vous le `+1` pour la lettre elle-même. Autres
**En supposant que toutes les 26 lettres apparaissent**. Utilisez une carte ou marquez les entrées traitées; ignorez les distances lorsque la lettre n'est jamais vue. Autres
**Mutting `distance` dans Check‐ Deuxièmement, sans copie**.Les effets secondaires peuvent s'infiltrer dans le code d'appel ou les tests. Copier le tableau d'abord (`int[] copy = distance.clone()`) ou documenter explicitement que la méthode la mute. Autres

---

C'est pas vrai. Vérification des essais

Texte
Essai 1
- Oui.
s = "abaccbe"
distance = [1,3,0,5,0,...]
Résultat: true

Essai 2
- Oui.
s = "aa"
distance = [1,0,0,...]
Résultat : faux

Essai 3 (bord)
- Oui.
s = "zzxyyzxxzz" // 10 lettres, chacune deux fois
distance = [0]*26; distance[25] = 8; distance[23] = 2; distance[24] = 1
Résultat: true
«» "

L'exécution des deux implémentations sur la même suite de test vous garantit d'attraper des bugs subtils.

---

# # 7-Optimized Blog Wrap- En haut

**Titre**
> *Vérifier les distances entre les mêmes lettres – Java, Python, C++ Solutions et conseils d'entrevue*

**Méta—Description**
> Master LeetCode 2399 avec des implémentations Java, Python et C++ claires. Apprenez la piste‐First vs Check‐ Deuxième approche, complexité et pièges communs. Boostez votre jeu d'entretien de codage aujourd'hui!

** Mots-clés en tête**
- LeetCode 2399
- Vérifier les distances Entre les mêmes lettres
- Algorithmes à cordes
- Correspondance à deux chaînes de passe
- Préparation de l'entrevue

**Closer l'appel à l'action**
> Si vous préparez votre prochaine interview d'ingénierie logicielle, pratiquez ce problème jusqu'à ce que la solution se sente seconde nature. Les concepts — cartes deash, contrôles à deux points et sécurité hors pair — sont réutilisables à travers d'innombrables défis de codage. (en milliers de dollars)

---

La pensée finale

*Le bon* – Un algorithme simple et efficace dans le temps qui transforme une règle potentiellement déroutante de distance en un passage linéaire propre.
*Le mauvais* – La tentation de coder des indices ou d'ignorer la règle « lettre absente » peut faire trébucher des codeurs même expérimentés.
*Les erreurs de laid* – Off‐by‐one qui brisent subtilement les solutions ; évitez-les en double-vérifiant les limites et en utilisant le tour `-1'.

Maintenant que vous possédez les trois implémentations de langage et comprenez le *pourquoi* derrière chaque ligne, vous êtes prêt à frapper LeetCode 2399, impressionner interviewers, et atterrir cette offre d'emploi. C'est ce qu'il a dit.

Bon codage !

---

*— Votre mentor de codage sympathique*
<https://www.codemaster.io>
---

**Bonne résolution, et que votre code d'entrevue soit toujours off-by-zero correct! * *