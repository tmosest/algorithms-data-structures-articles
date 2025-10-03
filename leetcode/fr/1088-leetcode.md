---
titre: LeetCode 1088. Numéro de confusion II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1088 – **Confuser numéro II**
**Difficulté**: dur
**Tag**: DFS, rétrotraçage, manipulation bit

Un nombre déroutant est un nombre qui, lorsqu'il tourne à 180°, devient un nombre différent. Nous devons compter tous ces nombres dans "[1, n]".

> *Input*: `n = 20`
> * Sortie*: `6` – `[6, 9, 10, 16, 18, 19]`

> **Constraints**
> 1 ≤ n ≤ 109

Vous trouverez ci-dessous :

1. **Trois implémentations prêtes à la production** – Java, Python, C++
2. Un billet de blog **SEO-friendly** qui explique le --Good, le Bad, et le Ugly de la solution.
3. Un guide rapide pour chaque langue.

> **TL;DR** – L'astuce est de générer seulement des nombres valides (en utilisant les chiffres 0, 1, 6, 8, 9), les compter si le nombre retourné est différent, et prune quand le candidat dépasse *n*. Complexité : O(#geneated_numbers) 106 pour l'entrée la plus défavorable.

---

- Oui. 1. Java – Retraçage avec nombres

"Java
// LeetCode 1088 – Numéro de confusion II
// Auteur : [Votre nom] – 2025-09-22

Importation de java.util.*;

solution de classe publique {

// chiffres pouvant apparaître dans un nombre déroutant
finale statique privée DIGITS = {0, 1, 6, 8, 9};

public int confusionNombreII(int n) {
// commencer la récursion à partir des premiers chiffres non zéro (1, 6, 8, 9)
nombre int = 0;
pour (int d : nouvelle int[]{1, 6, 8, 9}) {
nombre += dfs(n, d);
}
le nombre de retours;
}

Int privé dfs(int n, long cur) {
si (cur > n) retourne 0; // prune
long flipped = flip(cur); // 0,1,6,8,9
int cnt = (flipped != cur) ? 1 : 0; // compte seulement si elle change

// essayer d'ajouter chaque chiffre possible à la fin la moins significative
pour (int d : DIGITS) {
long suivant = cur * 10 + d;
cnt += dfs(n, suivant);
}
retour cnt;
}

// tourner un nombre 180°
flip privé long (long num) {
long res = 0;
pendant la période 0) {
digit int = (int) (num % 10);
num /= 10;
res = res * 10 + flipped Chiffre(numérique);
}
retour rés;
}

int privé flippedDigit(inint digit) {
interrupteur (numéro) {
cas 6 : retour 9;
Cas 9: retour 6;
par défaut : chiffre de retour ; // 0,8 reste le même
}
}
}
«» "

> **Pourquoi c'est bon* *
> * Séparation claire de la logique (DFS + basculement).
> * Utilise `long` pour rester dans les limites (`10^9` convient facilement).
> * Pas de chaînes → utilisation de mémoire constante par récursion.

---

- Oui. 2. Python – DFS récursif

'`python
Code Leet 1088 – Confuser Numéro II
# Auteur : [Votre nom] – 2025-09-22
# Python 3

DIGITS = (0, 1, 6, 8, 9)
FLIP = {0: 0, 1: 1, 6: 9, 8: 8, 9: 6}

NombreII(n: int) -> Int:
"""Compte rendu des nombres confus dans [1, n]."""
def dfs(cur: int) -> Int:
si cur > n:
retour 0
flipped = int(str(cur)[:-1].translate(str.maketrans('069', '906')))
# mais nous évitons la chaîne: voir ci-dessous
cnt = 1 si flippé != Autre

pour d en DIGITS:
cnt += dfs(cur * 10 + d)
retour cnt

# aide à basculer sans conversion de chaîne
def flip(num: int) -> Int:
Res = 0
alors que num:
Res = res * 10 + FLIP[num % 10]
NUM //= 10
retour res

def dfs2(cur: int) -> Int:
si cur > n:
retour 0
flipped = flip(cur)
cnt = 1 si flippé != Autre
pour d en DIGITS:
cnt += dfs2(cur * 10 + d)
retour cnt

(dfs2(d) pour d en (1, 6, 8, 9))
«» "

> **Python en bref* *
> * Utilise `int` (précision arbitraire) - pas de soucis de débordement.
> * 'FLIP ' dict garde le code rangé.
> * Profondeur de récursion ~ 10, très bien pour Python.

---

- Oui. 3. C++ – DFS itératif avec pile

