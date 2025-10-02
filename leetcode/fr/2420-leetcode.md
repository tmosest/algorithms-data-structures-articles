---
titre: LeetCode 2420. Trouver tous les bons indices -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 2420 – Trouver tous les bons indices
**Langues:** C++
**Complexité:** **Heure** O(n) **Espace** O(n) (peut être réduit à O(1) avec un tour de fenêtre coulissant)

---

1.1 Récapitulation du problème

Compte tenu d'un tableau «nums» (taille «n») et d'un entier «k», un indice «i» est **bon** si

* `k ≤ i < n-k`
* Les éléments «k» *avant* «i» sont dans l'ordre **non croissant**
* Les éléments `k` *après* `i` sont dans l'ordre ** non décroissant**

Retournez tous les bons indices en ordre ascendant.

> **Exemple**
> `nums = [2,1,1,1,3,4,1], k = 2 → [2,3]`

---

1.2 Intuition

La façon naïve de comparer chaque fenêtre de longueur `k` autour de chaque candidat `i` – c'est-à-dire O(n k) et TLE.
La clé est **précomputing** combien de temps une course monotone s'étend de chaque position:

Côté gauche
C'est quoi ?
Pour chaque index `i` magasin `decLeft[i]` – combien d'éléments consécutifs non croissants finissent à `i` (y compris `i`). Autres
Pour chaque index `i` magasin `incRight[i]` – combien d'éléments consécutifs non décroissants commencent à `i` (y compris `i`). Autres

Une fois que nous avons ces deux tableaux, index `i` est bon iff
«decLeft[i-1] ≥ k» ** et** `incRight[i+1] ≥ k`.

Les deux tableaux sont construits dans un scan linéaire chaque → O(n) temps, O(n) mémoire.
La vérification pour chaque candidat est O(1), donc l'algorithme entier est O(n) time, O(n) memory.

---

1.3 Mise en œuvre

Ci-dessous sont propres, des implémentations commentées dans **Java, Python et C++**.

---

#### 1.3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<entier> goodIndices(int[] nums, int k) {
int n = longueur nums;
Liste <Integer> res = nouvelle liste de distribution<>();

// 1. tableau de préfixe: longueur de l'exécution non croissante se terminant à i
int[] decLeft = nouvelle int[n];
dcLeft[0] = 1; // élément unique
pour (int i = 1; i < n; i++) {
decLeft[i] = (nums[i - 1] >= nombres[i]) ? dcLeft[i - 1] + 1 : 1;
}

// 2. tableau suffixe: longueur de l'exécution non décroissante commençant à i
int[] incRight = nouvelle int[n];
Incright[n - 1] = 1;
pour (int i = n - 2; i >= 0; i--) {
incRight[i] = (nums[i] <= nombres[i + 1]) ? IncRight[i + 1] + 1 : 1;
}

// 3. vérifier chaque centre possible
pour (int i = k; i <= n - k - 1; i++) {
si (décLeft[i - 1] >= k && incRight[i + 1] >= k) {
l'alinéa i est remplacé par le texte suivant:
}
}

retour rés;
}
}
«» "

---

##### 1.3.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def goodIndices(self, nombres: List[int], k: int) -> Liste[int]:
n = len(nums)

# préfixe: plus longue course non croissante se terminant à i
dec_left = [0] * n
dec_left[0] = 1
pour i dans la plage (1, n):
dec_left[i] = dec_left[i - 1] + 1 si nombres[i - 1] >= nombres[i] autres 1

# suffixe: plus longue course sans diminution à partir de i
Inc_right = [0] * n
inc_right[-1] = 1
pour i dans la plage (n - 2, -1, -1):
Inc_right[i] = inc_right[i + 1] + 1 si nombres[i] <= nombres[i + 1] autres 1

# Recueillir de bons indices
ans = []
pour i dans la plage (k, n - k):
si déc_left[i - 1] >= k et inc_right[i + 1] >= k:
Annexe(i)
retour et
«» "

---

#### 1.3.3 C++ (C++17)

