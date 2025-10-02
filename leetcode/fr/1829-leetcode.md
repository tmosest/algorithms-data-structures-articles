---
titre: LeetCode 1829. XOR maximum pour chaque requête -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions 3 langues

Vous trouverez ci-dessous trois implémentations prêtes à travailler et prêtes à produire** qui résolvent LeetCode 1829 – *XOR maximal pour chaque requête* – en temps O(n) et en espace supplémentaire O(1).
Chaque extrait comprend la même logique, uniquement exprimée dans la syntaxe de son langage.

> **Pourquoi ça marche* *
> La valeur maximale qui peut être obtenue par `xor φ k` où `k < 2^maximumBit` est `2^maximum Bit – 1' (tous les bits inférieurs sont fixés à 1).
> Si nous connaissons le XOR actuel du tableau (`curXor`), choisir
> `k = masque curXor ^` (où `masque = 2^maximumBit – 1`) fait
> `curXor -k = masque`.
> Ainsi, pour chaque requête, nous sortons simplement `curXor ^ mask` et puis *supprimer* le dernier élément par XOR en le sortie de `curXor`.

"Java
- Non, pas du tout.
// Java 17 – Code Leet 1829 – XOR maximum pour chaque requête
- Non, pas du tout.
solution de classe publique {
public int[] getMaximumXor(int[] nums, int maximumBit) {
dans curXor = 0;
pour (int num : nums) curXor ^= num; // XOR de l'ensemble du tableau

masque int = (1 << maximumBit) - 1; // 111...1 (maximumBit bits)
int n = longueur nums;
int[] ans = nouvelle int[n];

pour (int i = 0; i < n; i++) {
Ans[i] = masque curXor ^; // réponse pour cette requête
curXor ^= nombres[n - 1 - i]; // supprimer le dernier élément
}
le retour des an;
}
}
«» "

'`python
♪ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# Python 3 – Code Leet 1829 – XOR maximum pour chaque requête
♪ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
def getMaximumXor(nums, maximumBit):
cur_xor = 0
pour num en nombres: # XOR de tous les nombres
cur_xor ^= num

masque = (1 << maximum) - 1
n = len(nums)
ans = [0] * n

pour i dans la plage(n):
ans[i] = masque cur_xor ^
cur_xor ^= nombres[n - 1 - i] # supprimer le dernier élément
retour et
«» "

'`cpp
- Non, pas du tout.
// C++17 – Code Leet 1829 – XOR maximum pour chaque requête
- Non, pas du tout.
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> getMaximumXor(vecteur<int>& nums, int maximumBit) {
dans curXor = 0;
pour (int num : nums) curXor ^= num; // XOR de l'ensemble du tableau

masque int = (1 << maximumBit) - 1;
int n = nombres.size();
vecteur <int> ans(n);

pour (int i = 0; i < n; ++i) {
ans[i] = masque curXor ^;
curXor ^= nombres[n - 1 - i]; // supprimer le dernier élément
}
le retour des an;
}
};
«» "

> **Les trois solutions fonctionnent dans le temps O(n) et n'utilisent que de l'espace supplémentaire O(1). **
> Ils comptent sur le fait que le XOR *maximum* réalisable pour un "maximumBit" donné est toujours le masque bitwise lui-même, qui simplifie considérablement le problème.

---

- Oui. 2. Billet de blog – Le bon, le mauvais, et le mauvais de LeetCode 1829

Titre
** XOR maximum pour chaque requête (Code de Leet 1829) – Le bon, le mauvais et le mauvais *

