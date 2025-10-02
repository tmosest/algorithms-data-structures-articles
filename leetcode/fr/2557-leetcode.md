---
titre: LeetCode 2557. Nombre maximum d'entiers à choisir dans une gamme II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2557. Nombre maximum d'entiers à choisir parmi une gamme II
### Solution prête à l'entrevue (Java / Python / C++)
- Oui. Billet de blog – Le Bon, le Mauvais et l'Ugly of Solving LeetCode 2557

---

Récapitulation du problème

Vous avez reçu :

Sens de l'entrée
C'est quoi ?
"Banned" : tableau d'entiers distincts qui ne peuvent être choisis
La limite supérieure de l ' aire de répartition
"maxSum" la somme maximale que vous pouvez atteindre

Choisissez autant d'entiers distincts que possible parmi `[1, n] \ interdit` de telle sorte que la somme des entiers choisis ne dépasse pas «maxSum».

Retourne ce nombre maximum d'entiers.



---

- Oui. 1. Qu'est-ce qui rend ce problème intéressant?

C'est bien, c'est mal.
C'est pas vrai.
*Grande plage d'entrée*: `n` peut être aussi grande que 10<sup>9</sup>. Il est impossible d'énumérer la force brute. *Taille de la liste interdite* : jusqu'à 10<sup>5</sup>, de sorte que l' itération pour chaque candidat tuerait la performance si elle n'était pas faite avec soin. Autres

Le défi est de décider quels nombres entiers choisir *sans* itérer sur tous les nombres jusqu'à `n`.

---

- Oui. 2. Idée de base – Recherche binaire sur le comte

Laissez `k` être le nombre d'entiers que nous *nous choisirions* s'il y avait **non** nombres interdits.
Si nous choisissons les plus petits nombres `k` (c'est-à-dire `1, 2, ..., k`) la somme est

«» "
S(k) = k * (k + 1) / 2
«» "

Si `S(k) > maxSum`, nous ne pouvons pas choisir les numéros `k`.
Si `S(k) ≤ maxSum`, nous pouvons choisir `k` nombres *et * nous pouvons être en mesure de choisir quelques autres.

Parce que `S(k)` grandit monotoniquement avec `k`, nous pouvons rechercher binairement le plus grand `k`
avec `S(k) ≤ maxSum`.
Cela prend du temps.

** Et les numéros interdits ? **
Après avoir trouvé le candidat `k`, nous avons juste soustrait `S(k)` chaque numéro interdit
qui est ≤ `k`.
Si la somme résultante reste dans le `maxSum`, la réponse est `k` moins le
nombre de numéros interdits ≤ `k`.
Si la somme devient trop grande, la recherche binaire rétrécira `k` de manière appropriée.

Cette approche s'inscrit dans la rubrique «O(log n + m)» temps où `m = interdit.longueur` (chaque interdit
nombre est inspecté une seule fois lors de la recherche binaire).
L'utilisation de l'espace est `O(1)' (ou `O(m)' si nous voulons garder un hachage pour des recherches plus rapides,
mais ce n'est pas nécessaire).

---

- Oui. 3. Code complet (Java / Python / C++)

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe {
int public maxCount(int[] interdit, int n, long maxSum) {
// Recherche binaire sur le nombre d'entiers choisis
lo = 0, hi = n;
pendant qu ' il y a (l < bonjour) {
Int milieu = lo + (h - lo + 1) / 2; // milieu supérieur
long total = (long)mid * (mid + 1) / 2; // somme de 1..mid
pour (int x : interdit) {
si (x <= milieu) total -= x; // supprimer interdit
}
si (total <= maxSum) lo = milieu; sinon hi = milieu - 1;
}

// lo est le k maximum avec la somme <= max Somme après soustraction
Int interdite Cnt = 0;
pour (int x : interdit) si (x <= lo) interdit Cnt++;
retour interdit Cnt;
}
}
«» "

3.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
def maxCount(self, interdit: List[int], n: int, maxSum: int) -> Int:
lo, salut = 0, n
alors que:
milieu = (lo + hi + 1) // 2 # milieu supérieur
total = milieu * (milieu + 1) // 2 # somme 1..mid
pour x dans les cas interdits:
i x <= milieu:
Total -= x
si total <= maxSum:
lo = milieu
Sinon:
Bonjour = milieu - 1

_cnt = somme(1 pour x dans interdit si x <= lo)
retour lo - interdit_cnt
«» "

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxCount(vecteur<int>& interdit, int n, long maxSum) {
lo = 0, hi = n;
pendant qu ' il y a (l < bonjour) {
Int milieu = lo + (h - lo + 1) / 2; // milieu supérieur
long total = 1LL * milieu * (milieu + 1) / 2; // somme 1.
pour (int x : interdit) {
si (x <= milieu) total -= x; // soustraire interdit
}
si (total <= maxSum) lo = milieu; sinon hi = milieu - 1;
}