'`cpp
// LeetCode 1088 – Numéro de confusion II
// Auteur : [Votre nom] – 2025-09-22
// g++ -std=c++17 solution.cpp

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int confusionNombreII(int n) {
= {0, 1, 6, 8, 9};
long résultat = 0;
empiler <long> m;
// commencer par les premiers chiffres non zéro
à l'aide d'un dispositif de retenue pour enfants
un push à st(6);
un push st(8);
s.push(9);

pendant que (!st.vide()) {
longue courbure = m. haut(); st.pop();
si (cur > n) continue;
long et long = flip(cur);
si (flippé != cur) + + résultat;

pour (int d : chiffres) {
long long nxt = cur * 10 + d;
si (nxt <= n) st.push(nxt);
}
}
le résultat du retour;
}

particulier:
// tourner à 180°
long long flip(long long num) const {
longue rés = 0;
pendant que (num) {
nombre int = nombre % 10;
num /= 10;
si (chiffre) 6) chiffre = 9;
Sinon si (chiffre) 9) chiffre = 6;
res = rés * 10 + chiffre;
}
retour rés;
}
};
«» "

> **Pourquoi C++ est puissant* *
> * Exécution rapide – O(1 ms) pour le pire cas.
> * Utilise une pile pour éviter les limites de profondeur de récursion.
> * Contrôle de type explicite (garanties longues 64 bits).

---

- Oui. 4. Billet de blog – Le bon, le mauvais et le mauvais

Titre
* Confuser les chiffres, confuser la chasse à l'emploi : Master LeetCode 1088 & Land votre prochain rôle technique**

Description de la méta
Découvrez comment résoudre LeetCode 1088 – Confusing Number II en Java, Python et C++. Comprendre l'algorithme, discuter des pièges, et utiliser cette solution pour booster votre CV et SEO.

---

Introduction
*Si vous lisez ceci, vous vous préparez probablement pour une interview technique ou essayez de casser la prochaine ronde d'un bootcamp de codage. LeetCode="s "Confusing Number II=" (1088) est un problème classique *Hard* qui teste DFS, backtracking, et taille intelligente. Ci-dessous se trouve une marche en profondeur de l'approche **bonne**, les erreurs **mauvais** à éviter, et les cas de bord **ugly** qui peuvent voyager même les codeurs assaisonnés. *

---

- Oui. 1. Le Bon – Une stratégie de recul propre

Concept Pourquoi ça marche Détail de la mise en œuvre
- C'est quoi ?
Autres **L'ensemble Digit**. Seulement 0, 1, 6, 8, 9 peut apparaître dans un nombre confus. "DIGITS = {0,1,6,8,9}" Autres
**Génération récursive**=Construisez tous les nombres ≤ *n* en ajoutant un chiffre valide. DFS: `next = cur * 10 + d`
Autres **Prune tôt**=Arrêtez quand `cur > n`.= `si (cur > n) retourne;`=
**Flip & Compare**=Contrôle seulement si le nombre retourné diffère.= `if (flip(cur) != cur) count++;`=
**Space-Efficace** Exclure `long`/`long long` – aucune chaîne. "longe courbure;" Autres

*Résultat:* Linéaire dans le nombre de candidats valides (~106 pour le pire cas), mémoire permanente au-dessus.

---

- Oui. 2. Les mauvaises – Pièges communs

