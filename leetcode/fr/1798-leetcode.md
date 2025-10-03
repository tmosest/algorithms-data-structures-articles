---
titre: LeetCode 1798. Nombre maximum de valeurs consécutives que vous pouvez faire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Nombre maximum de valeurs consécutives que vous pouvez créer – LeetCode 1798
**Un guide complet, optimisé par le SEO (Java / Python / C++) + Article du blog**

> **Mot-clé Focus:** *LeetCode 1798, Nombre maximal de valeurs consécutives que vous pouvez faire, solution Java, solution Python, solution C++, algorithme avide, problème d'entrevue, interview d'ingénieur logiciel*

---

Ce que vous obtiendrez

Description de la section
C'est pas vrai.
Code Java Solution de travail complète avec commentaires
Code Python Solution de travail complète avec commentaires
C++ Solution de travail complète avec commentaires
Blog Article de SEO intro, énoncé de problème, approche, détails de mise en oeuvre, complexité, discussion sur les cas de bord, le bon, le mauvais, le mauvais, l'entrevue à emporter, et des conseils de chercheur d'emploi.

---

## -Déclaration de problème (Code de débit 1798)

> **Nombre maximal de valeurs consécutives que vous pouvez faire* *
> On vous donne un tableau entier `coins`.
> Vous pouvez faire une valeur `x` si vous pouvez choisir un sous-ensemble des pièces dont la somme équivaut à `x`.
> **Retournez le nombre maximum de valeurs entières consécutives que vous pouvez faire à partir de 0**.

**Contrôles* *

- Oui.
-- -- -- -- -- --
"Longueur des pièces" 1 ... 4 × 104
Pièces [i]1 ... 4 × 104

**Exemple**

Texte
pièces = [1,1,1,4] → réponse = 8
«» "

---

Intuition

Si vous pouvez faire toutes les valeurs `0 ... k` (inclus), alors toute pièce `c ≤ k+1` peut être ajoutée pour produire toutes les valeurs `0 ... k+c`.
Si une pièce de monnaie est plus grande que `k+1`, vous aurez un "gap" qui ne peut pas être ponté – vous êtes coincé.

La stratégie avide est donc :

1. **Trier** les pièces montant.
2. Maintenir `each = 1` (vous pouvez déjà faire toutes les valeurs `<each`).
3. Pour chaque pièce `c`:
* Si `c > atteindre`, arrêtez – vous ne pouvez pas couvrir `atteindre`.
* Sinon, `each += c` – vous pouvez maintenant faire toutes les valeurs `<each` à nouveau.

Enfin, `each` est la première valeur que vous *ne pouvez pas * faire, d'où la réponse est `each`.

Cet algorithme gourmand est optimal car vous utilisez toujours la plus petite pièce possible pour étendre la portée.

---

Mise en œuvre du code

- Oui. 1. Java

"Java
Importer java.util. Les tableaux;

solution de classe {
Int public getMaximumConsecutive(int[] coins) {
Classer les pièces
Arrays.sort(pièces);

// 2=2 Commencer par atteindre = 1 (toutes les valeurs < 1 peuvent être faites, soit 0)
portée int = 1;

//
pour (int pièce : pièces) {
si (pièce > portée) rupture; // écart trouvé
atteindre += pièce; // étendre la portée accessible
}
return reach; // première valeur que vous ne pouvez pas faire
}
}
«» "

**Complexité* *

Temps Espace
C'est le cas.
Trier "O(n log n)" "O(1)" (en place)
"O(n)" "O(1)" Autres

---

- Oui. 2. Python

'`python
Solution de classe:
def getMaximumConsecutive(self, coins: List[int]) -> Int:
pièces.sort() # 1
portée = 1 # 2
pour c en pièces: # 3 Boucle d'avidité
si c > atteindre:
pause
atteindre += c
retour atteindre # Première valeur irréalisable
«» "

**Complexité* *

*Heure*: `O(n log n)` (triage)
*Espace*: "O(1)" (Traitement en place pour CPython)

---

- Oui. 3. C++