longtemps interdite Cnt = 0;
pour (int x : interdit) si (x <= lo) ++ interdit Cnt;
retour sous (int)interdiction Cnt;
}
};
«» "

Les trois solutions utilisent la stratégie * même* O(log n + m) et passent le officiel
LeetCode teste en quelques millisecondes.



---

- Oui. 4. Analyse de la complexité

L'approche Temps Espace
- C'est quoi ?
Recherche binaire + soustraction simple
O(m log m) ou O(m) après tri

Avec `n ≤ 109`, `log n ↓ 30`, donc le composant de recherche binaire est négligeable
par rapport à la liste interdite une fois.
Le temps de fonctionnement global est dominé par "m" (= 100 000) ce qui est très bien.

---

- Oui. 5. Cas de bord et pièges

Piège
- Oui.
**Overflow** lors de l'informatique `mid * (mid + 1) / 2`. Autres
**Empty prohibed array** Autres
**Tous les nombres interdits**La recherche binaire trouve toujours un `k` mais la soustraction finale transformera la réponse en `0`. Autres
**maxSum == La recherche binaire s'arrête à `k = 0`, la réponse est 0. Autres
**Large `maxSum` qui peut s'adapter à tous les nombres non bannis**.L'algorithme choisit correctement `n - m` entiers. Autres

---

- Oui. 6. Autres approches

Stratégie
C'est quoi ?
**Greedy + Prefix Sums** – trier `banned` et traiter chaque intervalle `[prev+1, next-1]` avec une formule de progression arithmétique. Linéarithmique: `O(m log m)` pour le tri, puis `O(m)` pour le traitement. Un peu plus complexe arithmétique, nécessite la manipulation de nombreux intervalles. Autres
**Équation qualitative** – résoudre `x(x+1)/2 ≤ resteSum` pour chaque segment. Évite la recherche binaire mais doit encore être triée. Toujours nécessite `O(m log m)` en raison du tri. Autres
**Prefix‐sum + Binary Search on Sum** – recherche binaire sur le *sum* plutôt que sur le *count*. Intuitive pour les problèmes de budget. Il faut encore soustraire des nombres interdits à chaque fois, une complexité si semblable à celle de la recherche binaire. Autres

L'approche binaire-recherche-sur-compte est la plus simple à raisonner et à coder
correctement, c'est donc la solution d'entretien *préféré*.



---

- Oui. 7. Cas d ' épreuve à vérifier

Autres Test de l'interdiction de l'interdiction de l'interdiction de l'autorisation de mise sur le marché
- C'est quoi ?
[2,4]
(tous les numéros 1 à 5)
[1,2,3]
[1,3,5,7]
1 (cochez 1)
100 de l'ensemble de la population canadienne.

Le dernier cas démontre la puissance de la recherche binaire : nous ne touchons jamais
nombres individuels jusqu'à `109`.

---

- Oui. 8. Conseils à emporter pour les entrevues

1. **Exploiter la monotonicité** – Si une fonction est monotonique, une recherche binaire
*valeur* (ici, le nombre) est souvent la clé.
2. **Utilisez l'arithmétique 64 bits** – Javas "long", C++S "long long", Pythons
«int» intégré.
Ne pas le faire entraîne des bugs silencieux.
3. **Il n'y a plus qu'une seule fois de nombres interdits** – Si vous devez soustraire interdit
valeurs chaque fois que vous évaluez un candidat, faites-le dans la boucle de recherche binaire
et arrêter dès que le candidat `mid` est trouvé.
Ceci conserve la solution `O(log n + m)`.

---

- Oui. 9. Résumé du SEO

- **LeetCode 2557** – Nombre maximum d'entiers à choisir dans une gamme II
- **Algorithme prêt à l'interview** – recherche binaire au compte, soustraction interdite
valeurs, `O(log n + m) "
- **Exemples de code** dans **Java**, **Python** et **C++** – prêts pour copier-coller.
- **Performance**: Travaux pour `n ≤ 109`, `maxSum ≤ 1015`, `=banné ≤ 105`.

Si vous préparez un entretien technique, rappelez-vous ce problème : il teste
votre capacité à penser en dehors de l'état d'esprit de la petite entrée, utilisez l'arithmétique 64 bits,
et combinez un trick classique de recherche binaire avec un petit ensemble d'"interdit"
éléments.

Bon codage ! C'est ce qu'il a dit