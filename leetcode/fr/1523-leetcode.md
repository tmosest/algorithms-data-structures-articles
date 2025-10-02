---
Titre: LeetCode 1523. Compter les nombres dans un intervalle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1523 – Nombres par défaut dans un intervalle
Les bons, les mauvais et les méchants
*(Guide convivial pour le référencement qui vous aidera à débarquer cette entrevue d'ingénierie logicielle)*

---

### TL;DR
- **Problème**: Compter les nombres entiers dans la gamme inclusive `[faible, élevé]`.
- **Constraints**: "0 ≤ faible ≤ élevée ≤ 10^9".
- ** Solution optimale**: temps O(1), espace O(1).
- **Pièges communs**: erreurs hors-par-un, division entière quirks, ignorant les grandes valeurs.

> **Vous voulez impressionner les intervieweurs? * *
> Montrez que vous savez *pourquoi* les maths fonctionnent, et soyez prêt à discuter *cas de pointe* et *alternatives* (p. ex., deux-pointeurs).

---

- Oui. 1. Exposé des problèmes

> **LeetCode 1523 – Nombres par défaut dans un intervalle* *
> Compte tenu de deux nombres entiers «faible» et «élevé» non négatifs, retourner le nombre de nombres impairs entre «faible» et «élevé» (inclus).

Exemples
Taux de croissance
C'est pas vrai.
3, 5, 7
Dénomination des marchandises

---

- Oui. 2. Recapture des contraintes

Valeur
- C'est quoi ?
"faible" "0 ... 10^9"
"haut" "bas ... 10 ans

Parce que la plage d'entrée peut être énorme, *iterating* sur chaque entier est **non** acceptable pour une solution de style interview.

---

- Oui. 3. Approches

### 3.1. Brute-Force (temps O(n))

Texte
nombre = 0
pour i de faible à élevée:
i % 2 == 1:
nombre += 1
Nombre de retours
«» "

**Pourquoi c'est mauvais**:
- Temps linéaire → 1 milliard d'itérations le pire.
- Limites de temps sur les grandes entrées.
- Un intervieweur ne s'y attend pas.

---

3.2. Formule mathématique – **Bien** (heure O 1)

**Observation* *
- Le nombre de nombres entiers impairs dans `[0, x]` est `(x + 1) / 2` (division entière).
Pourquoi ? *
- Pour `x = 0` → 0 cotes → `(0+1)/2 = 0`.
- Pour `x = 1` → 1 impair → `(1+1)/2 = 1`.
- Chaque étape ajoute 1 impair si `x` est impair, sinon pas de nouveau impair.

Par conséquent:

«» "
Count(haut) - Count(bas-1)
«» "

'`cpp
compte intOdds(int bas, int haut) {
auto impairUpTo = [](long long x) {
retour (x + 1) / 2; // division entière
};
retour impairUpTo(high) - impairUpTo(low - 1);
}
«» "

- **Heure**: "O(1)"
- **Espace**: "O(1)"
- **Edge-case**: Quand `faible = 0`, `faible-1 = -1` → `(−1+1)/2 = 0`, ce qui est exact.

> **Pourquoi il s'agit de la solution "Good"* *
*Simplicité*, *exactitude*, *temps constant* et *mémoire constant*.
> Parfait pour les interviews.

---

#### 3.3. Deux-pointeurs – **Les Ugly** (O(n) mais encore mieux que la force brute)

Texte
1. Faites bas le premier nombre impair dans la gamme.
2. Faites haut le dernier nombre impair de la gamme.
3. Comptez combien d'étapes vous pouvez sauter en deux étapes.
«» "

**Java** (de l'extrait que vous avez posté):

"Java
solution de classe {
compte d'intérêt publicOdds(int bas, int haut) {
si (faible) élevé) retour (faible % 2 == 0) ? 0 : 1;

// Faire bas bizarre
faible = (faible % 2) 0) ? faible + 1 : faible;
// Faites de l'étrange
haut = (haut % 2) 0) ? haut - 1 : haut;

nombre int = (faible !=élevé) ? 2 : 0;
pendant que (faible < haut) {
faible += 2;
-= 2;
si (faible < élevé) nombre += 2;
}
si (faible) 1;
le nombre de retours;
}
}
«» "

- **Temps**: `O(n/2)` ( pire-cas ~5 × 108 itérations → encore trop lent pour l'entrevue).
- **Espace**: "O(1)"

> **Pourquoi c'est la solution de "gugly"* *
> Ça marche, mais tu tournes toujours sur l'intervalle.
> La version mathématique est beaucoup plus propre et plus rapide.

---

- Oui. Python monoligne – **Clean** (O(1))

'`python
Solution de classe:
def countOdds(self, low: int, high: int) -> Int:
retour (élevé + 1) // 2 - faible // 2
«» "

- Utilise la division entière (`//`).
- Manipulation automatique du boîtier de bord `faible = 0`.

---

3.5. Une ligne C++ – **Même plus propre** (O(1))

'`cpp
solution de classe {
public:
compte intOdds(int bas, int haut) {
retour (élevé + 1) / 2 - faible / 2;
}
};
«» "

---

- Oui. 4. Analyse de la complexité

L'approche Temps Espace
- C'est quoi ?
Brute-Force Autres
Formule mathématique Autres
"O" (haut - bas)" Autres
Python monoligne / C++ Autres

La solution optimale fonctionne en temps constant, indépendamment de la taille des entrées, et n'utilise que quelques variables.

---

- Oui. 5. Cas courants

Pourquoi ça compte Comment la solution mathématique la gère
C'est-à-dire
"faible = 0" "faible-1 = -1` → division négative" "(−1+1)/2 = 0` → correcte"
La formule fonctionne toujours
Grandes entrées Utiliser `long long` en C++ / `long` en Java si nécessaire
"low" ou "high" impair vs even" Off-by-one en boucle naïve La logique de division entière explique naturellement la parité

---

- Oui. 6. Conseils d'entrevue

1. **Démarrer avec la perspicacité des mathématiques** – expliquer comment vous pouvez compter les cotes jusqu'à n'importe quel `x`.
2. **Écrire la formule** sur le tableau: `compte = (élevé + 1) / 2 - faible / 2`.
3. **Cas de bord de discussion**: zéro, plages d'éléments uniques, très grands nombres.
4. **Temps et complexité de l'espace**: mentionnez O(1) et pourquoi il est optimal.
5. **Afficher la connaissance des alternatives**: vous pouvez utiliser une approche à deux points, mais il est inutile.

Les intervieweurs aiment quand vous:
- *Connais la solution la plus rapide.
- *Expliquer* pourquoi cela fonctionne (le raisonnement mathématique).
- *Anticiper* pièges et cas de bord.

---

- Oui. 7. A emporter

- **Bien**: formule temps constant.
- **Bad** : dénombrement de la force brute.
- **Ugly**: Deux points avec boucle inutile.

Maîtrisez la formule, comprenez sa dérivation, et vous allez clouer cette question dans toute interview technique.

---

Prêt à impressionner les recruteurs ?
- **Ajouter** cette solution à votre portefeuille.
- **Tag** votre blog avec: `LeetCode 1523`, `Count Odd Numbers`, `O(1) algorithme`, `Java`, `Python`, `C++`, `Coding Interview`, `Logiciel Engineer`.

Bon codage – et bonne chance pour votre prochaine entrevue!