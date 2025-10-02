---
titre: LeetCode 3684. Maximiser la somme des éléments distincts au plus K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

**Code de leet #3684 – Valeur maximale de la somme d'éléments distincts au plus K* *

> Compte tenu d'un tableau "nums" d'entiers positifs et d'un entier `k`, choisissez **au plus** `k` éléments tels que
> 1. Les numéros choisis sont **distincts**
> 2. Leur somme est maximale
> 3. Retourner les numéros choisis dans l'ordre ** strictement descendant**

La longueur du tableau est jusqu'à 100, chaque élément jusqu'à \(10^9\).

---

- Oui. 2. Esquisse de solution rapide

1. **Dupliquer** – placer tous les nombres dans un `Set` (ou `unordered_set` / `TreeSet`).
2. **Trier descendant** – convertir en liste/array, trier en ordre décroissant.
3. **Prenez le premier `k`** – qui est le sous-ensemble de la somme maximale.

Parce que `k` n'est jamais plus grand que le nombre d'éléments distincts, nous pouvons simplement couper les premières valeurs `k`.
L'algorithme fonctionne dans \(O(n \log n)\) temps (le tri domine) et utilise \(O(n)\) espace supplémentaire.

---

- Oui. 3. Mise en œuvre des références

3.1 Python 3

'`python
Solution de classe:
def maxKDistinct(self, nombres: list[int], k: int) -> list[int]:
"""
Dédoublement, tri en descendant, tranche k.
"""
1. Dédoublement
unique = set(nums)

2. Tri descendant
trié_desc = trié(unique, inversé=True)

# 3. Prenez les premiers éléments k
retourner trié_desc[:k]
«» "

** Version monoligne** (parfaite pour les concours de codage):

'`python
Solution de classe:
def maxKDistinct(self, nums, k):
retour trié(set(nums), inverse=True)[:k]
«» "

---

#### 3.2 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
Int[] maxKDistinct(int[] nums, int k) {
// Utilisez un TreeSet pour garder les numéros triés automatiquement (commande décroissante)
TreeSet<Integer> ts = nouveau TreeSet<>(Collections.reverseOrder());
pour (int n : nombres) ts.add(n);

int[] résultat = nouveau int[Math.min(k, ts.size())];
Int idx = 0;
pour (int val : ts) {
en cas de rupture (idx >= k);
résultat[idx++] = valeur;
}
le résultat du retour;
}
}
«» "

> **Pourquoi TreeSet?**
> Il supprime les duplicata *et* garde les éléments triés, donc nous n'avons jamais besoin d'une étape de tri explicite.

---

### 3.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> maxKDistinct(vecteur<int>& nums, int k) {
// Unordered_set pour la duplication O(1)
unordered_set<int> uniq(nums.begin(), nums.end());
// copier vers le vecteur et trier en descendant
vecteur<int> vals(uniq.begin(), uniq.end());
tri(vals.begin(), vals.end(), plus grand<int>();
// prendre jusqu'aux éléments k
si (k < (int)vals.size()) vals.resize(k);
les valeurs de retour;
}
};
«» "

---

- Oui. 4. Article de blog – Le bon, le mauvais, le mauvais de LeetCode #3684

4.1 Introduction

Si vous êtes en préparation pour une interview technique, l'un des problèmes les plus courants de la liste est **Maximize Sum of At Most K Distinct Elements**. Il semble simple mais vous apprend à penser à **déduplication, tri et terminaison anticipée** – toutes les compétences que les intervieweurs aiment voir.

Dans ce post, nous allons marcher à travers:

- Pourquoi le problème a l'air facile mais peut vous faire monter
- Une solution propre de 3 lignes (Python) et ses équivalents Java/C++
- Cas de bord qui peuvent vous mordre
- Conseils pour garder le code propre et facile à tester
- Comment utiliser ce problème pour obtenir un emploi

Et, bien sûr, nous allons le garder SEO-friendly: LeetCode 3684 solution, -maximiser la somme au plus k éléments distincts, -interview défi de codage, etc.

---

4.2 La bonne: ce qui fait Ce problème est génial pour les entrevues

1. **Small Input Size** – `n <= 100` vous permet de vous permettre une solution \(O(n \log n)\), mais vous donne également le temps de réfléchir aux structures de données.
2. ** Support multilingue** – Vous pouvez présenter Java TreeSet, Python set, C++ unordered_set + trier.
3. **Profondeur conceptuelle** – Il teste *triage*, *opération de réglage* et * logique de tranche* en un seul énoncé.
4. **Extrait prévu clair** – Un ordre strictement descendant élimine l'ambiguïté.
5. **Potentiel de variation** – Une fois que vous connaissez le noyau, vous pouvez l'étendre à -retour le sous-ensemble - au lieu de juste somme.

