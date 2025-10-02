---
titre: LeetCode 2427. Nombre de facteurs communs -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Nombre de facteurs communs (LeetCode 2427) – Un guide complet
*Java, Python, & C++ Solutions + un référencement optimisé Blog Post pour stimuler votre jeu d'entrevue*

---

Table des matières
1. [Récapitulation des problèmes] (#récapitulation des problèmes)
2. [Approches naïves et optimales] (#approches naïves-vs-optimales)
3. [La solution fondée sur le GCD](#la solution fondée sur le GCD)
4. [Analyse de la complexité] (#analyse de la complexité)
5. [Listages de codes complets](#Listages de codes complets)
- [Java] (#Java)
- [Python] (#python)
- [C++](#cpp)
6. [Le Bon, le Mal et le Malheur]
7. Pourquoi ça compte pour votre recherche d'emploi ?
8. [Take-Away final](#final-take-away)

---

- Oui. 1. Récapitulation du problème <un nom="problème-recap"></a>

**LeetCode 2427 – Nombre de facteurs communs**
> **Don** deux entiers positifs `a` et `b` (1 ≤ a, b ≤ 1000),
> **Retour** le nombre de entiers `x` de telle sorte que `x` divise à la fois `a` et `b`.

> **Exemples**
> *Input:* `a = 12, b = 6` → **Output:** `4` (`{1, 2, 3, 6}")
> *Input:* `a = 25, b = 30` → **Output:** `2` (`{1, 5}`)

---

- Oui. 2. Approches naïves et optimales <une approche naïve-vs-optimale></a>

L'approche de l'idée de la complexité temporelle de l'espace de la complexité quand il fonctionne
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Brute-Force**Énumérer tous les entiers de `1` à `min(a, b)` et vérifier la disvisibilité. `O(min(a, b))` (= 1000)="O(1)`=" Fonctionne parce que les contraintes sont minuscules, mais il s'écaille mal si les limites grandissent. Autres
Calculer `g = gcd(a, b)`; compter les diviseurs de `g`. Autres

Alors que la solution Brute-Force est parfaitement acceptable pour les contraintes données, **la solution basée sur le GCD est l'approche « good »** – elle est évolutive, mathématiquement élégante et démontre une pensée algorithmique plus profonde – quelque chose que les intervieweurs aiment.

---

- Oui. 3. La solution fondée sur le GCD <un nom>

1. ** Calculer le GCD**
Le plus grand diviseur commun de `a` et `b` est le plus grand nombre qui divise les deux. Tous les facteurs communs de `a` et `b` sont exactement les divisions de ce GCD.

2. **Diviseurs de nombre de g**
Pour chaque entier `i` de `1` à ` √g`:
- Si `i` divise `g`, augmentez le nombre.
- Si `i` n'est pas égal à `g / i`, incrémenter à nouveau le compte (pour tenir compte du diviseur complémentaire).

3. **Retourner le total**.

---

- Oui. 4. Analyse de complexité <un nom="analyse de complexité"></a>

Étape
C'est quoi ?
Calculer le GCD (algorithme euclidien) Autres
Autres Diviseurs de compte de "g" , "O" Autres
**Total**** "O" (μg)"** ( pire affaire ~ 32 pour g = 1000)
Espace Autres

L'algorithme est *presque* temps constant pour les limites du problème, et il s'échelle facilement si `a` et `b` deviennent beaucoup plus grands.

---

- Oui. 5. Listes complètes de codes <un nom="listes complètes de codes"></a>

### Java <a name="java"></a>
"Java
Importation de java.util.*;

solution de classe publique {
// Algorithme euclidien pour GCD
Int privé gcd(int x, int y) {
pendant que (y != 0) {
l'entrée tmp = x % y;
x = y;
y = tmp;
}
retour x;
}

commune Facteurs(int a, int b) {
g = gcd(a, b);
nombre int = 0;
pour (int i = 1; i * i <= g; i++) {
si (g % i] 0) {
count++; // diviseur i
si (i != g / i) count++; // diviseur complémentaire
}
}
le nombre de retours;
}
}
«» "

> **Pourquoi c'est bien* *
> * Séparation nette des préoccupations (aide).
> * Utilise l'algorithme euclidien (GCD optimal).
> * Traversée linéaire seulement jusqu'à √g.

---

### Python <un nom="python"></a>
'`python
Solution de classe:
def gcd(self, a: int, b: int) -> Int:
tandis que b:
a, b = b, a % b
retour a

Fréquent Facteurs(auto, a: int, b: int) -> Int:
g = auto.gcd(a, b)
nombre = 0
i = 1
alors que i * i <= g:
si g % i] 0:
nombre += 1
i != g // i:
nombre += 1
i += 1
Nombre de retours
«» "

> **Pourquoi c'est bien* *
> * La boucle pythonique et la division entière.
> * Pas de bibliothèques supplémentaires; entièrement autonomes.

---

### C++ <a name="cpp"></a>
'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// Algorithme euclidien
int gcd(int a, int b) {
pendant que (b != 0) {
tmp = a % b;
a = b;
b = tmp;
}
retour a;
}

Fréquent Facteurs(int a, int b) {
g = gcd(a, b);
nombre int = 0;
pour (int i = 1; i * i <= g; ++i) {
si (g % i] 0) {
++compte; // diviseur i
si (i != g / i) ++compte; // diviseur complémentaire
}
}
le nombre de retours;
}
};
«» "

> **Pourquoi c'est bien* *
> * Utilise l'arithmétique en entier rapide, la mémoire minimale.
> * `bits/stdc++.h` est acceptable dans le codage concurrentiel; sinon inclure `<algorithm>` et `<numérique>`.

---

- Oui. 6. Le Bon, le Mauvais, et l'Ugly <un nom, le bon, le mauvais et le mauvais"></a>

Autres Phase: Code typique: Ce qui ne va pas?
- C'est quoi ?
**Bon**="pour (int i = 1; i * i <= g; ++i)="Contrôle supérieur correct, aucun contrôle redondant=" Autres
**Bad**="pour (int i = 1; i <= Math.max(a, b); ++i)="Loops up to 1000, inutile quand `g` est petit="
**Pour (int i = 1; i <= g; ++i) { si (a % i] 0 && b % i] 0) count++; }`= O(min(a,b)) runtime; échoue pour 109 entrées.

**Traitements clés:**
- **Toujours penser GCD d'abord** – il effondre l'espace de problème.
- **Éviter les opérations de modulo répétées** – ne calculer qu'une seule fois par candidat.
- **Ne présumez jamais que les contraintes resteront petites** – écrivez des solutions à cette échelle.

---

- Oui. 7. Pourquoi cela compte pour votre chasse à l'emploi <un nom> <un nom</a>

- **Les intervieweurs aiment les optimisations basées sur les mathématiques.** Un candidat qui choisit la route GCD montre qu'il comprend la théorie des nombres et l'efficacité algorithmique.
- **Les tests de codage cachent souvent des contraintes subtiles.** Même si les limites du LeetCode sont faibles, les employeurs peuvent tester des entrées cachées plus importantes.
- **Le code propre est favorable à l'embauche.** Les solutions fournies ont des lignes minimales, aucune dépendance supplémentaire, et des commentaires clairs – parfaits pour un portfolio ou un GitHub Gist.
- **Mauvaise maîtrise de la langue.** Présenter les versions Java, Python et C++ démontre la capacité d'adaptation – un grand plus pour les rôles technologiques qui nécessitent plusieurs piles.

---

- Oui. 8. Take‐Away final <a name="final-take‐away"></a>

> **Le problème de facteurs communs est un terrain de jeu parfait pour montrer la maturité algorithmique. **
> * Commencez par une preuve brute de la force.
> * Refactor to GCD + calcul du diviseur – c'est la solution "good".
> * Gardez le code maigre, bien commenté, et le langage-agnostique.

> Lorsque vous partagez ces extraits sur votre CV, votre blog ou votre portfolio de codage, vous ne vous contentez pas de résoudre un problème – vous racontez une histoire sur l'efficacité, la clarté et la capacité d'échelle**. C'est exactement ce que les employeurs veulent.

Bonne chance, et que votre code compile proprement dans chaque langue! C'est ce qu'il a dit.

---