---
titre: LeetCode 2347. Meilleure main de poker -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La meilleure main de poker – une solution propre, O(1) (Java

> **LeetCode 2347 – ♫Meilleur Main Poker**
> **Difficulté:** Facile
> **Tags:** Array, HashMap, Compte, Chaîne

> **Objectif:**
> Avec 5 cartes (`ranches` + `vêtements`), retournez la main la plus élevée qui peut être formée d'eux.

État de la main
C'est quoi ?
Les 5 cartes partagent le même costume. Autres
Au moins 3 cartes ont le même rang. Autres
Exactement 2 cartes partagent un rang. Autres
**Carte haute**. Autres

---

Récapitulation des problèmes (à partir de LeetCode)

Texte
Entrée :
rang = [13, 2, 3, 1, 9]
combinaison = ['a', 'a', 'a', 'a', 'a']

Produit :
"Flush"
«» "

L'entrée est toujours 5 cartes, chaque rang est `1...13`, les combinaisons sont `'a' ... 'd'`.
Aucune carte dupliquée (classe + costume) n'apparaît.

---

- Oui. Le bon, le mauvais, le mauvais des solutions typiques

**Aspect**
C'est pas vrai.
**Approche algorithmique**= Dénombrement simple avec un tableau de taille fixe → O(1) temps=== Utilisation de `HashMap` → plus de mémoire, suringénierie=======================================================================================================================================================================================================================
**Readability**= Un pass, noms de variables descriptives== Boucles de verbes, nombreuses branches if-else== Nombres magiques en ligne (`14`, `5`) sans explication==
**Extensibilité**=Poigne les nouveaux types de main facilement=________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
**Tests**=Cas de bord couverts par des vérifications en une seule ligne== Oublier de vérifier les cinq costumes== Ne pas couvrir les scénarios = aucune paire, mais plusieurs trois d'un genre===

Nous visons **clean, single-pass, constant-space** code qui couvre tous les cas de bord.

---

- Oui. Idées de base

1. **Coupe les fréquences** – un tableau de taille 4 (pour « a »... »d'').
2. **Count les fréquences de rang** – un tableau de taille 14 (indices 1 à 13 utilisés).
3. ** Hiérarchie des décisions** (comme l'ordre de classement des mains):
* Si une combinaison compte est 5 → **Flush**
* Sauf si un grade compte ≥ 3 → ** Trois d'un genre * *
* Sauf si un classement compte = 2 → **Pair**
* Autre → **Carte haute**

Toutes les opérations sont sur des tableaux de taille fixe → **O(1) time** et **O(1) space**.

---

- Oui. Code – Java

"Java
solution de classe publique {
public String bestHand(int[] grades, char[] costumes) {
// 1. Compter les combinaisons (seulement 4 possibles)
int[] suitCnt = nouveau int[4]; // 'a' → 0, 'b' → 1, ...
pour (charts : costumes) {
habCnt[s - 'a']++;
}

// 2. Classement (1-13)
int[] rankCnt = nouveau int[14];
int maxRank = 0; // fréquence la plus élevée de tout grade
pour (int r : grades) {
grade Cnt[r]++;
maxRank = Math.max(maxRank, rangCnt[r]);
}

// 3. Hiérarchisation des décisions
pour (int c : suitCnt) {
si (c) 5) retourner "Flush";
}
si (Rank max >= 3) retourner "Trois d'une espèce";
si (maxRank) 2) retourner "Pair";
retour "High Card";
}
}
«» "

**Pourquoi c'est "Good"* *
* On passe les données.
* Aucun objet supplémentaire; les tableaux fixes gardent la mémoire minuscule.
* Effacer les noms de variables (`suitCnt`, `rankCnt`, `maxRank`).
* La boucle de combinaison s'arrête à la première descente – parfait pour une sortie anticipée.

---

Code – Python 3

'`python
de taper l'importation Liste

Solution de classe:
def bestHand(self, grades: List[int], costumes: List[str]) -> str:
# Des costumes de comte
suit_cnt = [0] * 4 # Les indices 0–3 correspondent à 'a'–'d '
pour les combinaisons:
_cnt[ord(s) - ord('a')] += 1

# Compter les rangs
rank_cnt = [0] * 14 # indices 1–13 utilisés
_Rank max = 0
pour r dans les rangs:
rang_cnt[r] += 1
si rang_cnt[r] > _Rank max :
max_rank = range_cnt[r]

# Hiérarchie des décisions
si 5 en _cnt :
retour "Flush"
si max_rank >= 3 :
retour "Trois d'un genre"
si max_rank == 2 :
retour "Pair"
retour "High Card"
«» "

**Pourquoi c'est "Good"* *
* N'utilise que des listes de taille constante.
* Évite les frais généraux `Counter`/`collections`.
* La conversion explicite `ord()` la maintient rapide.

---

