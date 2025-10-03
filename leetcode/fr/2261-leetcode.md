---
titre: LeetCode 2261. K Éléments divisibles Subarrays -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

> **2261. K Éléments divisibles Subarrays**
> **Difficulté:** Moyenne
> **Signature (Java):**
> `public int countDistinct(int[] nums, int k, int p) "

Étant donné un tableau entier `nums`, un entier `k` et un diviseur `p`, compter **distinct** subarrays contigus qui contiennent **à la plupart des éléments `k` divisibles par `p`**.

Deux sous-barrages sont distincts si leurs séquences de valeurs sont différentes, pas seulement leurs positions.

> **Constraints**
> * `1 ≤ longueur nominale ≤ 200`
> * `1 ≤ nombres[i] ≤ 200`
> * `1 ≤ k ≤ longueur nums "
> * `1 ≤ p ≤ 200`

Parce que `n` est minuscule (= 200) un algorithme `O(n2)` est assez rapide pour tous les cas de test LeetCode.
Ci-dessous nous donnons **trois solutions linguistiques** faciles à comprendre et prêtes pour une entrevue de codage.

---

- Oui. 2. Mise en œuvre des références

Code de la langue
- C'est quoi ?
*Java * Brute-force + `HashSet` des tuples *
*Python * Brute-force + "set" (tuple + facultatif Rabin-Karp)
*C++ * Brute-force + `unordered_set` + rolling-hash pour la vitesse

Autres Tous les trois codes utilisent le même «generate‐all‐subarrays → check → add to set» pattern, mais le choix de la structure des données montre les compromis que les intervieweurs aiment discuter.

---

#### 1.1 Java – Version Hash‐Set (La plupart des commentaires)

"Java
Importation de java.util.*;

solution de classe publique {
***
* Compte des sous-arraies distinctes qui contiennent au plus des éléments k divisibles par p.
*/
nombre d'entrées publiquesDistinct(int[] nombres, int k, int p) {
Set<String> vu = nouveau HashSet<>();
int n = longueur nums;

// O(n^2) – générer chaque sous-profil une fois
pour (int start = 0; start < n; ++start) {
int divisible Cnt = 0;

pour (int fin = début; fin < n; ++ fin) {
si (nums[end] % p == 0) {
divisible Cnt++;
}
Si (divisibleCnt > k) rupture; // pas besoin d'étendre davantage

// Convertir la tranche en une chaîne canonique
StringBuilder sb = nouveau StringBuilder();
pour (int i = début; i <= fin; ++i) {
sb.append(nums[i]).append(','); // virgule maintient les limites claires
}
voir.add(sb.toString()); // définir des garanties unicité
}
}
retour vu.size();
}
}
«» "

**Pourquoi c'est "Good"* *
* Utilise uniquement une bibliothèque standard (`HashSet`).
* Linéaire dans le nombre de subarrays (`n(n+1)/2`).
* Pas de hachage délicat – facile à expliquer dans une entrevue.

**Potentiel:
* La représentation de la chaîne n'est pas optimale pour la mémoire; elle stocke jusqu'à 200 × 200 caractères de 40 k – fin pour LeetCode, mais gaspillé dans des scénarios de mémoire serrée.
* La boucle intérieure `pour` qui reconstruit le `StringBuilder` sur chaque sous-arraché peut être un peu lente en Java.

---

#### 1.2 Python – Set + Facultatif Rabin‐Karp

'`python
def countDistinct(nums: list[int], k: int, p: int) -> Int:
"""
Code du leet 2261 – Mise en œuvre de Python.
Utilise un ensemble simple de tuples (rapide pour n ≤ 200) et
un hachage roulant Rabin–Karp optionnel à des fins de démonstration.
"""
n = len(nums)
distinct = set()

N° 1 Jeu de tuple simple (clair, assez rapide pour n ≤ 200)
pour i dans la plage(n):
cnt = 0
pour j dans la plage(i, n):
si nombres[j] % p == 0:
cnt += 1
si cnt > k:
pause
distinct.add(tuple(nums[i:j+1]))

# Décommenter le bloc suivant pour voir une variante de rolling-hash.
"""
# 2-- Karp style rolling hash (montre comment éviter la création de tuple)
MOD = 10**9 + 7
BASE = 257
puissance = [1] * (n+1)
pour i dans la plage(1, n+1):
puissance[i] = (puissance[i-1] * BASE) % MOD

pour i dans la plage(n):
h = 0
cnt = 0
pour j dans la plage(i, n):
si nombres[j] % p == 0:
cnt += 1
si cnt > k:
pause
h = (h * BASE + nombres[j]) % MOD
distinct.add(h)
"""

