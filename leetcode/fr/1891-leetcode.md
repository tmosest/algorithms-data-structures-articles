---
titre: LeetCode 1891. Rubans de coupe -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1891. Couper les rubans – le problème ultime d'entrevue de recherche binaire
*(Code de débit #1891)*

Code de la langue
C'est quoi, ça ?
**Java** Cliquez pour agrandir</sommary>``java
***
* 1891. Rubans de coupe
* Code Leet – Moyen
*
* Complexité temporelle : O(n · log(max(ribbons))
* Complexité spatiale: O(1)
*/
solution de classe {
public int maxLength(int[] rubans, int k) {
// 1. Trouvez la longueur maximale possible dans le tableau
Int maxLen = 0;
pour (int r : rubans) maxLen = Math.max(maxLen, r);

// 2. Recherche binaire sur la réponse
int low = 1, high = maxLen, best = 0;
alors que (faible <= haut) {
int milieu = faible + (élevé - faible) / 2; // longueur du candidat

long cnt = 0; // combien de pièces nous pouvons obtenir
pour (int r : rubans) cnt += r / mi; // division entière

si (cnt >= k) { // nous pouvons produire au moins k pièces
meilleur = milieu; // milieu est un candidat
faible = milieu + 1; // essayer d'augmenter la longueur
} autre {
haute = milieu - 1; // besoin d'une longueur plus petite
}
}
le meilleur retour;
}
}
```</details> Autres
**Python**= <details><sommaire>Cliquez pour agrandir</sommaire>``python
"""
1891. Rubans de coupe – LeetCode
Complexité temporelle : O(n * log(max(ribbons))
Complexité spatiale: O(1)
"""

def maxLength(ribbons: list[int], k: int) -> Int:
# Trouvez la longueur maximale du ruban
max_len = max(ribbons)

# Recherche binaire sur la réponse
faible, élevé = 1, max_len
meilleur = 0
alors que faible <= élevé:
milieu = (faible + élevé) // 2

# Compte combien de morceaux de longueur `mid` nous pouvons obtenir
morceaux = somme(r // milieu pour r en rubans)

si des morceaux >= k:
best = mi # mi est une réponse valide, essayez d'augmenter
faible = milieu + 1
Sinon:
haute = milieu - 1 # trop de pièces, longueur trop grande

le meilleur retour
«» "
```</details> Autres
**C++** Cliquez pour agrandir</sommary>``cpp
***
* 1891. Rubans de coupe – LeetCode
* Complexité temporelle : O(n · log(max(ribbons))
* Complexité spatiale: O(1)
*/

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maxLength(vecteur<int>& rubans, int k) {
int maxLen = *max_element(ribbons.begin(), rubans.end());

int low = 1, high = maxLen, best = 0;
alors que (faible <= haut) {
int milieu = faible + (élevé - faible) / 2;

longs morceaux = 0;
pour (int r : rubans)
morceaux += r / mi;

si (pièces >= k) { // peut produire au moins k pièces
meilleur = milieu;
faible = milieu + 1; // essayer plus grande longueur
} autre {
haute = milieu - 1; // besoin de plus petite longueur
}
}
le meilleur retour;
}
};
```</details> Autres

---

Billet de blog – Rubans de coupe : les bons, les mauvais et les mauvais

> **Titre du référencement**: Couper les rubans LeetCode 1891 – Stratégie de recherche binaire, Java/Python/C++ Solutions & Conseils d'entrevue
> **Meta Description**: Master LeetCode 1891 (Cutting Ribbons) avec une solution de recherche binaire claire en Java, Python et C++. Apprenez les pièges, les tours de performance et comment assiter ce problème lors de votre prochaine entrevue sur l'ingénierie logicielle.

---

- Oui. 1. Présentation

**Cutting Ribbons** (LeetCode #1891) est un problème classique *maximum-value binaire-search* qui teste votre capacité à combiner deux concepts CS fondamentaux:

1. **Comptabilité de la graisse** – Avec un ruban de longueur `L`, combien de pièces pouvons-nous couper? (en milliers de dollars)
2. **Recherche binaire sur la réponse** – Trouver le plus grand `L` qui satisfait à la condition. (en milliers de dollars)

Si vous vous préparez à un entretien d'ingénierie **logiciel**, ce problème est un point de départ. Il est souvent demandé dans *Google*, *Amazon* et *Microsoft* entrevues. Comprendre les bonnes, les mauvaises et les mauvaises approches vous aidera **score high** sur le cycle de codage.

---

- Oui. 2. Exposé des problèmes (simplifié)

Vous avez reçu :

- Oui. Un tableau entier `ribbons` où `ribbons[i]` est la longueur du ruban i‐th.
- Un entier "k".

Vous pouvez couper chaque ruban dans n'importe quel nombre de segments *positifs entiers* (ou le laisser intact). Jetez les restes.

**Objectif**: Trouvez le maximum entier `x` de sorte que vous pouvez couper au moins `k` morceaux de longueur `x`.
Si un tel `x` n'existe pas, retourner `0`.

---

- Oui. 3. La recherche binaire bonne – efficace (O(n log m))

### 3.1. Intuition

- Si une longueur `x` fonctionne (vous pouvez couper des morceaux `k`), alors chaque plus petite longueur fonctionne aussi.
- Si une longueur `x` échoue, chaque plus grande longueur échoue aussi.

Ainsi la fonction de faisabilité est *monotonique*: `true → true → ... → false → false`.
Ceci est un scénario de manuel pour la recherche binaire sur la réponse.

3.2 Vérification de faisabilité

Texte
countPièces(L) = (ribbon / L) pour tous les rubans
«» "

- `/` est la division entière → rejette automatiquement les restes.
- Résumez le nombre de morceaux de longueur `L` de tous les rubans.

Si `countPièces(L) >= k` → `L` est *facile*.
«» "

#### 3.3. Procédure de recherche binaire

1. **Espace de recherche**: `[1, max(ribbons)]`.
("max(ribbons)" est la plus grande réponse possible).
2. **Point moyen**: < < milieu = faible + (élevé - faible) / 2 > > (éviter le débordement).
3. **Mettre à jour les pointeurs**:
- Si possible → stocker la réponse, rechercher à droite (`bas = milieu + 1`).
- Sinon → recherche gauche (`haut = milieu - 1`).

#### 3.3. Complexité

Chaque essai de faisabilité est "O(n)".
Besoins de recherche binaire `O(log max(ribbons))` itérations → `O(n log m)`.
- **Espace**: Quelques variables entières → `O(1)`.

- Oui. Tranche Traitement des cas

- **k > sum(ribbons)**: impossible → retourner `0`.
La recherche binaire donnera naturellement `0` car aucune longueur ne peut produire assez de pièces.
- **Grande "k"** : Utilisez `long long` / `long` pour éviter le trop-plein lors du summing.

---

- Oui. 4. Les mauvaises – Naïve Linear ou DP Solutions

L'approche du temps L'espace Pourquoi il est mauvais
- C'est quoi ?
Le dénombrement de la force brute de toutes les longueurs (1...max) Pire que `O(n log m)` pour une grande entrée. Autres
Une programmation dynamique sur les longueurs de rubans.O(n · max).O(max).PDP est inutile et ajoute une mémoire supplémentaire. Autres
La fenêtre coulissante à deux points O(n) O(1) s'applique pas – le problème n'est pas au sujet des sous-courses. Autres

Ces approches naïves *mismatch le problème de la propriété monotonique* et donnent **90-plus pour cent** des solutions plus lentes que la méthode de recherche binaire. Dans le cadre d'une entrevue, l'intervieweur doit **aviser immédiatement** l'inefficacité.

---

- Oui. 5. L'Ugly – Récursion incorrecte / Sur-optimisation

Certains candidats écrivent un « divis-and-conquer » récursif que *trise* pour couper des rubans et des pistes arrière en cas d'échec. Intéressant, il :

- **Souffle sur la récursion profonde** (`k` jusqu`à `10^9` → débordement de la pile).
- **Le pire cas est exponentiel**, sinon soigneusement mémorisé.
- **Difficile à lire** – les interviews récompensent *code propre et lisible*.

> ** Ligne de bottom** : S'en tenir à la boucle cupide + binaire de recherche propre. Pas besoin de récursion ou de mémoisation.

---

- Oui. 6. Pièges communs et comment les éviter

Erreurs Symptômes Correction
C'est pas vrai.
Utiliser `int` pour résumer les morceaux → déborder. Autres
Erreurs hors-par-un dans les limites de la recherche binaire Retourne `maxLen+1` ou `0` incorrectement. Autres
Ne pas manipuler `k > totalLongueur` Retourne `maxLen` au lieu de `0`-Vérification précoce: si `k > sum(ribbons)` → retourner `0`. Autres
Recalculer `maxLen` dans chaque boucle. Autres

---

- Oui. 7. Idées de modification et d'extension

1. **Different Cut Cost** – Chaque coupe coûte du temps; minimiser le coût total tout en conservant au moins `k` pièces. → Utilisez *recherche binaire* + *fonction coûts*.
2. **Longueur de la pièce Non-entier** – Autoriser les longueurs fractionnelles → recherche encore binaire mais utiliser *essai de faisabilité de point flottant*.
3. **Questions multiples** – Précalculer les montants du préfixe pour répondre à plusieurs valeurs `k` dans O(log m) chacune.

Savoir adapter l'algorithme de base vous donne *flexibilité* dans les interviews.

---

- Oui. 8. Exemples de solutions (Java / Python / C++)

(Voir le tableau de codes ci-dessus).
Chaque solution suit la même structure propre:

```pseudo
maxLen = max(ribbons)
meilleur = 0
alors que faible <= élevé:
milieu = (faible + élevé) // 2
morceaux = somme (ribbon // milieu)
si des morceaux >= k:
meilleure = moyenne
faible = milieu + 1
Sinon:
élevé = milieu - 1
le meilleur retour
«» "

---

- Oui. 9. Liste de contrôle de l'approche à suivre

- [ ] Comprendre la faisabilité *monotonique* → recherche binaire.
- [ ] Utiliser la division entière (`//` dans Python, `/` dans Java/C++).
- [ ] Conserver le compteur dans un type 64 bits pour éviter le débordement.
- [ ] Calculez l'espace de recherche "haut" une fois (`max(ribbons)`).
- [ ] Préférez `bien que faible <= élevé` sur `bien que faible < élevé` pour plus de clarté.
- [ ] Ajouter le retour anticipé `0` si `k > totalPièces(1)` (facultatif mais soigné).

---

10. Pensées finales

Couper les rubans est un **micro-écosystème** des idées CS : recherche cupide, monotonique, binaire.
- **Bon**: recherche binaire sur la réponse, faisabilité linéaire → rapide et évolutive.
- **Bad**: Force brute linéaire ou exponentielle → trop lente pour les grands tests.
- **Ugly**: Récursion trop poussée → difficile à lire et à entretenir.

Maîtrisez le modèle *bon*, évitez le *mauvais* et gardez le *puissant* loin. Vous serez prêt à résoudre ce problème lors de toute entrevue de codage, et à impressionner les gestionnaires qui s'intéressent à des solutions propres et efficaces.

---

> **Vous souhaitez avoir plus de questions d'entrevue LeetCode? * *
> Abonnez-vous à notre bulletin hebdomadaire de contestation du codage pour les problèmes curés, les questions d'entrevue et les visites vidéo. C'est ce qu'il a dit.

---