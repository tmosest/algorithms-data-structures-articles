---
titre: LeetCode 473. Sticks à carré -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 473 – **Matchsticks to Square* *
Les bons, les mauvais et les affreux
> **Vous voulez obtenir un emploi dans la technologie? * *
> Maîtrisez ce problème, montrez une solution propre, et entrez dans votre entretien avec confiance.

---

- Oui. 1. Aperçu du problème

> **Don** un tableau entier `matchsticks`, où `matchsticks[i]` est la longueur du *i*-th matchstick.
> **Objectif**: Utilisez *tous* allumettes pour construire un **carré** (pas de bris, pas de bâtons supplémentaires).
> **Retour** « vrai » si possible, sinon « faux ».

Obstacles

- Oui.
-- -- -- -- -- --
1 <= allumettes.longueur <= 15 '=1 <= allumettes[i] <= 108 '=

---

- Oui. 2. Le bien

* **Intuitive** : Traitez-le comme un problème de partition à quatre sommes égales.
* **Backtracking**: Facile à comprendre, code minimal.
* **Bitmask DP**: Exploite la petite taille d'entrée (=15) → `2^15 = 32768` états.

---

- Oui. 3. Le "Bad"

* **La récursion naïve** explose rapidement avec 15 bâtons (boîte pire `4^15').
* **Le tri** n'est pas strictement requis mais souvent utilisé pour la taille.
* **Les plus gros nombres** (=108) peuvent causer un débordement s'ils ne sont pas traités avec `long`.

---

- Oui. 4. Les

* **Contre les contraintes** vous force à gérer de nombreux cas de bord :
* Longueur totale non divisible par 4 → immédiat `faux`.
* Un seul bâton plus long que le côté cible → impossible.
* **Les astuces de Bit-mask** peuvent être difficiles à lire pour les candidats qui ne les connaissent pas.

---

- Oui. 5. Approche optimale: DFS + Bitmask + Mémoisation

1. ** Calculer le périmètre total** et le côté **cible** (`total/4`).
2. ** Sorties précoces**
* Si "total % 4 != 0` → `faux`.
* Si un bâton > côté cible → `faux`.
3. ** DFS** sur les bâtons, essayant de construire quatre côtés.
4. Utilisez un **bitmask** pour représenter les bâtons utilisés.
5. **Mémoiser** `(masque, index latéral)` → résultat pour éviter la recomputation.

> **Pourquoi mémorisation? **
> Sans cela, l'algorithme peut revisiter des états identiques plusieurs fois, en particulier avec des longueurs dupliquées.

---

- Oui. 6. Mise en œuvre du code

Voici des solutions propres et bien commentées pour **Java**, **Python** et **C++**.

---

#### 6.1 Java

"Java
Importation de java.util.*;

solution de classe {
bâtonnets privés; // longueurs de bâtonnets
côté int privéLen; // longueur du côté cible
Int privé n; // nombre de bâtonnets
carte privée <Long, Boolean> mémo; // clé = (masque << 3)

marque de booléen public carré(int[] allumettes) {
if (matchsticks == null=" matchsticks.longueur == 0) retourner faux;
ce.n = allumettes.longueur;
Ça. bâtons = Arrays.copyOf(matchsticks, n);

long total = 0;
pour (int v : bâtons) total += v;
si (total % 4 != 0) retourner faux;

Ce.sideLen = (int) (total / 4);

// Taille précoce: un bâton plus long que le côté ne peut s'adapter
pour (int v : bâtons) {
si (v > sideLen) retourner faux;
}

// Trier en descendant pour placer les gros bâtons en premier (mieux tailler)
Arrays.sort(ceci.sticks);
inverse(ceci.sticks);

ce.memo = nouveau HashMap<>();
retour dfs(0, 0, 0);
}

/** DFS avec masque et côté actuel */
dfs booléens privés (masque int, côté intIdx, int curLen) {
clé longue = ((long)masque << 3)
si (memo.contientKey(key)) retourne memo.get(key);

// Tous les 4 côtés terminé → succès
Si (sideIdx) 3) retour vrai;

pour (int i = 0; i < n; i++) {
si ((masque & (1 << i)) != 0) continuer; // déjà utilisé
int len = bâtons[i];
si (curLen + len > sideLen) continue; // déborderait le côté courant

int newMask = masque (= 1 < < i);
int newCurLen = curLen + len;
int newSideIdx = (newCurLen == sideLen) ? SideIdx + 1 : sideIdx;
si (dfs(newMask, newSideIdx, newCurLen == sideLen ? 0 : newCurLen) {
mémo.put(clé, true);
retour vrai;
}
}

mémo.put(clé, faux);
retourner faux;
}

vide privé inverse(int[] a) {
int l = 0, r = longueur - 1;
pendant que (l < r) {
int tmp = a[l]; a[l] = a[r]; a[r] = tmp;
l++; r--;
}
}
}
«» "

---

6.2 Python

'`python
à partir de functools importer lru_cache
de taper l'importation Liste

Solution de classe:
def makesquare(self, allumettes: List[int]) -> bool:
si elle n'est pas assortie:
Retour Faux

total = somme (maquettes)
si total % 4 != 0:
Retour Faux

côté = total/ 4
si max (stickers) > côté:
Retour Faux

# Tri descendant pour placer les grands bâtons d'abord
matchsticks.sort(reverse=True)
n = len(sticots)

@lru_cache(Aucun)
def dfs(masque: int, side_idx: int, cur_len: int) -> C'est vrai.
Si side_idx == 3: # 4ème côté correspond automatiquement
retour Vrai
pour i dans la plage(n):
si masque & (1 << i):
poursuivre
si cur_len + allumettes[i] > côté:
poursuivre
nouvelle_masque = masque
new_cur = cur_len + allumettes[i]
new_side = side_idx + 1 si new_cur == side_idx
new_cur = 0 si new_cur == côté autre new_cur
si dfs(new_mask, new_side, new_cur) :
retour Vrai
Retour Faux

retour dfs(0, 0, 0)
«» "

---

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Bool makequare(vecteur<int>& allumettes) {
int n = allumettes.size();
si (n) 0) retourner faux;

long total = 0;
pour (int v : allumettes) total += v;
si (total % 4 != 0) retourner faux;

côté int = total / 4;
pour (int v : allumettes) si (v > côté) retourner faux;

tri(matchsticks.begin(), matchsticks.end(), plus grand<int>(); // descendant
Carte_non ordonnée<longe> mémo;

fonction<bool(int, int, int)> dfs = [&](int masque, int sideIdx, int curLen) -> Bool {
longue clé longue = ((long long)masque << 3)
si (memo.find(key) != memo.end()) retourne memo[key];
Si (sideIdx) 3) retour true; // dernier côté s'adapte automatiquement

pour (int i = 0; i < n; ++i) {
si (masque & (1 << i)) continuer; // déjà utilisé
int len = allumettes[i];
Si (courLen + len > côté) continue; // côté du courant de débordement

int newMask = masque (= 1 < < i);
int newCur = curLen + len;
int newSideIdx = (newCur) ? SideIdx + 1 : sideIdx;
newCur = (nouvelCur) ? 0 : newCur;
si (dfs(newMask, newSideIdx, newCur)) {
mémo[key] = true;
retour vrai;
}
}
mémo[key] = faux;
retourner faux;
};

retour dfs(0, 0, 0);
}
};
«» "

