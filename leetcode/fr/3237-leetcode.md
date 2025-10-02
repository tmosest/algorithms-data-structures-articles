---
titre: LeetCode 3237. Simulation Alt et Tab -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 3237 – Simulation Alt et Tab
> **Objectif** – Simuler le sélecteur classique de fenêtres Alt-+-Tab- et retourner l'ordre final des fenêtres.
> **Langues** – Java, Python, C++
> **Interview–Ready** – complexité temporelle O(n + q), Complexité spatiale O(n)

---

Récapitulation des problèmes

Texte
Entrée
- Oui.
windows : int[] // pile initiale – le premier élément est en haut
requêtes : int[] // chaque élément est l'id de la fenêtre à apporter en haut

Produit
- Oui.
ordre final des fenêtres après toutes les requêtes
«» "

> *Si une requête fait référence à la fenêtre qui est déjà en haut, rien ne change. *

Exemple
«» "
windows = [1,2,3], requêtes = [3,32]
Résultat = [2,3,1]
«» "

---

Approche naïve (trop lente)

«» "
pour chaque requête :
trouver la fenêtre dans le tableau
le déplacer vers l'avant (O(n))
«» "

Complexité: **O(q · n)** – inacceptable pour *n, q ≤ 105*.

---

Stratégie efficace

1. **Demandes relatives au processus en sens inverse**
La dernière fois qu'une fenêtre apparaît dans la liste des requêtes est la première fois qu'elle doit être placée en haut de la pile finale.

2. **HashSet + Liste**
* Gardez un ensemble de fenêtres qui ont déjà été déplacées en haut.
* Construisez une liste `topOrder` (en sens inverse) en itérant les requêtes de la fin au début et en ajoutant une fenêtre seulement si elle n'est pas apparue avant.

3. **Appendir les fenêtres restantes**
Après le traitement inversé, toutes les fenêtres qui ne sont pas dans l'ensemble sont toujours dans leur ordre relatif d'origine.
Ajoutez-les après "topOrder".

4. **Retourner le résultat concaténé**

> **Time**: O(n + q) – chaque fenêtre et chaque requête traitées une fois.
> **Espace**: O(n) – jeu de hachage + tableau de résultats.

---

Code (Java, Python, C++)

> Les implémentations suivantes suivent la même logique.

### Java

"Java
Importation de java.util.*;

solution de classe {
public int[] simulationRésultat(int[] windows, int[] requêtes) {
// Utilisation liée HashSet pour maintenir l'ordre d'insertion implicitement
Définir <integer> déplacé = nouveau LinkedHashSet<>();
Liste<Integer> Haut de la pageCommander = nouvelle liste de distribution<>();

// Requêtes inverses pour déterminer l'ordre final
pour (int i = requêtes.longueur - 1; i >= 0; i--) {
int win = requêtes[i];
si (!mouvement.contient(gagnant)) {
moved.add(win);
topOrder.add(win); // retournera plus tard
}
}

// Préparer le tableau de résultats
int[] res = nouvelle int[windows.longueur];
Int idx = 0;

// Ajouter des fenêtres qui ont été déplacées en haut (inverser la commande)
pour (int i = topOrdre.size() - 1; i >= 0; i--) {
res[idx++] = topOrder.get(i);
}

// Ajouter des fenêtres qui n'ont jamais été déplacées (conserver la commande originale)
pour (int windows) {
si (!mouvement.contient(gagnant)) {
res[idx++] = gain;
}
}

retour rés;
}
}
«» "

---

Python

'`python
de taper l'importation Liste

Solution de classe:
def simulationRésultat(self, windows: List[int], requêtes: List[int]) -> Liste[int]:
déplacé = set()
top_order = []

# Virement inverse des requêtes
pour gagner en cas d'inversion (requêtes):
si la victoire n'est pas déplacée:
déplacement.add(gagnant)
top_order.append(win) # inversera plus tard