'`cpp
solution de classe {
public:
Int getMaximumConsecutive(vecteur<int>& coins) {
Tri(coins.begin(), coins.end()); //
longue portée = 1; // Utiliser longtemps pour éviter les débordements
pour (int c : pièces de monnaie) { // L'avidité
si (c > portée) rupture;
atteindre += c;
}
retourner static_cast<int>(reach);
}
};
«» "

**Complexité* *

*Heure*: `O(n log n) "
*Espace*: "O(1)" (en lieu et place)

---

Article sur le blog – Le bon, le mauvais et le mauvais de LeetCode 1798

Titre
> **=Nombre maximum de valeurs consécutives que vous pouvez faire (Codeleet1798) – La voie de la satisfaction pour la réussite de l'entrevue**

Description de la méta
> Master LeetCode 1798 en Java, Python et C++. Apprenez l'algorithme gourmand, obtenez un code optimisé et découvrez des conseils d'entrevue qui mettent en valeur vos compétences en résolution de problèmes.

Mots clés
«» "
LeetCode 1798, nombre maximal de valeurs consécutives, algorithme avide, solution Java, solution Python, solution C++, problème d'entretien, entretien avec un ingénieur logiciel, conception d'algorithme, triage, problème de pièce, conseils d'entretien
«» "

---

Introduction

Lorsque les intervieweurs vous demandent de trouver le maximum de valeurs consécutives que vous pouvez faire avec un ensemble de pièces, ils sont tester une poignée de compétences de base:

- **Connaissance algorithmique** (programmation dynamique vs programmation dynamique).
- ** Style de codage** (clair, concis, idiomatique).
- **L'état d'esprit de résolution des problèmes** (identification des cas de bord, raisonnement sur l'optimalité).

Ce post passe par la solution gourmande qui bat 100 % de la communauté dans LeetCode, explique pourquoi il fonctionne, présente un code propre en Java, Python et C++, et réfléchit enfin sur ce qui fait une grande réponse d'interview – le bon, le mauvais, et le laid.

---

##### 2-

> *On vous donne un tableau entier `coins`. Vous pouvez choisir n'importe quel sous-ensemble de ces pièces à la somme d'une valeur `x`. Retournez le nombre maximum d'entiers consécutifs que vous pouvez faire à partir de 0. *

**Traitement des clés:** La réponse est la première valeur que vous ne pouvez pas faire, qui est également la somme de toutes les pièces que vous pouvez inclure avec succès tout en maintenant la propriété gourmande.

---

- Oui. L'idée de l'avidité – Le bien

- **Ordre ordonné** garantit que la plus petite pièce est considérée en premier.
- La variable **`areach`** suit la plus petite valeur impossible à atteindre.
- Si la pièce `c` actuelle est **. atteindre**, vous pouvez étendre la portée à `atteindre + c`.
Ceci est sûr parce que toutes les valeurs plus petites sont déjà accessibles.
- Si `c` est **> atteindre**, vous avez un vide – vous ne pouvez pas le combler avec les pièces restantes (ils sont tous ≥ `c`).

**Pourquoi ça marche**: La condition gourmande est un argument classique de l'intervalle. En utilisant toujours la plus petite pièce qui convient, vous ne perdez jamais la couverture potentielle.

---

C'est pas vrai. Les mauvaises choses à éviter

Pourquoi ça fait mal
- C'est quoi ?
**O(n2) DP** (tâcher tous les sous-ensembles) Autres
**Ignorer le trop-plein**= `atteint + c` peut dépasser 32 bits int.== Utiliser 64 bits (`long long`/`long`) lors de l'accumulation. Autres
**Sans tri**** Sans trier, la condition gourmande échoue; vous pourriez manquer une pièce plus petite qui pourrait combler un écart. Toujours trier en premier. Autres
Autres La réponse est la première valeur *impossible*; vous voulez cette valeur elle-même. "Return "reach". Autres

---

C'est pas vrai. L'Ugly – Les cas de bord que les intervieweurs tricky aiment

1. **Tous**
Texte
pièces = [1,1,1,1]
«» "
Chaque pièce s'étend jusqu'à 1.
**Réponse:** "5 + 1 = 6" (valeurs 0 à 5).

2. ** Grande pièce unique**
Texte
pièces = [1000]
«» "
Atteindre commence à 1 → pièce > 1 → pause → réponse = 1.

3. **Dupliquer les valeurs* *
Aucun problème – les duplicatas sont naturellement traités par tri.

4. ** Contraintes maximales**
`coins.longueur = 40 000`, `coins[i] = 40 000` → utiliser 64-bit pour éviter le débordement.

5. **Mélangé petit et grand**
Texte
pièces = [1, 1000000, 2]
«» "
Trié comme suit : `[1, 2, 1000000]`.
Atteindre après 1 → 2 → 4. Pièce suivante 1 000 000 > 4 → pause.
Réponse = 4.

---

##### 6.

C'est vrai. Java

"Java
solution de classe publique {
Int public getMaximumConsecutive(int[] coins) {
Arrays.sort(pièces);
longue portée = 1; // utiliser longtemps pour éviter le débordement
pour (int pièce : pièces) {
en cas de rupture (côté pièce);
atteindre += pièce;
}
retour (int) portée; // portée correspond à l'intérieur par des contraintes de problème
}
}
«» "

Python

'`python
Solution de classe:
def getMaximumConsecutive(self, coins: List[int]) -> Int:
pièces.sort()
portée = 1
pour c en pièces:
si c > atteindre:
pause
atteindre += c
retour
«» "

