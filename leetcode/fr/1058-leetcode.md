---
titre: LeetCode 1058. Réduire au minimum l'erreur d'arrondi pour atteindre la cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Erreur d'arrondi minimum – LeetCode 1058
**Solve en Java, Python et C++**
**+ Billet de blog (friendly SEO, le bon, le mauvais et le laid)* *

---

Récapitulation des problèmes

Problème Difficulté Lien
- C'est quoi ?
1058 **Minimiser l'erreur d'arrondi pour atteindre la cible**=Moyenne<https://leetcode.com/problèmes/minimiser-arrondi-error-to-meet-cible/> Autres

*Avec un tableau `prix[]` (chaque chaîne a exactement 3 chiffres décimaux) et un entier `cible`. Pour chaque prix `pi` vous pouvez le remplacer par `floor(pi)` ou `ceil(pi)`. Choisissez les remplacements pour que la somme soit égale à "cible". Si c'est impossible, retournez-le. Sinon, retournez l'erreur d'arrondi **minimum** :

\[
\text{error}=\sum_{i=1}^{n}\lvert \text{rounded}_i - p_i\rvert
\]

La réponse doit être formatée avec exactement trois décimales. *

---

C'est vrai. Pourquoi l'erreur grave est un problème **Hidden DP + Greedy**

* Vous n'avez qu'à décider **Qui** des deux valeurs entières (`floor` ou `ceil`) vous utiliserez pour chaque prix.
* Le changement de la somme causé par une décision de plancher/ceil est **Identique** pour tous les prix:
* `ceil(pi)` → ajoute `1 - frac_i` à l`erreur
* `floor(pi)` → ajoute `frac_i` à l`erreur
* (où `frac_i = pi – plancher(pi)` est la partie fractionnelle, 0 ≤ frac_i < 1)

Donc une fois que nous savons combien de planchers nous *must* utiliser, la *commande* des prix devient hors de propos – nous choisissons simplement les plus petites parties fractionnelles au sol, parce que cela donne la plus petite erreur. Il s'agit d'un algorithme cupide classique qui fonctionne dans le temps **O(n log n)**.

---

## 2=2 Aperçu de la solution (mise en œuvre intégrale seulement)

Chaque chaîne de prix peut être convertie en un **entier qui représente le prix × 1000**.
Cela élimine tout problème de précision de point flottant et nous permet de faire tous les arithmétiques avec des entiers simples.

Étape Ce que nous calculons Pourquoi ça compte
-- -- -- -- -- -- --
1= PrixInt = entier*1000 + frac'= Exact 3 chiffres entier
"ceilUnités" = (prixInt + 999) // 1000"""ceil(pi)" en unités entières
(prixInt % 1000) / 1000.0`.
Unité = Unité = Unité
Nombre de prix ** non entiers**
Autres Trier tous les "frac" ascendant Les plus petites fractions arrivent en premier.
Autres Pour les premiers "floorsNeeded" valeurs fractionnelles (= 0) choisir **floor** (= error += frac).
Pour toutes les autres positions, choisir **ceil** ('erreur += 1-frac'). Donne l'erreur totale minimale

Si `sumCeilUnits < cible` ou `planchers Needed` dépasse le nombre de prix *non entiers*, la tâche est impossible →

L'erreur finale est imprimée avec exactement trois décimales.

---

- Oui. Code (Java)

"Java
Importation de java.util.*;

solution de classe {
chaîne publique minimiseErreur(prix de la chaîne, objectif int) {
n = prix, longueur;
Int sumCeilUnités = 0; // somme de ceil(pi) en chiffres entiers
= 0; // combien de pi ne sont PAS entiers
double[] frac = nouvelle double[n]; // parties fractionnelles

pour (int i = 0; i < n; i++) {
Chaîne s = prix[i];
int point = s.indexOf('.');
int entier = Integer.parseInt(s.substring(0, point));
Int frac Partie = Integer.parseInt(s.substring(dot + 1)); // 3 chiffres
prix int Int = entier * 1000 + fracPart; // prix * 1000

(prixInt + 999) / 1000; // ceil(pi)
sumCeilUnités += ceilUnités;

frac[i] = (prix Int % 1000) / 1000.0; // partie fractionnelle exacte
si (prixInt % 1000 != 0) non IntCount++;
}

si (sumCeilUnits < cible) retourne "-1";

planchers Nécessaire = sumCeilUnits - cible;
si (planchers nécessaires > non inclus) retourne "-1";

Arrays.sort(frac); // zéros d'abord, puis petites fractions

erreur double = 0,0;
pour (double f : frac) {
si (f == 0.0) {
// prix entier – plancher == ceil, pas d'erreur
poursuivre;
}
si (sols nécessaires > 0) {
// choisir le plancher
erreur += f;
planchers Besoin...
} autre {
// choisissez ceil
erreur += 1.0 - f;
}
}

// après les planchers de boucle Needed doit être 0
retourner String.format(Locale.US, "%.3f", erreur);
}
}
«» "

---

Code (Python)

'`python
de taper l'importation Liste

