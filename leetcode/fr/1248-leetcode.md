---
titre: LeetCode 1248. Numéro de compte de Nice Subarrays -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1. Le Code – Trois langues

Ci-dessous, vous trouverez une solution propre, à un seul passage, O(n) qui compte le nombre de sous-arrays "nice" (exactement *k* nombres impairs).
L'idée est de transformer le problème en sous-barrages avec au plus des cotes k, puis de soustraire le nombre pour *k‐1*.
Les trois implémentations utilisent la même routine d'aide `atMostK`.

Code de la langue
C'est quoi, ça ?
**Java**
**Python**
*C++******solution.cpp**

---

## 1.1 Java

"Java
// 1248. Numéro de compte des sous-barrages de Nice
// Sliding-Window + Prefix-Sum Trick (temps O(n), espace O(1))

Importation de java.util.*;

solution de classe publique {
// Compter les sous-groupes avec exactement k nombres impairs
numéro d'entrée publiqueDeSubarrays(int[] nums, int k) {
retour àMostK(nums, k) - àMostK(nums, k - 1);
}

// Compter les sous-groupes avec au plus k nombres impairs
Int privé chezMostK(int[] nums, int k) {
si (k < 0) rendement 0; // rien ne peut satisfaire à un quota négatif
Int gauche = 0, droite = 0;
Int bizarre Cnt = 0;
= 0;
pendant que (à droite < longueur nums.) {
// ajouter l'élément courant à la fenêtre
pairCnt += nombres[droit] % 2;
// diminuer à gauche si nous dépassons le quota
pendant la période (oddCnt > k) {
impairCnt -= nombres[gauche] % 2;
gauche++;
}
// tous les sous-cours se terminant à droite et commençant n'importe où
// entre gauche et droite sont valables
total += droit - gauche + 1;
droite++;
}
le total des retours;
}
}
«» "

---

## 1.2 Python

'`python
# 1248. Numéro de comte de Nice Subarrays
# Approche de la fenêtre coulissante – temps O(n), espace O(1)

de taper l'importation Liste

Solution de classe:
Numéro DeSubarrays(soi-même, nombres: Liste[int], k: int) -> Int:
return self.at_most_k(nums, k) - self.at_most_k(nums, k - 1)

def at_most_k(self, nombres: List[int], k: int) -> Int:
si k < 0:
retour 0
gauche = 0
_cnt impair = 0
Total = 0
pour droite, val in énumérate(nums):
_cnt impair += valeur & 1 # 1 si impair, 0 si pair
alors que impair_cnt > k :
impair_cnt -= nombres[gauche] & 1
gauche += 1
Total += droite - gauche + 1
retour total
«» "

---

C++

'`cpp
// 1248. Numéro de compte des sous-barrages de Nice
// Fenêtre coulissante – temps O(n), espace O(1)

#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
Numéro int Dénomination des marchandises
retour àMostK(nums, k) - àMostK(nums, k - 1);
}

particulier:
int atMostK(const vector<int>& nums, int k) {
si (k < 0) retourner 0;
Int gauche = 0;
Int bizarre Cnt = 0;
= 0;
pour (int right = 0; right < (int)nums.size(); ++right) {
impairCnt += nombres[droit] & 1; // 1 si impair
pendant la période (oddCnt > k) {
impairCnt -= nombres[gauche] & 1;
+ + gauche;
}
total += droite - gauche + 1; // sous-arrays se terminant à droite
}
le total des retours;
}
};
«» "