> **Pourquoi `(long)masque << 3)?**
> `mask` a besoin de 15 bits; nous décalons de 3 (depuis `0 <= sideIdx <= 3`) pour garder une clé unique.

---

- Oui. 7. Liste de contrôle des cas de bord

Condition Pourquoi ça compte
-- -- -- -- -- -- -- --
Un tableau vide ne peut pas former un carré. Autres
Autres Total non divisible par 4 : Impossible – aucun côté de longueur égale. Autres
Un seul bâton trop long → aucun ajustement. Autres
Dupliquer les longueurs Dupliquer La mémorisation gère efficacement des masques identiques. Autres
Toujours possible si chaque côté utilise plusieurs bâtonnets. Autres

---

- Oui. 8. Analyse de la complexité

Temps Espace
C'est pas vrai.
(sans taille) Autres
DFS + Bitmask + Memoussation (en milliers de dollars)
C++ carte non ordonnée 'O(2^n)' cas moyen, pire cas 'O(2^n * n)' Autres

*Avec `n <= 15`, la solution optimale fonctionne en millisecondes sur le matériel moderne. *

---

- Oui. 9. Pièges communs à éviter

1. **Débordement entier**
* Utilisez `long`/`long long` lors du summing longueurs de bâton.
2. **Manipulation de l'indice latéral de référence* *
* Rappelez-vous: après avoir terminé le côté 3 nous pouvons retourner `vrai` parce que les bâtons restants doivent former le 4ème côté.
3. ** Échelle manquante**
* Trier en descendant et placer les plus gros bâtons coupe d'abord de façon spectaculaire l'arbre de recherche.
4. ** Clé de mémo incorrecte**
* Assurez-vous que le masque et l'index latéral sont combinés de façon unique (position + OU).
5. **Délai sur bâtonnets en double* *
* Sans mémorisation, les longueurs dupliquées entraînent une explosion exponentielle.

---

- Oui. 10. Conseils de préparation à l'entrevue

Pourquoi ça aide ?
C'est quoi ?
**Exposer le problème en anglais clair** avant le codage. Montre des compétences en communication. Autres
Autres **Montrer l'intuition** (partition en 4 sommes égales). Démontre l'état d'esprit de résolution de problèmes. Autres
**Écrire un DFS propre d'abord** (pas de mémo), puis ajouter la taille. Laissez les intervieweurs voir votre processus de pensée. Autres
**Discute clairement la clé de mémo** dans votre réponse. Évite la confusion au sujet des tours de bit-mask. Autres
**La complexité temporelle de la concentration** et la raison pour laquelle les contraintes permettent des états `2^15`. Autres
**Afficher les essais de cas** (`[1,1,1,1,4]', "[1,1,1,2,2,2]". Autres

> **Promouvoir:** Après avoir résolu, demandez à l'intervieweur:
> Si nous avions 30 bâtons, cette approche serait-elle toujours en vigueur? Quels changements ?
> Il transforme une question simple en une discussion sur l'évolutivité et les compromis algorithmiques.

---

## 11. Prise- Comment résoudre ce problème

Mise en œuvre
-- -- -- -- -- -- -- -- --
**Readability**
**Efficacité**
**Évoluabilité**
**Animaux d'entrevue** . Discutez des sorties précoces, de la taille et de la complexité

---

12. Conclusion

> **LeetCode 473** est une base d'entrevue classique.
> Maîtriser le modèle de rétro-suivi avec la masque, comprendre les cas de bord et être prêt à expliquer l'algorithme en langage clair.

> **SEO-ready hook**:
> *LeetCode 473 Matchsticks to Square solution – DFS, Bitmask, Memoization – préparez-vous à votre prochain entretien technique.

---

Description de la méta
*Apprenez à résoudre le LeetCode 473 avec une approche claire DFS + bitmask. Comprendre les aspects bons, mauvais et laids, et entrer dans votre interview avec une solution polie. *

---

Bon codage, et bonne chance d'atterrissage ce rôle de rêve! C'est ce qu'il a dit