---

### 4.3 Les mauvaises: pièges communs

Pourquoi ça arrive ?
- Oui.
**Ne pas manipuler les duplicata** , Beaucoup résolvent le problème de k , mais oublient l'exigence distincte. Utiliser un `set` ou un `TreeSet`/`unordered_set`. Autres
**Sur-triage**= Trier l'ensemble du tableau lorsque seul le haut `k` est nécessaire.= Trier la liste *unique*, puis trancher. Autres
**Création d'un mauvais ordre** Trier explicitement avec `reverse=True` ou `Collections.reverseOrder()`. Autres
**L'indice hors limites**Le terme "k" peut être plus grand que le nombre d'éléments distincts. Utiliser `Math.min(k, set.size())` ou couper en toute sécurité. Autres
Autres **Limite de temps sur les grands ints**= Pour les nombres énormes, Python=s `int` est bien, mais soyez prudent avec le débordement C++. Utilisez `long' en C++ si nécessaire (bien que les valeurs ici <= 1e9). Autres

---

4.4 L'horrible : les choses que vous pourriez faire pour rendre le code difficile

1. **Manual Duplicate Removal** – L'écriture d'une boucle imbriquée pour filtrer les duplicatas est fastidieuse et sujette à erreur.
2. **Désorption de l'ensemble** – "Arrays.sort(nums)" suivie d'une déduplication manuelle.
3. **Verbose Variable Names** – Surcommenter les parties triviales.
4. **Ignorer les cas de bord** – Oublier le cas lorsque `k` est égal au nombre d'éléments distincts.

*Clean code* est le meilleur atout d'entrevue. Utilisez le langage-idiomes (ensembles, flux, etc.) pour le garder court.

---

4.5 La solution 3-Line Python (Pourquoi elle bat 100%)

'`python
Solution de classe:
def maxKDistinct(self, nums, k):
retour trié(set(nums), inverse=True)[:k]
«» "

- **Déduplication** – `set(nums)` supprime les duplicatas instantanément.
- **Trier** – "trié(..., inverse=True)" donne un ordre décroissant.
- **Découpage** – `[:k]` saisit les premiers éléments `k` ou tous si moins.

C'est tout ce dont vous avez besoin. Il fonctionne dans \(O(n \log n)\) et utilise la mémoire \(O(n)\). Les intervieweurs aiment la brièveté et la justesse.

---

4.6 Extension de la solution (facultative)

Si vous êtes coincé sur les questions d'entrevue, essayez ces variations:

1. **Retourner la somme au lieu des éléments** – juste 'sum(sorted(set(nums), inverse=True)[:k]'.
2. **Retourner les indices des éléments sélectionnés** – stocker une carte de la valeur à la liste d'index.
3. ** Maximiser la somme avec un nombre *minimum* d'éléments distincts** – choisir le plus petit nombre distinct qui atteint la somme.

Chaque extension renforce les mêmes idées de base.

---

4.7 Testez votre solution

'`python
assertion Solution().maxKDistinct([84,93,100,77,90], 3) == [100,93,90]
assertion Solution().maxKDistinct([84,93,100,77,93], 3) == [100,93,84]
assertion Solution().maxKDistinct([1,1,1,2,2,2], 6) == [2,1]
affermissez Solution().maxKDistinct([5], 1) == [5]
affermissez Solution().maxKDistinct([5,5,5), 2) == [5]
«» "

L'exécution de ces assertions garantit que les duplicatas, les petits «k» et les tableaux à éléments uniques sont tous traités.

---

### 4.8 SEO— Enveloppe amicale En haut

*Mots clés: * **LeetCode 3684 solution**, **maximiser la somme d'au plus k éléments distincts**, **Python LeetCode solution facile**, **Java TreeSet deduplication**, **C++ trie unordered_set**, **interview coding challenge**.

**Pourquoi ce poste est important:**
- Oui. Il vous montre une solution rapide et propre.
- Oui. Il met en évidence les pièges à éviter.
- Oui. Il est écrit dans un format que les robots recruteurs aiment : titre clair, blocs de code, listes de balles.

Si vous préparez une entrevue de codage, ajoutez-la à votre sac et pratiquez les variations. Bonne chance !

---

- Oui. 5. TL;DR (à emporter)

Mots clés Autres
- C'est quoi ?
**Python**="set → trié(inverse) → tranche"="set(nums), inverse=True"=" Autres
*Java*** *TreeSet<> (inverse) → itérer jusqu'à `k`-
**C++** → redimensionner Voir la section C++ ci-dessus

Bon codage – et bonne chance avec votre prochaine entrevue!