'`cpp
#incluez <vecteur>
#incluez <string>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> goodIndices(vector<int>& nums, int k) {
int n = nombres.size();
vector<int> decLeft(n), incRight(n);

// préfixe
decLeft[0] = 1;
pour (int i = 1; i < n; ++i) {
decLeft[i] = (nums[i-1] >= nombres[i]) ? decLeft[i-1] + 1 : 1;
}

// suffixe
incRight[n-1] = 1;
pour (int i = n-2; i >= 0; --i) {
IncRight[i] = (nums[i] <= nombres[i+1]) ? incRight[i+1] + 1 : 1;
}

vecteur <int> ans;
pour (int i = k; i <= n-k-1; ++i) {
si (décLeft[i-1] >= k && incRight[i+1] >= k)
le nom de l'autorité compétente;
}
le retour des an;
}
};
«» "

---

- Oui. 2. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 2420

> **Titre**: *=LeetCode 2420 – Trouver tous les bons indices: le bon, le mauvais, et le mauvais
> **Mots-clés cibles**: LeetCode 2420, Trouver tous les bons indices, interview d'algorithme, solution Java, solution Python, solution C++, codage d'entretien d'emploi

---

2.1 Introduction

Si vous êtes à la recherche d'un rôle d'ingénierie logicielle, vous avez probablement regardé les mêmes problèmes LeetCode encore et encore. L'une de ces questions de niveau moyen est **2420. Trouver tous les bons indices**. Bien que la déclaration soit simple, les solutions naïves peuvent être trompeusement lentes.

Dans cet article, nous allons passer par:

1. **Qu'est-ce qui fait que ce problème est une bonne question d'interview.
2. **La bonne solution** – une approche O(n) DP/prefix-suffixe propre (Java/Python/C++).
3. **Les mauvaises approches** – pièges communs qui conduisent à TLE ou MLE.
4. **Les laid** – les cas de bord et comment les manipuler sans sur-ingénierie.
5. **Pratiques à emporter** pour votre prochaine entrevue.

---

2.2 Pourquoi ce problème mérite d'être étudié

Aspect Pourquoi ça compte dans une interview
-- -- -- -- -- ----------------------------------
**Array + Two-Pointer DP** Autres
**Runs monotoniques**= Montre la compréhension des techniques de préfixe/suffixe – un point de départ dans de nombreux problèmes d'entrevue. Autres
Autres **Échanges entre l'espace et le temps**= Possibilité de discuter de la réduction de la mémoire O(n) à O(1) avec une fenêtre coulissante. Autres
**Connaissance d'Edge**=k = 1', tableau de tous les nombres égaux, tableau avec pics alternés – bon pour la discussion. Autres

---

2.3 La bonne solution – Préfixe + suffixe DP

**Idée de base**
*Précompter, pour chaque indice, jusqu'où la propriété monotone s'étend des deux côtés. *

1. **Préfixe gauche** – «decLeft[i]»: longueur de la plus longue subarraie non croissante qui se termine à «i».
Texte
decLeft[i] = (nums[i-1] >= nombres[i]) ? decLeft[i-1] + 1 : 1
«» "
2. **Suffixe droit** – «incRight[i]»: longueur de la plus longue subarraie non décroissante qui commence à «i».
Texte
IncRight[i] = (nums[i] <= nombres[i+1]) ? incRight[i+1] + 1 : 1
«» "
3. **Vérifier chaque candidat** – pour `k ≤ i < n-k`:
Texte
si décLeft[i-1] ≥ k et incRight[i+1] ≥ k → i est bon
«» "

**Pourquoi ça marche* *
Le côté gauche d'un bon indice doit contenir des éléments consécutifs `k` qui ne s'élèvent jamais. Cela signifie exactement que la fin de la course à `i-1` est au moins `k`. La même logique s'applique au côté droit.

**Complexités* *
- **Heure**: `O(n)` (deux scans linéaires + un contrôle linéaire)
- **Espace**: `O(n)` pour les deux tableaux auxiliaires (peut être paré à O(1) si vous préférez la version coulissante).

**Les extraits de code**
* (voir les implémentations Java, Python et C++ ci-dessus)*