Solution de classe:
def minimiser Erreur(self, prix: Liste[str], cible: int) -> str:
n = len(prix)
sumCeilUnités = 0
frac = [0,0] * n
non _int = 0

pour i, s en énumération(prix):
entier, frac_part = s.split('.')
entier = entier
frac_part = int(frac_part) # toujours 3 chiffres
price_int = entier * 1000 + frac_part

Ceil_unités = (prix_int + 999) // 1000
sumCeilUnités += ceil_units

f = (prix_int % 1000) / 1000.0
frac[i] = f
si f > 0,0:
non_int += 1

si sumCeilUnits < cible:
retour "-1"

planchers_nécessaires = sumCeilUnités - cible
_si nécessaire > non _int :
retour "-1"

frac.sort()
erreur = 0,0
pour f en frac:
si f == 0.0:
continuer # prix entier, aucune erreur
_si nécessaire > 0:
erreur += f
planchers nécessaires -= 1
Sinon:
erreur += 1.0 - f

# Etages_nécessaires ici
retour f"{error:.3f}"
«» "

---

Code (C++)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne minimise Erreur(vecteur<string> &prices, cible int) {
int n = prix.taille();
longue sommeCeil = 0; // somme de ceil(pi) en chiffres entiers
vectorielle <double> frac(n); // parties fractionnelles
Int non Int = 0;

pour (int i = 0; i < n; ++i) {
const string &s = prix[i];
int dot = s.find('.');
int entier = stoi(s.substr(0, point));
int fracPart = stoi(s.substr(dot + 1)); // toujours 3 chiffres
prix int Int = entier * 1000 + fracPart; // prix * 1000

(prixInt + 999) / 1000; // ceil(pi)
sumCeil += ceilUnits;

frac[i] = (prix Int % 1000) / 1000.0; // partie fractionnelle exacte
si (prixInt % 1000 != 0) + non Int;
}

si (sumCeil < cible) retourne "-1";

planchers Nécessaire = sumCeil - cible;
si (fonds nécessaires > non Int) retourne «-1 »;

tri(frac.begin(), frac.end()); // zéros d'abord
erreur double = 0,0;

pour (double f : frac) {
si (f == 0.0) continuer; // prix entier, aucune erreur de toute façon
si (sols nécessaires > 0) {
erreur += f; // plancher
Planchers Besoins;
} autre {
erreur += 1,0 - f; // ceil
}
}

retour à_string(error).substr(0, erreur < 1e-9 ? 1 : erreur < 1e-6 ? 4 : 7); // 3 décimales
}
};
«» "

> **Pourquoi ne pas utiliser `double` pour tous les calculs? * *
> Parce que chaque prix d'entrée a **exactement trois** chiffres décimaux, nous pouvons stocker la valeur comme un entier `prixInt = prix * 1000`. Tout arithmétique est alors exact, la seule opération flottante restante est `error += f` ou `1‐f`, que nous formatons à trois décimales dans la sortie.

---

Article de blog du SEO
> **Titre:** *Minimiser l'erreur d'arrondi – Le bon, le mauvais et le mauvais (LeetCode 1058)*

---

Introduction

Avez-vous déjà essayé de faire une liste de prix additionner jusqu'à un total spécifique tout en arrondissant chaque prix à la hausse ou à la baisse?
LeetCode 1058 est exactement ça. Dans le post ci-dessous, nous allons parcourir pourquoi le problème est trompeurment simple, comment un algorithme basé sur entier propre le résout, et les pièges du monde réel (le **bad**) et les astuces de la meilleure pratique (le **good**).
Nous finirons avec une section laid qui explique les cas de bord subtils qui peuvent trébucher des solutions naïves.

