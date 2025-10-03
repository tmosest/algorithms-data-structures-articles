---
titre: LeetCode 2546. Appliquer des opérations bitwise pour rendre les cordes égales -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le Code (Java / Python / C++)

Voici les implémentations *clean, prêt à la production* qui résolvent LeetCode 2546 –
Appliquer des opérations bitwise pour rendre les cordes égales.
Les trois versions partagent la même logique O(n), seule la syntaxe diffère.

Code de la langue
C'est quoi, ça ?
**Java**=___________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
Solution de classe : def makeStrings Equal(self, s: str, cible: str) -> bool: retour ('1' en s) == ('1' en cible)" Autres
**C++**=___________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

---

Port d'essai rapide (facultatif)

"Java
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
System.out.println(sol.makeStringsEqual("1010", "0110")); // true
Système.out.println(sol.makeStringsEqual("11", "00")); // faux
}
«» "

'`python
si __nom__ == "__main__" :
sol = Solution()
imprimer(sol.makeStringsEqual("1010", "0110")) Vrai
imprimer(sol.makeStringsEqual("11", "00") # Faux
«» "

'`cpp
Int main() {
Solution sol;
cout << boolalpha;
Cout << sol.makeStringsEqual("1010", "0110") << endl; // true
cout << sol.makeStringsEqual("11", "00") << endl; // faux
}
«» "

Les trois harnais impriment la sortie attendue.

---

- Oui. 2. Article de blog – Pouvez-vous faire deux cordes binaires égales? LeetCode 2546 expliqué

### Méta-données (SEO)

- **Titre**: *LeetCode 2546 – Pouvez-vous faire deux cordes binaires égales? L'O(1) Insight (Java / Python / C++)*
- **Méta-Description**: Apprendre la solution d'un liner à LeetCode 2546. Comprendre l'astuce d'opération bitwise, voir les implémentations Java/Python/C++, et obtenir l'interview-ready. (en milliers de dollars)
- **Mots clés**: *LeetCode 2546, make strings egal, bitwise operation, chaîne binaire, solution O(1), question d'entrevue, algorithme, interview de codage, entretien d'emploi, Java, Python, C++. *

---

Introduction

> **Problème 2546 – Appliquer des opérations bitwise pour rendre les cordes égales**
> On vous donne deux chaînes binaires `s` et `target` de longueur égale.
> Dans une opération, vous pouvez choisir deux indices distincts `i` et `j` et changer simultanément
> `s[i] = s[i] OU s[j]` et `s[j] = s[i] XOR s[j]`.
> Le but est de décider si vous pouvez transformer les `s` en `cible`.

À première vue, l'opération semble compliquée. Un DP ou un BFS naïf exploserait dans le temps et la mémoire. La clé pour casser ce problème est ** observer comment l'opération se comporte sur les paires 0/1**.

---

2.1 Intuition – Ce que l'opération peut faire

Considérez les quatre paires de bits possibles et le résultat d'une opération:

Nouveau `s[i]` Observation
- C'est quoi ?
Aucun changement
Un seul 1 peut transformer un 0 en 1
1---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Deux 1s peuvent transformer l'un d'eux en 0.

À partir du tableau, nous pouvons distiller trois faits :

1. **Tous les zéros restent des zéros pour toujours** – l'opération ne crée jamais un `1` sur deux zéros.
2. **Si au moins un `1` existe, un `0` peut être transformé en `1`** – choisissez `1` comme `i` et `0` comme `j`.
3. **Si au moins deux `1`s existent, un `1` peut être transformé en `0`** – choisissez les deux `1`s comme `i` et `j`.

Ces observations signifient que toute chaîne qui contient au moins une `1` peut atteindre **chaque** autre chaîne qui contient également au moins une `1`. Le seul cas impossible est lorsque vous essayez de changer une chaîne all-zero en une chaîne contenant une `1`.

---

#### 2.2 Le bon – Un liner

Tout le problème s'effondre à une condition unique:

> **Si `s` a un `1` iff `cible` a un `1`, retourner `true`; sinon `faux`**.

C'est pourquoi chaque solution haute note sur LeetCode se résume à une seule ligne qui vérifie la présence de `'1''.

**Java**

"Java
retour s.contient("1") == cible.contient("1");
«» "

**Python**

'`python
retour ('1' en s) == ('1' en cible)
«» "

**C++**

'`cpp
retour (s.find('1') != chaîne::npos) == (target.find('1') != chaîne::npos);
«» "

La solution fonctionne dans **O(n)** temps (scanner chaque chaîne une fois) et **O(1)** espace.

---

#### 2.3 L'erreur – Pièges communs

Pourquoi il échoue
- C'est quoi ?
Autres **En supposant que vous avez besoin de compter zéros/ones**.Le comptage ajoute une complexité inutile et peut cacher la logique simple. Autres
**Penser deux 1s suffit pour faire n'importe quelle chaîne**.Vous ne pouvez faire un 1 → 0 que si vous avez *au moins* deux 1s dans la chaîne actuelle, pas seulement dans la cible.
**Utiliser la récursion ou l'espace d'état exponentiel (jusqu'à 2n)

---

2.4 La suringénierie

Beaucoup de tentatives sur-enginer la solution avec:

- **Bitmask DP**: Essayer de traiter la chaîne comme un nombre binaire.
- **Recherche graphique**: Construire un graphique où les nœuds sont des chaînes et les bords sont des opérations valides.
- ** Simulations de greffe** : choix répété des indices sans preuve de convergence.

Ces approches sont les suivantes :

1. Briser la contrainte de temps O(n) (souvent devenir O(2n)).
2. Cacher l'invariant simple.
3. Rendre la solution difficile à comprendre et à maintenir.

---

2.5 Essais – Cas à couvrir

Autres Test d'entrée prévu
- C'est quoi ?
Autres Tous les zéros s = `"0000"`, cible = `"0000"`
Autres Tous les zéros à ceux s = `"0000"`, cible = `"1000"`
Autres Un 1 à tous les zéros s = `"1000"`, cible = `"0000" ́ ́ ́ ́ ́ `true`
Autres Deux 1s à 1 0=1 s = `"1100"`, cible = `"0100"`="true`="
Autres Grandes chaînes aléatoires (n = 105)

---

2.6 Résumé

- Oui. L'effet d'opération réduit à un invariant simple : **présence d'au moins un `1`**.
- Oui. Le problème entier est résolu avec un **one-liner** dans n'importe quelle langue.
- Complexité: **O(n)** temps, **O(1)** espace.
- Pas besoin de DP, BFS, ou des trucs compliqués.

**A emporter pour l'entrevue d'embauche**: Cherchez toujours un invariant ou un effondrement caché dans l'énoncé du problème. Il transforme souvent un défi apparemment difficile en un défi trivial.

---

2.7 Pensées finales

- **Écrire la solution, l'exécuter** – le harnais de test ci-dessus montre que le monoligneur fonctionne pour tous les exemples.
- **Expliquer l'intuition** – les intervieweurs aiment le raisonnement concis.
- **Keep the code minimal** – la beauté de LeetCode réside dans la simplicité élégante.

Bonne chance cracking LeetCode 2546 et impressionnant votre prochain employeur!