---

2.4 Les mauvaises approches – Pièges communs

Pourquoi il échoue
C'est pas vrai.
**Les boucles imbriquées de la force brute** – pour chaque élément `i` scan gauche `k` et les éléments `k` droite= O(n·k) → TLE quand `n` = 105 et `k` -
**Utiliser `ArrayList<Integer>` pour les préfixes sans pré-allouer**. Autres
**Brides d'index incorrectes** – erreurs hors-par-un lors de l'accès à «decLeft[i-1]» ou "incRight[i+1]"" conduit à "ArrayIndexOutOfBoundsException". Autres
**Misinterpréter "non-croissant" vs "non-décreasing"** Autres

**À emporter :**
Toujours vérifier les conditions des limites; le problème limite explicitement `i` à `k ≤ i < n-k`.

---

#### 2.5 Le mauvais – les cas de bord et les conditions du coin

Qu'est-ce que regarder ?
C'est ce qu'on dit.
`k = 1''' L'exigence de longueur d'exécution devient banale; il faut quand même s'assurer que nous n'avons pas accès aux indices hors limites. Conserver les boucles comme `k ≤ i <= n-k-1`. Autres
Chaque côté satisfait la monotonicité; la réponse est tous les indices dans l'intervalle. Les formules DP gèrent correctement les comparaisons `>=` et `<=`. Autres
Des pics alternants (`1 3 2 4 3 5 ...`) Les tableaux DP seront tous `1`; algorithme retourne la liste vide comme prévu. Autres
Une seule candidate `i = k`. La boucle fonctionne toujours; assurez-vous que vous ne manquez pas le dernier `i` valide. Autres
Grande `n` mais petite limite de mémoire (par exemple, 256 Mo) Si elle est serrée, implémentez la fenêtre coulissante O(1) : ne gardez que les longueurs actuelles `k` pendant la numérisation. Autres

---

2.6 Conseils pratiques pour votre entrevue

1. ** Expliquez votre plan d'abord** – écrivez les deux passes DP sur le tableau blanc avant de coder.
2. ** Mettre en avant l'optimisation O(n)** – les intervieweurs aiment entendre J'ai évité les boucles imbriquées. (en milliers de dollars)
3. ** Optimisation de l'espace de concentration** – faire connaître la variante O(1).
4. **Discus test** – demander à l'intervieweur d'aider à penser aux cas d'angle.
5. **Conservez votre code lisible** – même dans une entrevue, des noms de variables propres (`decLeft`, `incRight`) et une aide logique concise.

---

2.7 Conclusion

LeetCode 2420 est un problème de moyen qui cache un truc de DP soigné. La solution **good** est une approche préfixe-suffixe qui fonctionne dans le temps linéaire. Les approches **bad** vous apprennent à surveiller les bugs TLE et off-by-one. Les cas de bord **ugly** nous rappellent que même un algorithme propre peut échouer si vous manquez une liaison unique.

La maîtrise de ce problème vous donne un motif réutilisable – préfixe/suffixe pour les contraintes monotoniques – et vous démontre que vous êtes prêt à relever des défis d'entrevue dans le monde réel. Bon codage, et bonne chance pour votre prochain entretien technique!

---

### 2.8 Ressources et lectures supplémentaires

- LeetCode Discussion sur le problème 2420
- Boîte à outils algorithmique – Techniques de préfixe et suffixe
- Cracking the Coding Interview – Exemples de PDD à deux points
- GitHub Gist avec les trois solutions linguistiques (Java, Python, C++)

---

*Auteur*: *Votre nom*, *Ingénieur logiciel et recruteur technique*
* Publié le*: *2024‐04‐27*

---

> **Meta‐Note**: L'article est structuré de manière à offrir de la valeur aux lecteurs qui pourraient être sur la clôture au sujet de la difficulté du problème, et il se termine par des stratégies d'entrevues exploitables. En intégrant les mots-clés cibles naturellement dans les rubriques, le texte du corps et les commentaires de code, l'article est convivial pour le référencement et prêt à être classé sur les moteurs de recherche pour les balises spécifiées.