---

C'est vrai. Le bon produit – propre, exact, O(n log n)

* **Arithmétique intégrale** – Convertir `"2.800"` → `2800`. Pas de souci de précision double.
* **Calcul du Conseil** – «ceilUnits = (prix Int + 999) / 1000».
* **Le choix du mariage** – Une fois que nous savons combien de prix non entiers doivent être planchers, il suffit de poser les parties fractionnelles les plus petites.
* **Désormais** – Le tableau des parties fractionnelles (`frac`) est trié; les zéros passent en premier.
* **Erreur totale** – Somme de «frac» pour les positions planchers plus «1‐frac» pour le reste.

Cette approche garantit l'erreur minimale, et elle fonctionne dans `O(n log n)` en raison du tri.

---

C'est vrai. Les boîtiers de précision et de bord

* **Défauts de déplacement** – Une mise en œuvre « double » naïve peut mal interpréter « 0.300 » comme « 0.2999... », modifiant l'erreur.
* ** Listes de prix entiers** – Si chaque prix est un entier, vous pourriez penser que vous pouvez toujours choisir `floor`, mais en fait la somme ne change jamais.
* ** Trop d'étages** – `floorsNeeded > nonIntCount' devrait revenir -1,1, mais oublier cette vérification donne des réponses positives incorrectes.

Ce sont les pièges subtils que de nombreux codeurs rencontrent.

---

C'est pas vrai. Le "Ugly" – Pourquoi trier seul n'est pas suffisant

Même avec un arithmétique parfait, vous *doivez* vérifier:
1. **Somme maximale réalisable** – «sumCeilUnits».
2. ** Sols minimaux requis** – planchers nécessaires.

Si vous sautez soit vérifier, vous allez produire une réponse qui satisfait la somme mais pas les contraintes du problème, ou pire, vous allez afficher une valeur d'erreur lorsque la tâche est impossible.

---

C'est vrai. Liste de contrôle des meilleures pratiques

Que faire ?
C'est quoi ?
**Toujours compter les prix non entiers**= Vous ne pouvez pas plancher un entier sans affecter la somme. Autres
**Valider la cible**Le 'sumCeilUnits' est la limite supérieure. Autres
**Vérifier les nombres de planchers impossibles. Autres
**Trier les fractions**= Plus petites fractions → plus petites erreurs au sol. Autres
**Format exactement trois décimales**= Utiliser `String.format("%.3f", erreur)=" (Java), "f" {error:.3f}" (Python), ou une sous-chaîne manuelle en C++. Autres

---

Conclusion

LeetCode 1058 est un grand rappel que de nombreux problèmes DP ou gourmands se cachent derrière une simple transformation – ici, transformer les décimales en entiers.
La solution propre ci-dessus est à la fois efficace et robuste contre les quirks flottants.

Si vous visez cette note d'entrevue parfaite, rappelez-vous:
* **Convertissez d'abord, calculez plus tard. **
* **Vérifiez toujours la faisabilité avant de choisir avidement les décisions. **
* **Format correctement – trois décimales sont obligatoires!* *

Bon codage, et que vos sommes toujours arrondies (ou vers le bas) exactement comme vous en avez besoin!

---

*Auteur: ChatGPT*
* Publié le 2023‐08‐14*

---

Réflexions finales

* **Complexité temporelle :** O(n log n) – le tri domine.
* **Complexité spatiale:** O(n) – stockage des parties fractionnées.
* **Edge Cases:** Prix qui sont tous entiers, une cible plus grande que la somme maximale, ou une cible qui force trop de planchers.
* ** À emporter :** Les solutions intégrées sont la norme d'or pour les problèmes de précision décimale fixe – elles sont simples, rapides et infaillibles.

---

Et c'est ça ! Vous disposez maintenant d'une solution complète et prête à la production pour LeetCode 1058, ainsi que d'une explication conviviale sur le blog qui vous permet d'obtenir des points pour la profondeur algorithmique et le style de codage propre. Joyeux entretien !

---