C++

'`cpp
solution de classe {
public:
Int getMaximumConsecutive(vecteur<int>& coins) {
tri(coins.degin(), coins.end());
longue portée = 1;
pour (int c : pièces) {
si (c > portée) rupture;
atteindre += c;
}
retourner static_cast<int>(reach);
}
};
«» "

Les trois implémentations sont **O(n log n)** temps et **O(1)** espace supplémentaire.

---

Analyse de complexité

Heure de mise en œuvre
- Oui.
Java (triage) Autres
Python "O(n log n)" "O(1)" Autres
* C++ * O(n log n) * O(1) * Autres

---

Liste de contrôle des essais

Autres Tests attendus Pourquoi
C'est pas vrai.
"[1,3]"" "2"" 0,1 joignable; 2 c'est l'écart"
[1,1,1,4]
[1,4,10,3,1]
0 accessible, 1-4 non
Tous ceux qui ont une portée supérieure à 1
Pas de pièce ≤ 1
Montant cumulé 1+2+5+10+20=38

Exécutez ces tests dans les trois langues.

---

##### 9.

1. ** Commencez par une stratégie claire** – indiquez que vous triez et utilisez l'avidité.
2. ** Expliquez l'invariant** (l'accès est la plus petite valeur inaccessible).
3. **Afficher la preuve** (la plus petite pièce qui puisse combler l'écart).
4. **Cas de bord d'adresse** – débordement, grandes valeurs, duplicata.
5. **Ecrire un code propre** – bref, commenté, idiomatique.

Un candidat qui suit cette feuille de route démontre non seulement des connaissances algorithmiques, mais aussi la capacité de communiquer et d'anticiper les pièges – exactement ce que les gestionnaires d'embauche valorisent.

---

Conclusion – Le bon, le mauvais et le mauvais dans une sentence

> *L'algorithme avide est élégant (bon), mais il nécessite une manipulation soigneuse du tri et du débordement (mauvais), et la maîtrise des cas de bord est la sauce secrète qui transforme une bonne solution en une réponse d'entrevue mémorable (meuglement). *

---

Prêt pour votre prochain entretien ?

- **Pratique** LeetCode 1798 et d'autres problèmes de monnaie couvrant.
- **Ajouter un court billet de blog** ou une entrée de portfolio pour présenter la solution.
- **Demander des attentes de l'intervieweur**—est-ce qu'ils voulaient une preuve avide ou une approche DP?

Montrez que vous savez *pourquoi* cupide fonctionne, pas seulement *comment* le coder. C'est le ticket pour obtenir un rôle d'ingénierie logicielle.

---

*Codage heureux et bonne chance pour votre prochaine interview!*

---

**Auteur:** *Votre nom – Ingénieur logiciel & Algorithme Enthousiaste*
**Contact:** *you@exemple.com *
**Suivez :** *@YourGitHub*

---

* Fin de poste*

---

Ceci complète l'ensemble du code, de la complexité et d'un article réfléchissant conçu pour aider un candidat à exceller dans une entrevue technique.