retour len(distinct)
«» "

> **Ce que fait le bloc facultatif :**
> * Garde un seul entier hasch par sous-array, donc la mémoire est `O(n2)` entiers au lieu de tuples.
> * Fonctionne de la même façon pour l'entrevue – vous pouvez mentionner que c'est un tour de Rabin–Karp.

---

### 1.3 C++ – Non commandé- Set + Hash roulant

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nt countDistinct(vector<int>& nums, int k, int p) {
int n = nombres.size();
unordered_set<long> vu; // stocke le hash de subarray
longue MOD = 1'000'000'007LL; // une grande prime
Const longue BASE = 257; // > max(nums[i])

// Pouvoirs précalculateurs de BASE
vecteur <long long> pow(BASE * 1LL, 1);
pour (int i = 1; i < pow.size(); ++i) {
pow[i] = (pow[i-1] * BASE) % MOD;
}

pour (int i = 0; i < n; ++i) {
long h = 0;
cnt = 0;
pour (int j = i; j < n; ++j) {
si (nums[j] % p == 0) cnt++;
en cas de rupture (cnt > k);
h = (h * BASE + nombres[j]) % MOD;
voir.insérer(h);
}
}
retour vu.size();
}
};
«» "

> **Pourquoi cela fonctionne:**
> * Chaque sous-aire est cartographiée à une valeur de hachage unique (probabilité de collision - 1/`MOD`).
> * Parce que `n ≤ 200`, un jeu simple de haches est suffisant – pas besoin d'un suffixe complet.

---

- Oui. 2. L'échange – Bonne – Mauvais – Ugly

Aspect (Interview-Amiendly)
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Complexité**=Temps `O(n2)`, espace `O(n2)` – parfaitement acceptable pour le temps `n=200`.==Temps `O(n2)`, espace `O(n2)` – même mais avec une lourde structure de données.==Temps `O(n)`, espace `O(n)` avec des tableaux suffixes – overkill pour ce problème. Autres
**Readability** Même chose, plus un petit snipet de rolling-hash. L'implémentation de Trie – nécessite beaucoup de code et de nombreux tableaux. Autres
**Mémorie**="HashSet<tuple>" – utilise environ quelques KB. Même – mais les tuples Python ajoutent des frais généraux. Un peu plus efficace que Python. Autres
**Risque de collision**. Aucun – tuples uniques. Petit risque avec le hachage roulant, atténué par une grande prime. Autres
**Valeur de l'interview**** Affiche que vous pouvez raisonner sur *subarray* generation + *set* utilisation. Ajoute un peu de "Hash-engineering" flair. Montre que vous pouvez implémenter une solution basée sur le hash et comprendre les pièges. Autres
**Pitfalls** La création de tuple de Python est lourde mais fine. En C++, oublier d'utiliser `réserve` peut causer des frais de rehash. Autres

> **Ligne de bottom:**
> La solution simple `HashSet` / `tuple` est ce que vous voulez écrire dans une interview – elle est rapide, propre et facile à expliquer.
> Si l'intervieweur vous demande de *optimiser* la solution, parlez de la façon dont vous pourriez remplacer le tuple par un seul hachage roulant 64 bits et pourquoi cela serait encore correct.
> Enfin, vous pouvez mentionner l'approche de *suffix-array* comme un facteur de "wow-factor" – vous pouvez dire, "I"ve a étudié l'algorithme du temps linéaire pour compter des sous-chaînes distinctes; je pourrais le brancher ici si les contraintes étaient plus grandes. (en milliers de dollars)

---

- Oui. 3. Article sur le blog des amis du SEO

> **Titre (H1) :**
> **K Subarrays d'éléments divisibles – Un LeetCode 2261 Masterclass (Java, Python, C++)* *

> **Méta-description :* *
> Apprendre à résoudre le LeetCode 2261 – K Divisible Elements Subarrays – avec le code Java, Python et C++ propre. Comprendre le hasch-set, le trie, Rabin-Karp, les astuces suffixes. (en milliers de dollars)