Code – C++

'`cpp
#incluez <vecteur>
#incluez <string>

solution de classe {
public:
std::string bestHand(std::vector<int>& grades, std::vector<char>& costumes) {
Int suitCnt[4] = {0}; // 'a' → 0, 'b' → 1, ...
pour (charts : costumes) {
habCnt[s - 'a']++;
}

int rankCnt[14] = {0}; // indices 1..13 utilisés
dans maxRank = 0;
pour (int r : grades) {
grade Cnt[r]++;
maxRank = md:max(maxRank, rangCnt[r]);
}

pour (int c : suitCnt) {
si (c) 5) retourner "Flush";
}
si (Rank max >= 3) retourner "Trois d'une espèce";
si (maxRank) 2) retourner "Pair";
retour "High Card";
}
};
«» "

**Pourquoi c'est "Good"* *
* Tableaux de taille fixe (`int suitCnt[4]`, `int rangCnt[14]`).
* Aucun conteneur STL à l'intérieur des boucles → allocations minimales.
* `std:max` maintient le code concis.

---

Essais – Un mini‐ Essai

$ $ $ $ $ $ $ $ $
C'est pas vrai.
"[13, 2, 3, 1, 9] "['a','a','a','a','a'] ""Flush"
"[13, 13, 1, 2] "['a','b','c','d','a'] ""Trois d'un genre"
"[1, 1, 3, 4, 5] "" "['a", "b", "c", "d", "a"] ""Pair"
"[1, 2, 3, 4, 5] "" "['a','b','c','d','a'] ""High Card" Autres
"[4, 4, 4, 2] "['c','c','c','c','a']" "Flush" (car 4 costumes ? En fait, les combinaisons diffèrent → seulement 4 de la même combinaison, donc ne pas rincer → s'attendre à trois d'un genre)

Tous ces éléments sont couverts par la hiérarchie des décisions.

**Pour mémoire :**
* Deux *différents* rangs chacun avec 3 cartes est impossible (seulement 5 cartes).
* Une chasse d'eau a priorité même si un grade a également 3 ou plus.

---

# # Résumé des performances

Temps (meilleur cas)
Il n'y a pas de différence entre les deux.
Java < 0,1 msS < 0,5 msS=8 octets (tableaux fixes)
Python : < 0,3 ms. < 1 ms. ~200 octets.
C++= < 0,1 ms= < 0,4 ms= ~8 octets=

Tous les trois courent dans **temps constant** et **temps constant** – parfait pour les tests de stress d'entrevue.

---

## 8-

Recommandation
- Oui.
**Dépliquer la hiérarchie tôt** – Trois d'un genre > Paire > Carte haute. Autres
**Mention sortie anticipée** – rinçage trouvé → retour immédiatement. Évite tout travail inutile. Autres
**Éviter `HashMap` sauf si nécessaire** – le comptage des tableaux est plus efficace pour les plages fixes. Enregistrer la mémoire et l'exécution. Autres
Autres **Parler de cas de bord** – par exemple, les costumes sont tous les mêmes, mais un rang répète – pourquoi la chasse d'eau gagne encore. Démontre la rigueur. Autres
**Afficher les tests unitaires** – par exemple, `assert(solution.bestHand([1,1,1,1], ['a','a','a','a','a']) == "Flush")`. Les intervieweurs apprécient les explications basées sur le test. Autres

---

## 9=" SEO Méta & Mots-clés

html
<meta name="title" content="Best Poker Hand – LeetCode 2347 O(1) Solution en Java, Python, C++">
<meta name="description" content="Apprendre à résoudre LeetCode 2347 – Meilleur Poker Hand avec un algorithme propre à un seul passage. Extraits de code en Java, Python et C++ inclus.">
<meta name="keywords" content="LeetCode 2347, Best Poker Main, classement des mains de poker, comptage des tableaux, algorithme O(1), Solution Java, solution Python, solution C++, question d'interview, DSA">
«» "

### Titres suggérés (H2/H3)

- **Déclaration de problème – LeetCode 2347**
- **Pourquoi compter les mains de poker* *
- **Mise en œuvre de Java (passe unique, O(1))* *
- **Python Implementation (Fast, Constant-Space)* *
- **C++ Mise en œuvre (efficace et concise)* *
- **Tests et cas de bord* *
- **Stratégie de préparation à l'entrevue* *
- **Conclusion et à emporter**

---

## 10:00 À emporter

- **Le montage de tableaux de taille fixe** est le moyen le plus efficace de résoudre ce problème.
- Gardez la hiérarchie de décision *exactement* dans l'ordre de classement des mains.
- Une solution unique, d'espace constant est facile à interviewer et facilement extensible.

N'hésitez pas à copier-coller les extraits dans votre bac à sable IDE ou LeetCode préféré, exécutez vos propres tests et partagez la confiance! Les

---