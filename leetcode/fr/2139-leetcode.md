---
titre: LeetCode 2139. Déplacements minimums pour atteindre le score cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Déplacements minimums pour atteindre le score cible – un complet Guide (Java + Python + C++)

> **SEO-Optimized Title**: *LeetCode 2139 – Déplacement minimum pour atteindre le score cible – Java, Python, C++ Solutions, Greedy Algorithm, Time Complexity, Interview Prep*

---

Aperçu du problème

LeetCode #2139 – **Le minimum passe à l'atteinte du score cible** (Moyenne)

> Vous commencez à l'entier `1`.
> Dans un mouvement, vous pouvez :
> 1. `x = x + 1` (incrément) – utilisations illimitées
> 2. `x = 2 * x` (double) – au maximum `maxDoubles` heures
>
> **Objectif:** atteindre la «cible» avec le nombre minimum de mouvements.

> **Constraints**
> «1 ≤ objectif ≤ 109 "
> `0 ≤ maxDoubles ≤ 100`

---

- Oui. Intuition : travailler en arrière

La stratégie la plus efficace est de penser *de la cible de retour à 1*.

Pourquoi?
* Doublage est *puissant* seulement lorsque le nombre actuel est *petit*.
* À l'inverse, le doublage devient le doublage (l'opération la plus rentable).
* Vous voulez utiliser un double aussi tard que possible et autant de fois que vous pouvez.

**Greedy règle (simulation inverse)* *

État de l'action
- C'est quoi ?
La "cible" est **odd** D'après les données
La "cible" est **même**
Autres Pas de "maxDoubles" à gauche

La boucle s'arrête lorsque `cible` devient `1` ou que nous manquons de double opportunité.

---

- Oui. Algorithme

Texte
mouvement = 0
pendant la cible > 1 et maxDoubles > 0:
si la cible est étrange:
mouvements += 2 # diminution + moitié
cible -= 1
Sinon:
mouvements += 1 # seulement moitié
cible //= 2
maxDoubles -= 1

# incréments restants si cible > 1
mouvement += cible - 1
retour
«» "

* **Complexité temporelle**: `O(log cible)` – chaque boucle réduit de moitié `cible`.
* **Complexité spatiale**: `O(1)` – espace auxiliaire constant.

---

- Oui. Pourquoi ça marche (Le Bon)

* **Optimalité** – Dans la direction inverse l'opération de réduction de moitié est toujours le meilleur que vous pouvez faire avec un double.
* **Simplicité** – La boucle est courte, pas de récursion, pas de table DP.
* **Évoluabilité** – Fonctionne pour la plus grande "cible" (`109`) parce qu'elle ne fait qu'itérer "=30` fois.

---

## 5:0 Pièges potentiels (Le mauvais)

Numéro
C'est quoi ?
Autres Oubliant de diminuer "maxDoubles" après une moitié "maxDoubles -= 1" dans chaque itération de boucle
Le mélange de l'incrément vers le haut vers le haut vers le bas dans la simulation inverse
Le cas des bords est "maxDoubles". La boucle ne s'exécutera jamais, vous sauterez tout droit sur `cible‐1'

---

Code anti-patterns

1. **Récursif DFS avec mémoisation** – surkill, haute mémoire.
2. **BFS** – espace d'état exponentiel (nœuds `109`).
3. **Manipulation de gros entiers non nécessaire** – L'int de Python est parfait, mais évitez le débordement de 64 bits en C++ si vous utilisez `int` et déplacez les valeurs négatives.

---

## 7-

#### 7.1 Java

"Java
solution de classe publique {
Int public int minMoves(int cible, int maxDoubles) {
mouvement int = 0;
pendant que (cible > 1 && maxDoubles > 0) {
si ((cible & 1)] 1) { // impair
mouvement += 2; // diminution + moitié
cible -= 1;
} autre { // même
+= 1; // seulement moitié
}
cible >>= 1; // diviser par 2
maxDoubles--;
}
mouvement de retour + (cible - 1); // incréments restants
}
}
«» "

7.2 Python

'`python
Solution de classe:
def minMoves(self, cible: int, maxDoubles: int) -> Int:
mouvement = 0
pendant la cible > 1 et maxDoubles > 0:
si cible % 2: # impair
mouvements += 2 # diminution + moitié
cible -= 1
Autre: # même
mouvements += 1
cible //= 2
maxDoubles -= 1
mouvement de retour + (cible - 1)
«» "

### 7.3 C++

'`cpp
solution de classe {
public:
int minMoves(int cible, int maxDoubles) {
mouvement int = 0;
pendant que (cible > 1 && maxDoubles > 0) {
si (cible & 1) { // impair
mouvement += 2; // diminution + moitié
cible -= 1;
} autre { // même
mouvements += 1;
}
cible >>= 1; // diviser par 2
--maxDoubles;
}
les mouvements de retour + (cible - 1);
}
};
«» "

---

Tableau de complexité

Langue Heure Espace
- C'est quoi ?
Java (cible de l`O(log)) Autres
Python "O(cible de log)" "O(1)" Autres
"O(log cible)" "O(1)" Autres

---

FAQ

Question Réponse
C'est pas vrai.
Autres **Puis-je utiliser l'approche cupide quand `maxDoubles` est grand?**= Oui, parce que chaque itération de boucle consomme un double, garantissant une utilisation optimale. Autres
Autres **Et si `cible` est déjà La fonction retourne `0` – aucun déplacement nécessaire. Autres
**Est-ce que `int` est sûr pour le C++?**= Oui, parce que `cible ≤ 109` et que nous ne débordons jamais la gamme 32-bit pendant la réduction de moitié. Autres
Autres **Qu'en est-il si `maxDoubles` est 0?**- Nous sautons la boucle et retournons `target‐1` (tous les incréments). Autres

---

Bonus : exécuter le code localement

"""
# Python
Python3 - <<'PY'
de solution d'importation
print(Solution().minMoves(19, 2)) # 7
print(Solution().minMoves(5, 0)) # 4
PY
«» "

"""
♪ Java
Javac Solution.java
java Solution
«» "

"""
Numéro C++
g++ -std=c++17 solution.cpp -O Sol
./sol
«» "

---

Conclusion

L'approche **reverse cupidy** offre une solution optimale, propre et rapide pour LeetCode 2139.
Ses principaux avantages pour vos entrevues d'emploi :

1. **Pensez à l'envers** – souvent réduit considérablement la taille du problème.
2. **Greedy avec une preuve d'optimalité** – la réduction de moitié est toujours la meilleure stratégie à double usage.
3. ** Garder le code maigre** – pas de structures de données inutiles, espace O(1).

Partagez ce post avec vos pairs, et n'hésitez pas à modifier le code pour s'adapter à votre style de codage. Bonne chance pour écraser l'interview !

---

> **Balises de référence:** LeetCode 2139, Déplacements minimums pour atteindre la cible Note, Solution Java, Solution Python, Solution C++, Algorithme gourmand, question d'entretien, prép d'entretien de codage, analyse d'algorithme, codage d'entretien d'emploi.