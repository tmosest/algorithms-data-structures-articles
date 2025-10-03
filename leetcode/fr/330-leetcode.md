---
titre: LeetCode 330. Tableau de correspondance -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 330. Patching Array – Une entrevue complète‐ Guide prêt
implémentation C++ + un billet de blog profond*

---

### TL;DR

Langue
- C'est quoi ?
Utiliser un `long` pour éviter le débordement; patching avide
**Python** La même logique – `int` n'est pas liée
**C++**=O(log n + m)==Arithmétique 64 bits (`long') Autres

> **Ce que nous couvrirons* *
> 1. Énoncé de problème et exemples
> 2. Greedy perspicacité + preuve formelle
> 3. Algorithme étape par étape
> 4. Cas de bord et pièges
> 5. Analyse temps/espace
> 6. Extraits de code complet (Java, Python, C++)
> 7. Le bon, le mauvais, l'article de blog laid

---

- Oui. 1. Exposé des problèmes

> **Don**:
> * `nums`: une gamme ** triée** d'entiers positifs (longueur ≤ 1000).
> * `n`: un entier (1 ≤ n ≤ 231 − 1).
> **Tâche**: Ajouter les nouveaux nombres (pièces) **fewest** à `nums` de sorte que chaque entier dans `[1, n]` puisse être représenté comme une somme de **quelques** éléments du tableau *augmenté*.
> **Retour** le nombre minimal de patchs.

> **Exemples**
> 1. `nums = [1, 3]`, `n = 6` → réponse = 1 (patch `2`).
> 2. `nums = [1, 5, 10]`, `n = 20` → réponse = 2 (patch `2, 4`).
> 3. `nums = [1, 2, 2]`, `n = 5` → réponse = 0 (déjà toutes les sommes).

---

- Oui. 2. Pourquoi l'avidité fonctionne

Nous maintenons une variable `miss` qui représente le plus petit entier **not** actuellement représenté par le tableau que nous avons vu jusqu'à présent (y compris les patchs que nous avons ajouté). Dans un premier temps, "miss = 1".

- Si l'élément suivant dans `nums` (`nums[i]`) est **. miss**, cela signifie que nous pouvons étendre la plage de représentation:
`miss += nombres[i]` (tous les montants du nouveau "miss - 1" deviennent accessibles).
- Sinon, nous *doit* patch `miss` lui-même.
Ajouter `miss` double la portée accessible: `miss += miss`.

Pourquoi le patching est-il optimal?
Parce que tout nombre < `miss` est déjà représentatif, et tout nombre ≥ `miss` mais < `miss + nums[i]` ne peut être rendu accessible qu'en ajoutant un nombre ≤ "miss". Le plus petit de ces nombres est exactement "miss". Ainsi, le patching avidement "miss" est le seul moyen de combler le fossé avec un seul patch.

Le processus s'arrête une fois `miss > n`. À ce stade, chaque entier jusqu'à `n` est représentatif.

---

- Oui. 3. Algorithme (Pseudo-code)

«» "
minPatches(nombres, n):
patchs = 0
i = 0
Miss = 1 // plus petite somme non représentative

pendant que l'erreur <= n:
si i < len(nums) et nums[i] <= manque:
Miss += nombres[i]
i += 1
Sinon:
// Patch miss
Miss += Miss
patchs += 1

retour des correctifs
«» "

*Important*: Utilisez des entiers 64 bits (long'/long') pour `miss` car `miss` peut doubler plusieurs fois et dépasser les limites de 32 bits.

---

- Oui. 4. Edge Cases & Gotchas

Autres Décision Pourquoi ça compte ?
- - - - - - - - - - Non.
"nums" contient Si le tableau commence à 1, nous étendons immédiatement la portée. Autres
"nums[i]` > "miss"" Gap – nous avons besoin d'un patch. Autres
`n` trÃ ̈s grande (`=231 - 1`)="miss` peut dÃ©passer 32 bits=" Utilisez 64 bits entiers. Autres
"nums" couvre déjà toutes les sommes. Autres

---

- Oui. 5. Analyse de la complexité

Java / Python / C++
-- -- -- -- -- -- -- -- --
Temps **O(log n + m)** (chaque patch au plus double `miss`, donc au plus `log2 n` patchs; chaque élément de tableau traité une fois). Autres
Espace **O(1)** (seulement quelques variables). Autres

---

- Oui. 6. Code complet

### Java

"Java
solution de classe publique {
Int minPatches(int[] nums, int n) {
les correctifs int = 0;
i = 0;
long miss = 1; // utiliser longtemps pour éviter le débordement

pendant que (miss <= n) {
si (i < nombres.longueur && nombres[i] <= manque) {
mademoiselle += nombres[i++];
} autre {
miss += miss; // patch miss
patchs++;
}
}
les correctifs de retour;
}
}
«» "

Python

'`python
Solution de classe:
def minPatches(self, nombres: List[int], n: int) -> Int:
patchs = 0
i = 0
miss = 1 # Les entrées de Python sont débordées

pendant que l'erreur <= n:
si i < len(nums) et nums[i] <= manque:
Miss += nombres[i]
i += 1
Sinon:
Miss += Miss
patchs += 1
retour des correctifs
«» "

C++

'`cpp
solution de classe {
public:
Int minPatches(vector<int>& nums, int n) {
les correctifs int = 0, i = 0;
long long manque = 1; // 64-bit pour éviter le débordement

pendant que (miss <= n) {
si (i < nums.size() && nums[i] <= miss) {
mademoiselle += nombres[i++];
} autre {
miss += miss; // patch miss
+ palettes;
}
}
les correctifs de retour;
}
};
«» "

---

- Oui. 7. Article de blog – Le bon, le mauvais et le mauvais

> **Titre**: *Arrayage – La feuille d'entrevue ultime (bon, mauvais, et ingly)*
> **Meta‐Description**: - Apprenez à cracher le problème LeetCodeS Patching Array en 5 minutes. Comprendre l'algorithme avide, les cas de bord, et se préparer pour votre prochain entretien d'emploi. (en milliers de dollars)

7.1 Les bonnes
* **Simplicité** – Une boucle, deux branches, arithmétique 64 bits.
* **Optimalité** – Une stratégie avide éprouvée garantit le nombre minimal de patchs.
* **Speed** – O(log n) patchs; fonctionne en millisecondes pour les contraintes maximales.

7.2 Les mauvais
* **Piège de sortie** – Dans les langues avec des limites 32 bits (`int` en Java/C++), `miss` peut déborder avant de le réaliser.
* **Musreading the problem** – Beaucoup de candidats pensent qu'il manque le plus petit nombre, mais oublient de doubler "miss" après le patching.
* **Cas d'Edge points aveugles** – Oublier que les "nums" pourraient déjà couvrir toute la gamme ou que `n` pourrait être 1.

### 7.3 L'horrible
* **Proof complexe** – Certaines solutions tentent un DP ou une récursion qui souffle dans le temps et l'espace.
* ** Variables inutiles** – La sur-ingénierie de la solution (par exemple, la construction d'un ensemble de toutes les sommes accessibles) conduit à TLE.
* **Type de données Wong** – L'utilisation de `int` pour `miss` dans Java/C++ donne lieu à des bogues cachés qui ne couvrent que les grandes `n`.

7.4 Comment faire des ongles Dans une interview

1. ** Expliquez l'intuition d'abord** – Parlez de `miss` et pourquoi le patching est optimal.
2. **Afficher l'algorithme sur papier** – Écrire le pseudo-code, puis le mapper à la langue choisie.
3. **Débordement d'adresse** – Mention en utilisant `long`/`long` et pourquoi il importe.
4. **Run à travers les cas de bord** – `n=1`, `nums=[1]`, `nums=[2]`, `n` énorme.
5. **Complexité** – 1-2 phrases sur le temps/l'espace.

Liste de contrôle du référencement 7.5

Pourquoi ça compte ?
C'est-à-dire
**Mot-clé**==Patching array=== Inclus dans le titre, les en-têtes et dans tout le texte. Autres
**Déscription de la Méta**= Courte, convaincante = Fourni en haut de l'article. Autres
**En-têtes (H1, H2, H3)**= Améliore la lisibilité & SEO== Hiérarchie structurée avec titres descriptifs. Autres
Chaque langue est enveloppée dans des clôtures appropriées (``java`, etc.). Autres
**Image alt text**= Si des images ont été ajoutées, utilisez un texte alt descriptif comme le diagramme de patchage de la graisse. Autres
**Liens internes**=Conserve les utilisateurs sur le site=Suggested="Related: LeetCode 1527="Top interview problems. Autres
**Références externes**= Autorité== Liens vers LeetCode et les postes de discussion. Autres
**Paragraphes lisibles** Autres

7.6 A emporter

Le problème **Patching Array** est un défi avide classique qui teste la capacité d'un candidat à penser à la couverture de portée et à la croissance progressive. La maîtrise vous donne :

* Confiance dans les stratégies gourmandes.
* Un bon sujet d'entretien.
* Un extrait de code prêt à travailler qui fonctionne en Java, Python et C++.

---

**Codage heureux – et que vos correctifs soient toujours minimes! * *