> **Mots clés:**
> LeetCode 2261, K Éléments divisibles Subarrays, subarrays distincts, interview d'algorithme, hachage, hachage roulant, Rabin‐Karp, tableau suffixe, solution O(n2), C++ unordered_set, Java HashSet, jeu de tuples Python.

---

3.1 Introduction

> **(H2) Pourquoi LeetCode 2261 est une question d'entrevue classique**
> *Le calcul des sous-réseaux avec contraintes est un élément essentiel des entrevues sur les structures de données. LeetCode 2261 est un mélange parfait de l'utilisation du réseau traversal + set.

---

3.2 Ventilation des problèmes

> **(H2) Déclaration formelle du problème* *
> * Expliquez la définition de "divisible par p" et "au plus k" en mots simples. *
> *Illustrez avec un exemple de tableau de 4 éléments pour montrer le concept de k.c.v.c. exactement k.c. *

---

### 3.3 Stratégie de solution – L'approche Brute-Force + Set

> **(H2) Guide étape par étape**
> 1. **Générer tous les sous-réseaux** – boucles imbriquées (« O(n2) ».
> 2. **Couvercle des éléments divisibles** tout en s'étendant.
> 3. **Ajouter à un ensemble** – assure l'unicité.
> 4. Retournez la taille de l'ensemble.

> *Afficher le pseudocode sur la page et lier chaque extrait de langue. *

---

3.4 Démarches linguistiques spécifiques

En haut de la page
- C'est quoi ?
*Java *HashSet <String> + "StringBuilder". (Insérer le code Java)
Ensemble de tuples + option Rabin-Karp.
(Insérer le code C++)

> **(H3) Explication de la fuite de roulement* *
> Au lieu de stocker toute la tranche, nous construisons un entier 64 bits en utilisant une base > 200. Les collisions sont astronomiquement improbables parce que nous modions avec 1 000 000 007. (en milliers de dollars)

---

3.5 Techniques avancées – Si les contraintes étaient plus grandes

> **(H2) Hash roulant vs. Tuple* *
> Dire pourquoi un hachage 64 bits est suffisant et mentionner la probabilité de collision. Insistez sur le fait que c'est un tour de Rabin-Karp classique. (en milliers de dollars)

> **(H2) Solution de suffixe-image**
> Introduisez l'algorithme linéaire du temps pour compter des sous-chaînes distinctes (Karkkainen-Sanders).
> Description succincte des étapes : build SA → LCP → formule → s'adapter à l'état le plus k. (en milliers de dollars)

> * Terminer avec un teaser:* * J'ai également implémenté un tri complet pour ce problème, mais il est inutile à moins que vous êtes s'attaquer 105 éléments. (en milliers de dollars)

---

#### 3.6 Résumé et prise‐ Loin

> **(H2) Liste de contrôle à emporter* *
> * Écrivez d'abord la solution `HashSet` simple.
> * Soyez prêt à discuter du remplacement du hachage sans collision.
> * Mention suffix tableau comme une optimisation théorique.
> * Pratiquez le code dans les trois langues; LeetCode accepte n'importe lequel.

> **Appel à l'action (H3):**
> Essayez le code sur LeetCode vous-même. Laissez un commentaire si vous voulez le suffixe-array ou aidez à optimiser pour les ensembles de données plus grands! (en milliers de dollars)

---

- Oui. 4. Conseils finaux pour l'entrevue

1. ** Commencez par la solution la plus simple. **
2. ** Expliquer clairement la logique de base :** Nous énumérons chaque sous-réseau et utilisons un "set" pour déduper automatiquement. (en milliers de dollars)
3. **Si l'on demande d'optimiser, discutez de l'approche du hachage roulant et pourquoi il donne toujours une réponse sans collision pour les limites de LeetCode. **
4. **Mentionner l'approche suffixe-array seulement si l'intervieweur est à la recherche d'un facteur de «wow»** – ne pas l'appliquer réellement.
5. **Toujours tester votre code sur une petite entrée personnalisée** (par exemple, `nums = [2, 3, 4, 6]`, `k=1`, `p=2`) – il montre que vous êtes prudent.

---

- Oui. 5. Clôture

Vous avez maintenant **prêt à soumettre** Le code Java, Python et C++ pour LeetCode 2261, ainsi qu'une compréhension claire des compromis « bons – mauvais » qui font ressortir un candidat.

Bon codage ! C'est ce qu'il a dit.

---

> **Joyeux piratage, et que vos intervieweurs aiment la solution de hachage autant que nous l'aimons. **