1. ** Manipulation de la chaîne* *
- La conversion des nombres en chaînes et retour est plus lente et exigeante en mémoire.
- Dans Python, `int(str(num)[:-1)' Il faut toujours une table de cartographie.

2. ** Utilisation de la profondeur de récursion trop profonde**
- La limite de récursion du Python (~1k) est plus qu'assez (profondeur max. 10).
- La récursion C++ peut frapper le débordement de la pile sur des arbres très profonds ; préférer une pile explicite.

3. **Négligence des zéros principaux**
- Après la rotation, les zéros de tête doivent être ignorés (`8000` → `0008` → `8`).
- Notre fonction `flip()` les rejette naturellement en construisant le chiffre le moins significatif.

4. **Numéros non-confuseurs**
- Les nombres comme `1`, `8`, `88` restent les mêmes après la rotation – ils ne doivent pas **** être comptés.
- La vérification `flip(cur)= cur` garantit la justesse.

---

- Oui. 3. Les cas de bord et les quirques de performance

Pourquoi c'est bizarre Réparer
- C'est quoi ?
**n = 109**La récursion explore un million de candidats ; le flipping naïf devient un goulot d'étranglement. Autres Utilisez l'arithmétique entier (`% 10`, `/ 10`) au lieu de la chaîne ops. Autres
**Huge Leading Zero Sequences** Commencer la récursion avec des chiffres ** non-zéro** seulement (1, 6, 8, 9). Autres
Autres **Limite de temps dépassée sur Java**.Les Javas autoboxing ou utilisant `Long` au lieu de `long` peuvent ajouter des frais généraux. Stick aux types primitifs (`long`). Autres
**Excédent en C++**= Utiliser `int` pour `cur * 10 + d` les débordements lorsque `cur` ~ 2 × 108.= Utiliser `long long` (64-bit). Autres

---

- Oui. 4. Comment montrer ceci sur votre CV / Portfolio

1. ** Dépôt de gitHub**
- Commettez les trois implémentations linguistiques.
- Inclure un `README.md` avec l'énoncé du problème, une brève explication et des exemples d'utilisation.

2. **Blog Post / Article moyen* *
- Poster l'article complet (ci-dessus) sur Medium, Dev.to, ou votre site personnel.
- Ajouter des captures d'écran des résultats de soumission de LeetCode.
- Étiquette avec **#LeetCode**, **#Algorithmes**, **#Backtracking**, **#Java**, **#Python**, **#C++**.

3. **Profil du code de débit* *
- Mettez en avant votre temps de run le plus rapide parmi les trois langues.
- Ajouter un commentaire: *=Mise en œuvre d'une solution DFS optimale pour LeetCode 1088. Score X en Y

4. **Préparation de l'entrevue**
- Apportez l'article comme référence lors de la discussion des stratégies algorithmiques.
- Soyez prêt à expliquer pourquoi vous avez choisi DFS sur BFS, pourquoi vous avez évité les chaînes et comment vous avez géré les zéros de tête.

---

- Oui. 5. SEO Boost – Ce que les recruteurs recherchent

SEO Tactique
C'est quoi ?
**Titre et Meta**=Les recruteurs cherchent des solutions de confusing Number II=. Autres
**Structured Content**= Google aime les tables et les blocs de code. Autres
**URLs canoniques**= Éviter le contenu en double si vous postez sur plusieurs plateformes. Autres
**Liens externes** Autres

---

Conclusion
*LeetCode 1088 peut sembler comme un puzzle de théorie des nombres bizarre, mais le motif sous-jacent est un exemple de manuel de **bounded backtracking**. En maîtrisant la solution à travers Java, Python et C++, vous démontrerez la polyvalence, la sensibilisation aux performances et la capacité d'écrire un code propre et prêt à la production. Partagez-le, expliquez-le, et laissez-le commencer la conversation dans votre prochaine interview. *

---

### Appel à l'action
*Prêt à s'attaquer à d'autres problèmes *Hard*? Abonnez-vous aux défis hebdomadaires de résolution de problèmes, ou consultez notre guide complet de préparation d'entrevues sur la maîtrise du SSD et la rétro-suivi. *

---

FAQ (facultative)

Question Réponse
C'est pas vrai.
*Puis-je utiliser le BFS itératif à la place?*= Oui, mais le DFS est plus naturel pour cet arbre combinatoire. Autres
*Dois-je gérer les contraintes de LeetCode négatives `n ≥ 1`. Autres
*La mémorisation est-elle utile? Pas ici – chaque numéro est unique; aucun sous-problème ne se chevauche. Autres

---

- Oui. 5. Conclusion

*Solving LeetCode 1088 n'est pas seulement à propos d'obtenir un verdict "Accepté" ; il s'agit d'écrire un code qui interviewe l'amour, de construire un portefeuille que les recruteurs scanner, et de démontrer la pensée algorithmique qui balance. Utilisez la bonne stratégie, évitez les mauvais pièges, et n'ignorez jamais les cas de bord laid. Avec les implémentations ci-dessus, vous êtes désormais équipé pour aser ce problème en Java, Python et C++ – et pour mettre en valeur votre expertise auprès des gestionnaires et des moteurs de recherche. *

---

- Oui. 6. Pensée de clôture

> Les algorithmes sont comme des puzzles ; chacun résolu aiguise votre esprit et votre CV. Les maîtriser est la première étape d'une carrière stellaire en génie logiciel. – *— Votre futur gestionnaire d'embauche*.

---

- Oui. 7. Mots clés pour référencement
`#LeetCode1088`, `#ConfuserNumberII`, `#Backtracking`, `#AlgorithmDesign`, `#Java`, `#Python`, `#C++`, `#TechnicalInterview`, `#JobSearch`, `#CodingInterview`.

---

### Fin du blog

---

- Oui. 5. Remarques finales

*Les solutions ci-dessus et l'article vous fournissent tout ce dont vous avez besoin pour:
1. Écrire le code prêt à la production.
2. Discutez de votre solution avec confiance lors des entrevues.
3. Publier un billet de blog haute visibilité qui met en valeur vos compétences analytiques. *

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

Liste de contrôle du référencement

État
- C'est quoi ?
Titre & Meta Tags
H1/H2 Rubriques
Autres Blocs de code avec tags de langue
Liens externes vers LeetCode
Autres Texte Alt pour les captures d'écran (le cas échéant)
Ensemble d'URL canonique

---

**Remplissez-le dans votre portefeuille, et vous ne maîtrisez pas seulement un problème de LeetCode difficile, mais faites aussi un cas fort à tout gestionnaire d'embauche que vous pouvez livrer un code propre, efficace et bien documenté. **