Description de la méta
Apprenez à fissurer LeetCode 1829 dans le temps O(n). Découvrez l'astuce bit-wise, les cas de bord, et pourquoi cette solution simple bat une approche naïve O(n2). Code en Java, Python et C++.

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Intuition et principale conclusion] (#intuition)
3. [La solution O(n) élégante](#solution)
4. [Justices et pièges] (#cas de référence)
5. [Analyse de la complexité] (#complexité)
6. [Pourquoi l'array trié est un hareng rouge]
7. [Le "Bad" – Une erreur commune](#bad)
8. [L'Ugly – Sur-ingénierie du problème] (#ugly)
9. [Code Snapshots (Java / Python / C++)](#code)
10. [Traitements et conseils d'entrevue](#tâches)

---

<a name="problème-overview"></a>
- Oui. 1. Aperçu du problème

> **LeetCode 1829 – XOR maximum pour chaque requête**
> **Difficulté:** Moyenne
> **Input:**
> * `nums` – un tableau trié de `n` entiers non-négatifs (0 ≤ nombres[i] < 2^maximumBit).
> * `maximumBit` – le nombre de bits qui lient la valeur `k` (`0 ≤ k < 2^maximumBit`).
> **Objectif:** Pour chaque requête, trouvez le `k` qui maximise
> `nums[0] nombres XOR[1] XOR ... nombres XOR[nums.longueur-1] XOR k`.
> Après avoir répondu, supprimer le dernier élément de `nums`. Retournez la liste de réponses.

**Exemple**
Texte
nombres = [0,1,1,3], maximumBit = 2
Sortie → [0,3,2,3]
«» "

---

<un nom></a>
- Oui. 2. Intuition et principales perspectives

Le crux est que le XOR *maximum* obtenu lorsque vous êtes autorisé à choisir un `k` sous une largeur fixe de bit est toujours une chaîne de tous les 1=2:

Texte
masque = (1 << maximumBit) - 1 // par exemple, maximum Bit = 3 → masque = 0b111 = 7
«» "

Pourquoi ?
- Le XOR de n'importe quel nombre `x` avec `masque` retourne chaque bit: `x = masque = ~x & masque`.
- La plus grande valeur que vous pouvez atteindre avec `k` est `mask` lui-même, parce que tout résultat XOR est limité par `mask`.
- Oui. Si vous connaissez le XOR actuel du tableau, dites `curXor`, la façon *seulement* de garantir que `curXor = k = masque` est de choisir

Texte
k = cur Masque Xor
«» "

Ainsi, la réponse pour chaque requête est tout simplement "curXor " masque.
Après avoir répondu, le dernier élément est supprimé, qui en termes XOR est juste `curXor ^= lastElement`.

**Traitement des clés**:
> *Le XOR maximal pour chaque requête est `currentXOR ^masque`. Aucune structure de données lourde n'est nécessaire. *

---

<un nom="solution"></a>
- Oui. 3. La solution O(n) élégante

1. Calculez le XOR de l'ensemble du tableau – appelez-le `curXor`.
2. Calculer `masque = (1 << maximumBit) - 1`.
3. Pour `i` de `0` à `n-1`
* `ans[i] = masque curXor ^ "
* `curXor ^= nums[n-1-i]` — supprimer le dernier élément.

Pas de boucles intérieures, pas de structures de données auxiliaires.
L'algorithme fonctionne parce que XOR est *commutative* et *associative* : la suppression d'un élément est la même que XOR la sortie.

---

<un nom="cases"></a>
- Oui. 4. Cas de bord et pièges

Autres Décision Pourquoi ça compte ?
C'est-à-dire
"maximumBit = 1"" "masque = 1" – plus petit masque non zéro" Soyez prudent avec le déplacement des bits; "(1 << 1)" est "2". Autres
"nums" contient `0`=" XOR avec `0` n'a aucun effet. Autres
Une seule requête fonctionne toujours – `curXor` est l'élément unique. Autres
Grand `maximumBit` (jusqu'à 20) Pas de débordement en Java/Python/C++. Autres
**Sortie**= Garanties d'entrée triées=Le tri n'est pas pertinent – l'algorithme ne dépend pas de l'ordre. Autres

---

<un nom="complexité"></a>
- Oui. 5. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
XOR tous les éléments
Boucle pour répondre aux questions
**En dehors du tableau de sortie/vecteur)

---

<a name="sorted-array"></a>
- Oui. 6. Pourquoi l'array trié est un hareng rouge

Beaucoup d'intervieweurs incluent "nums" est trié, juste pour vous tromper en pensant que vous avez besoin d'une solution *deux points* ou *binaire-recherche*.
En réalité, le triage ne donne aucun avantage parce que XOR est indépendant de l'ordre.
Ne perdez pas de temps à trier – cela coûterait O(n log n) et donne toujours le même résultat.

---

<a name="bad"></a>
- Oui. 6. L'erreur commune

** Approche naïve :**
Pour chaque requête, recalculez le XOR du tableau *remaining* et essayez chaque `k` possible de `0` à `2^maximum Bit – 1':

Texte
pour chaque requête :
curXor = XOR(nums[0...len-1])
meilleur = 0
pour k en 0 ... masque:
best = max(meilleur, curXor ^ k)
«» "

**Pourquoi c'est mauvais**
- **Complexité temporelle:** O(n · 2^maximumBit).
Avec "Bit maximum = 20", "2^Bit maximum = 1 048 576".
Pour `n = 10^5`, cela signifie 10^11 opérations – astronomiquement lentes.
- **Les boucles inutiles** le rendent *tardy* pour le juge en ligne et inutile dans un cadre d'entrevue.

Si vous le remarquez dans une entrevue, assurez-vous de demander si vous pouvez éviter la boucle intérieure. L'astuce "mask" élimine le besoin d'itérer sur tous les "k" possibles.

---

<a name="ugly"></a>
- Oui. 7. Le problème de la suringénierie

> **Les gens essaient parfois de construire une Trie des bits du tableau** (comme le problème classique de paire XOR maximum).
> Alors qu'un peu sage Trie est puissant, il s'agit d'un **over-kill** parce que:
> * Chaque requête demande un *différent* `k` qui ne dépend que du *current* XOR de tout le tableau.
> * Supprimer un élément est trivial dans XOR – pas besoin d'ajuster une Trie.
> * Construire et interroger une Trie ajouterait O(n · maximumBit) frais généraux.

**Ligne de bottom:**
> Gardez votre solution aussi *stateless* que possible. La suringénierie de la structure des données ne fera que distraire le simple tour du masque.

---

<un code de nom></a>
- Oui. 6. Captures de code (Java / Python / C++)

*(Voir la section Solutions linguistiques de la page 3 ci-dessus.) *
Chaque extrait suit les étapes exactes:

Texte
masque = (1 << maximum) - 1
Ans[i] = masque curXor ^
curXor ^= nombres[n-1-i] // supprimer le dernier élément
«» "

N'hésitez pas à copier-coller dans votre IDE préféré ou compilateur en ligne.

---

<a name="takeaways"></a>
- Oui. 7. A emporter et conseils d'entrevue

1. **Enfiler le lien en premier* *
*Lorsque la réponse est limitée par un peu de masque, c'est souvent le masque lui-même. *
2. **Utiliser les propriétés XOR**
*XOR est associatif, commutatif, et un nombre XOR avec lui-même est 0. *
3. **Demander des éclaircissements**
*Est-ce que le tri est important?* – Sinon, vous pouvez sauter le tri et gagner du temps.
4. ** Expliquez le tour de masque* *
*Parler à travers pourquoi `curXor ^ masque` donne le XOR maximum. Les intervieweurs aiment entendre le raisonnement. *
5. **Afficher vos côtelettes en 3 langues**
*L'utilisation du même algorithme en Java, Python et C++ démontre la flexibilité du langage – un plus pour les rôles de conception complète ou système. *

---

Dernier verdict

> **Bonne solution:** O(n) avec un truc propre.
> **Bad:** Oublier que le masque est le maximum XOR conduit à des boucles inutiles.
> **Ugly:** Construire un tri complexe ou trier à nouveau le tableau est une pure suringénierie.

Si vous pouvez expliquer l'astuce de masque et de livrer l'un des trois extraits de code ci-dessus, vous serez prêt à ace LeetCode 1829 et impressionner les intervieweurs à la fois. Bon codage 