Les trois implémentations ont **O(n)** complexité temporelle, scanner le tableau une fois, et utiliser seulement une poignée de variables entières – parfaitement adapté aux contraintes de LeetCode (jusqu'à 50 000 éléments).

♪ 2. Article de blog – Le bon, le mauvais, et l'atroce de compter de belles sous-images

> **Cible auprès du public:** Ingénieurs logiciels, code des personnes interrogées et recruteurs
> **Objectif:** Présentez une compréhension profonde d'un problème classique de fenêtre coulissante, tout en stimulant le référencement pour les mots-clés de recherche d'emploi.

---

## 2.1 Titre & Méta‐ Données

Valeur du champ
C'est pas vrai.
**Titre*****Des sous-images agréables : le bon, le mauvais et le mauvais – une marche à voile complète
**Meta Description**= Master LeetCode 1248 avec une solution de fenêtre coulissante O(n). Apprenez les pièges, les meilleures pratiques et comment réussir l'entrevue. Autres
**Mots-clés**=LeetCode 1248=", numéro de compte de beau subarrays=", fenêtre coulissante=", deux pointeurs=", question d'entrevue=", question de codage=", solution de Java=", solution de Python=", solution de C++=", probabilités de k exacts=", interview d'algorithme=", prép="

---

## 2.2 Introduction

> Dans les interviews en algorithme, les questions les plus redoutées sont celles qui ont l'air simples mais qui vous font monter. (en milliers de dollars)
>
> Code du leet 1248 – **Count Number of Nice Subarrays** – est ce classique. Il vous demande de trouver combien de sous-réseaux continus contiennent *exactement* `k` nombres impairs.
>
> Le truc ? Transformez le problème en une variante *préfixe sum* et résolvez-le en **O(n)** temps avec **O(1)** espace supplémentaire. Ci-dessous, nous traversons le **good**, le **bad** et le **ugly** de ce défi, avec le code en Java, Python et C++.

---

2.3 Aperçu du problème

Sens du paramètre
C'est pas vrai.
Tableau entier (`1 <= nombres[i] <= 105`) Autres
Nombre de cibles de nombres impairs (`1 <= k <= nums.length`) Autres
**Objectif**=Couvercle avec des numéros impairs exactement `k`

**Exemples**

1. `nums = [1,1,2,1,1]`, `k = 3` → `2` (`[1,1,2,1]`, `[1,2,1,1]`)
2. `nums = [2,4,6]`, `k = 1` → `0` (aucun nombre impair)
3. «nombres = [2,2,2,1,2,2,2,2,2]», `k = 2` → `16`

---

2.4 Le bon – Pourquoi l'approche de la fenêtre coulissante gagne

1. **Temps linéaire, espace supplémentaire constant**
Chaque élément est traité au plus deux fois – une fois lorsque le pointeur droit se déplace à droite, une fois lorsque le pointeur gauche se déplace à droite. Pas de tableaux supplémentaires ou de cartes de hachage.

2. **Evite le préfixe-sum + HashMap Overhead**
Une première tentative courante est de calculer les montants préfixés de -oddness et d'utiliser une carte de hachage pour compter les sommes de sous-arrachage égales à «k». Cela fonctionne mais a du temps et de l'espace O(n). La fenêtre coulissante réduit l'espace à O(1).

3. **Intuition claire**
Transformer le tableau : impair → 1, même → 0. Le problème se transforme en "sub-array sum" égale k.
Ensuite, *exactement k* = *au plus k* – *au plus (k‐1)*. Chaque appel d'aide compte combien de fenêtres contiennent au plus `k`.
Compter au plus k est un problème de fenêtre coulissante de manuel: étendre, rétrécir en dépassant "k".

4. **Aide réutilisable**
La fonction d'aide `atMostK` est agnostique de la cible. La réponse finale est une simple soustraction, évitant la duplication de code.

5. **Admissibilité au cas par cas**
Négatif `k` dans l`aide retourne automatiquement 0. Ceci gère bien `k‐1` lorsque `k = 0`.

---

## 2.5 Les mauvaises – Pièges communs et causes de bord

Pourquoi cela arrive-t-il ?
- C'est quoi ?
**Tréer chaque nombre comme sous-repère**= Décomptage lorsque la conversion impair/même n'est pas effectuée== Utiliser `num % 2` (ou `num & 1`) pour détecter les cotes==
**Au-delà d'une seule erreur dans la longueur de la fenêtre** «k=1» Autres
**L'utilisation d'un HashMap mais manquant la soustraction de "k‐1"**
**Ignorer le scénario négatif `k‐1`** Pas de problème.
**Utiliser `val % 2` à l'intérieur de la boucle intérieure à plusieurs reprises**
**En supposant que le tableau soit basé sur 0**= Indices C++ vs tranches de liste Python= Utiliser `pour droite, val in énumérate(nums):` dans Python, `pour (int right = 0; right < n; ++ right)` dans C++=

---

## 2.6 L'Ugly – Deep-Dive dans l'optimisation et les variantes

1. **Excédent total**
En Java, la somme des fenêtres peut atteindre `n * n / 2` (1,25 milliards pour n=50k). `int` est sûr en Java et C++, mais dans les langues avec des types entiers plus petits vous pourriez avoir besoin `long`.

2. **Bit-wise vs Modulo**
L'utilisation de `val & 1` (bit-wise AND) est légèrement plus rapide que `val % 2`. Les compilateurs modernes optimisent les deux, mais les microbenchmarks sur les grandes entrées montrent une augmentation de vitesse de ~5-10% pour le bit-wise.

3. **Lorsque k est très grand (k = n)**
`atMostK` ne rétrécira jamais la fenêtre; le tableau entier est une fenêtre unique. L'assistant fonctionne toujours – `total = n * (n + 1) / 2`.

4. ** Arrayage manuel du vide**
Le problème garantit `nums.longueur >= 1`, mais la programmation défensive vérifie toujours `k < 0`.

5. **Potentiel:
Un récursif -atMostK- est un itinéraire facile vers un débordement de pile pour des éléments de 50 k. Gardez la routine itérative.

6. **Stratégie de test**
Écrire des tests qui couvrent: toutes les cotes, tous les paires, `k = 1`, `k = n`, alternant les motifs impair/even.

---

2.7 Comment afficher dans une recherche de recruteur

Action Répercussions du SEO
C'est pas vrai.
**Inclure plusieurs solutions de langue**
**Utiliser des noms de fonctions clairs (`atMostK`)**= Aide les algorithmes de recherche à saisir sur la terminologie algorithmique
**Ajouter un horodatage et une analyse de complexité**
**Fournir des diagrammes visuels**
Autres **Embed code snippets dans `<pre><code>` tags**

---

## 2.8 Conclusion – Transformer la question en une pièce de portefeuille

> Il ne s'agit pas seulement d'obtenir la bonne réponse; il s'agit de montrer que vous comprenez pourquoi la réponse fonctionne, comment se garder des erreurs courantes, et comment expliquer l'algorithme de façon concise.
>
> En maîtrisant LeetCode 1248 avec l'approche de la fenêtre coulissante, vous démontrez :
> - Compétence avec des techniques à deux points
> - Capacité de transformer les problèmes en sous-problèmes plus simples
> - Utilisation efficace du temps et de l'espace
> - Code propre et durable sur Java, Python et C++

> Déployez cet article sur votre blog, LinkedIn ou Medium avec les mots-clés ci-dessus, et vous attirerez les recruteurs qui sont activement à la recherche de candidats prêts à l'entrevue. Bonne chance – et rappelez-vous : chaque bug que vous évitez est un pas plus près de cet appel d'entrevue suivant.

---

2.9 Liste de contrôle rapide pour l'entrevue

- [ ] **Lisez attentivement l'énoncé du problème** – notez que `k` est exactement.
- [ ] **Convertissez les cotes à 1, evens à 0** – simple astuce modulo ou bit-wise.
- [ ] **Mise en œuvre `atMostK` fenêtre coulissante** – agrandir → rétrécir → ajouter `right-left+1`.
- [ ] **Retour `atMostK(k) - atMostK(k-1)`** – s'occupe de tous les cas de bord automatiquement.
- [ ] **Test sur les exemples fournis + cas de bord** – les trois langues doivent passer.

Joyeux codage, et que votre prochaine interview soit un "nic"!