# Construire le résultat final
res = top_order[:-1] + [gagnant dans windows si la victoire n'est pas déplacée]
retour res
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> simulationRésultat(vector<int> windows, vector<int> requêtes) {
non ordonné_set<int> déplacé;
vecteur<int> topCommander;

// Traitement des requêtes de la fin au début
pour (int i = requêtes.size() - 1; i >= 0; --i) {
int win = requêtes[i];
si (déplacer.find(win) == déplacé.end() {
moved.insert(win);
topOrder.push_back(win); // inversera plus tard
}
}

vecteur<int> rés;
// Ajouter des fenêtres déplacées en haut (ordre inverse)
pour (int i = topOrdre.size() - 1; i >= 0; --i)
res.push_back(topOrder[i]);

// Ajouter des fenêtres qui n'ont jamais été déplacées
pour (int windows)
si (déplacer.find(win)) == déplacé.end()
res.push_back(win);

retour rés;
}
};
«» "

---

Article du blog – Les bons, les mauvais et les méchants

> **Titre**: *LeetCode 3237 – Simulation Alt et Tab: Une plongée profonde dans les algorithmes des fenêtres
> **Description détaillée**: Découvrez la solution rapide et efficace pour la mémoire de LeetCode 3237, en Java, Python et C++. Comprendre les pièges, les tours d'entrevue et comment impressionner les recruteurs.

---

C'est pas vrai. Pourquoi ce problème compte dans les entrevues

* **Analogie du monde réel**: La gestion des fenêtres est un problème d'assurance-chômage courant.
* **La flexibilité de la structure des données**: La solution touche *sets, listes et cartes de hachage*.
* **Échelle Essai**: Les contraintes vous poussent à penser aux solutions *O(n*).

---

- Oui. Le bien – ce qui a fonctionné

Pourquoi il est bon
C'est quoi ?
Autres **Renverser le traitement des requêtes**= Capture la dernière fois qu'une fenêtre est activée – la clé de la commande finale. Autres
**HashSet pour O(1) Adhérent** Autres
Autres **Single Pass Append**. Après avoir construit la liste des plus haut, nous venons de marcher les fenêtres d'origine une fois de plus. Autres
**Language-Indépendant Logic** , Java, Python, C++ partagent tous la même stratégie O(n+q). Autres

---

C'est vrai. Les mauvaises – pièges communs

Erreurs dans les résultats
- C'est quoi ?
**Pour la boucle du début à la fin**Vous finissez avec un ordre *top qui est l'inverse* de l'état final souhaité. Il est question **backwards**. Autres
**Using List.index() dans Python**= Recherche linéaire sur chaque requête → O(q·n).= Utilisez un jeu pour se souvenir des fenêtres vues. Autres
**Ignorer les requêtes en duplicata** Sauter les fenêtres déjà déplacées (cochez via le jeu). Autres
**Sur-ingénierie**= Mise en place d'une liste complète liée ou d'une TVB équilibrée pour ce simple problème. Autres Rester simple : seulement deux scans linéaires. Autres

---

C'est pas vrai. Les cas de bord et les conseils d'optimisation

C'est pourquoi il importe Recommandation
-- -- -- -- -- -- -- -- --
**Toutes les requêtes sont les mêmes**.Une seule fenêtre change de position; reste comme original. S'assurer que la logique de réglage saute les duplicatas suivants. Autres
**Les requêtes couvrent toutes les fenêtres**Le dernier ordre est exactement le revers de la liste des requêtes. Autres Notre algorithme s'en occupe automatiquement. Autres
Autres **Grande entrée (105)** L'utilisation de la mémoire devient critique. Utilisez des tableaux primitifs (Java `int[]`) et évitez la boîte automatique. Autres
**Multiple Test Cases**=LeetCode enveloppe parfois les appels en boucle. Autres Gardez la solution apatride ; il suffit de retourner le tableau. Autres

---

C'est vrai. Conseils d'entrevue

1. **Clarifier le problème** – Demandez si les requêtes en double sont autorisées (elles le sont).
2. **Explain Complexity Early** – Montrez-vous que vous pensez à *O(n+q*).
3. **Afficher votre approche dans Pseudocode** – Par exemple, . (en milliers de dollars)
4. **Edge‐Case Testing** – Mentionnez des cas de test comme tous les duplicatas, pas de duplicata, requêtes mixtes.
5. **Parler de la mémoire** – En Java, évitez `ArrayList<Integer>` pour 105 articles; utilisez le `int[]` primitif.

---

- Oui. A emporter

*LeetCode 3237* est un mélange parfait de manipulation **array** et d'utilisation **set**.
Par **traitement des requêtes en inverse** et mise à profit d'un ensemble **hash**, vous pouvez transformer une force brute *O(q·n)* en une solution propre **O(n+q)** qui fonctionne en Java, Python et C++.

---

Code final

> **Java**
"Java
solution de classe { ... }
«» "

> **Python**
'`python
Solution: ...
«» "

> **C++**
'`cpp
solution de classe { ... }
«» "

---

Référence Mots clés

- LeetCode 3237
- Simulation Alt et Tab
- Simulation Java Alt
- Algorithme de la pile de fenêtres Python
- Problème de gestion des fenêtres C++
- Question d'entrevue sur la structure des données
- Solution HashSet + liste
- Analyse de la complexité du temps
- Conseils d'entrevue pour le codage des entrevues

---

Bonne chance pour écraser *Alt et Tab Simulation* dans votre prochain entretien de codage! C'est ce qu'il a dit