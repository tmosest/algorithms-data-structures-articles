---
titre: LeetCode 2406. Diviser les intervalles dans le nombre minimum de groupes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Nombre minimum de groupes – 2406 (Code Leet)* *

Langue Heure Espace
[En milliers de dollars des États-Unis]
*Java * * O(n log n) * O(n) * Autres
*Python * * O(n log n) * O(n) Autres
*C++** Exclusivité Autres

> **Problème**:
> Compte tenu des «intervalles[i] = [lefti, righti]» (inclus), diviser tous les intervalles en les groupes les moins nombreux possibles de sorte qu'aucun intervalle ne se chevauche dans le même groupe. Retourner le nombre minimum de groupes.

---

Pourquoi ce problème est-il un problème ?

1. ** Concepts de base** : tri, technique à deux points, programmation par intervalles gourmands, ligne de balayage.
2. **Langue Agnostique**: Solvable en O(n log n) en Java, Python ou C++.
3. **Twist d'entrevue commune**: L'intervalle *points de fin sont inclus*, de sorte que `[1,5]` et `[5,8]` ** Le chevauchement.
4. **Profondeur du test**: Grandes entrées (`n ≤ 105`) – vous force à penser au temps et à la mémoire.

> * Si vous vous posez cette question, les recruteurs diront : "Vous comprenez l'avidité + le tri – parfait pour la conception de systèmes et l'interview backend !

---

## Comment le code fonctionne--

Aspect du bien
- C'est quoi ?
**Approach**=Two-pointer balai line, O(n log n)== Oubliez la règle inclusive → mauvaise réponse sur les cas limites==Utilisez une file de priorité/pap pour suivre les temps de fin – fonctionne mais plus lourd (O(n log n) + mémoire supplémentaire)===
**Complexité**= Rapide et efficace en mémoire== O(n2) si vous comparez chaque paire== O(n log n) mais surkill pour ce problème==
**Readability**= Séparation claire des starts/ends== Mises à jour mixtes en place → difficile à suivre== Astuces obfusquées de lambda===

Bonne: Balayage à deux points

1. **Trier** toutes les heures de début et toutes les heures de fin.
2. Passez par les départs.
3. Si le démarrage courant est *après* la fin la plus ancienne (`start > end[endPtr]`), l'intervalle peut réutiliser un groupe → déplacer `endPtr`.
4. Sinon, nous avons besoin d'un nouveau groupe → incrément "groupes".

C'est essentiellement la même idée que le problème classique des salles de réunion II, mais plus simple parce que nous n'avons besoin que des intervalles maximums.

Mauvaise : Variante du poids/de l'arbre

"Java
PrioritéQueue<entier> pq = nouvelle prioritéQueue<>();
pour (int[] intervalle : intervalles) {
pendant que (!pq.isEmpty() && pq.peek() < intervalle[0]) pq.poll();
pq.offre(intervalle[1]);
}
retour pq.size();
«» "

- Fonctionne, mais O(n log n) *et* un tas supplémentaire → frais généraux inutiles.

#### ─ Ugly: Balayage excessif

- Tri, puis balayage avec un compteur qui est incrémenté/décrémenté à la volée, mais avec des contrôles de limites en désordre.
- Difficile à déboguer et à entretenir.

---

Code complet (trois langues)

> Les trois implémentations suivent la même logique :
> *Trier commence et se termine → balayage à deux points → compter les intervalles maximum simultanés. *

---

Python 3

'`python
de taper l'importation Liste

Solution de classe:
def minGroupes(eux-mêmes, intervalles: Liste[Liste[int]]) -> Int:
"""
Nombre minimal de groupes pour les intervalles de non-overlaping.

Temps : O(n log n) – tri
Espace : O(n) – tableaux auxiliaires
"""
début = trié(i[0] pour i par intervalles)
fin = trié(i[1] pour i par intervalles)

end_ptr = 0 # points à l'intervalle de fin le plus précoce
groupes = 0

pour s en début:
# Si l'intervalle commence après la première fin,
# nous pouvons réutiliser ce groupe (déplacer end_ptr).
si s > termine[end_ptr] :
end_ptr += 1
Sinon:
Besoin d'un nouveau groupe.
groupes += 1

Groupes de retour
«» "

---

### Java (Java 17+)

"Java
Importer java.util. Les tableaux;

solution de classe {
public int minGroupes(int[][] intervalles) {
int n = intervalles de longueur;
int[] starts = nouveau int[n];
int[] fins = nouvelle int[n];

pour (int i = 0; i < n; i++) {
début[i] = intervalles[i][0];
fin[i] = intervalles[i][1];
}

Arrays.sort(débuts);
Tableau 3.

int endPtr = 0, groupes = 0;
pour (int s : commence) {
si (s > fin[endPtr]) { // intervalle peut réutiliser un groupe
fin Ptr++;
} autre { // besoin d'un nouveau groupe
groupes++;
}
}
les groupes de retour;
}
}
«» "

---

### C++ (C++17)

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
int minGroupes(std::vector<std::vector<int>>& intervalles) {
int n = intervalles.size();
md::vector<int> starts(n), fin(n);
pour (int i = 0; i < n; ++i) {
début[i] = intervalles[i][0];
fin[i] = intervalles[i][1];
}
à:sort(starts.begin(), starts.end());
std:sort(ends.begin(), find.end());

int endPtr = 0, groupes = 0;
pour (int s : commence) {
si (s > fin[endPtr]) // réutiliser un groupe
++endPtr;
Autre
++ groupes; // nouveau groupe nécessaire
}
les groupes de retour;
}
};
«» "

> **Astuce**: Pour **C++**, préférez `vector<int>` par `vector<vector<int>>` lorsque l'entrée est lue une fois.

---

## ♫ Blog-Style Write-Up (SEO optimisé)

---

# Diviser les intervalles dans le nombre minimum de groupes (LeetCode 2406) – Java, Python, C++ Solutions

Si vous préparez une entrevue de codage, vous rencontrerez souvent des questions liées à l'intervalle. L'un des plus délicats est le nombre minimum de groupes (LeetCode 2406). Dans ce post, nous allons décomposer le problème, marcher à travers une solution O(n log n) propre, présenter le code de travail dans **Java, Python, et C++**, et discuter des *bon*, *mauvais* et *ugly* façons de s'y attaquer. Cet article est rempli de mots-clés que les recruteurs aiment : *groupes minimums, cupidité, ligne de balayage, salles de réunion, intervalles inclusifs, préparation d'entrevue, interview de codage* et plus.

---

Déclaration du problème

Vous recevez un tableau `intervalles` où `intervalles[i] = [left_i, right_i]` (inclus).

Divisez les intervalles dans les groupes **fest** de sorte que **aucun intervalle dans le même groupe ne se chevauche**. Deux intervalles se chevauchent s'ils partagent au moins un point, **y compris les paramètres**. Retourner le nombre minimum de groupes requis.

> **Exemple**
> Entrée: `[[5,10],[6,8],[1,5],[2,3],[1,10]] "
> Produit: `3`

---

Pourquoi cette question est importante

- **Greedy + Tri**: Technique d'entretien classique.
- **Points de fin inclusifs**: De nombreux candidats oublient que `[1,5]` et `[5,8]` *do* chevauchement.
- ** Grandes contraintes**: `n ≤ 105` vous force à concevoir une solution `O(n log n)`.
- **Language-agnostic**: Fonctionne en Java, Python et C++.

---

## Aperçu de la solution – Ligne de balayage à deux points

1. **Séparer** tous les points de départ et de fin en deux tableaux.
2. **Trier** chaque tableau.
3. **Passer à travers les départs** tout en traçant la première extrémité ('endPtr').
- Si le démarrage actuel `s` est **après** `ends[endPtr]` (`s > fin[endPtr]`), nous pouvons réutiliser ce groupe → déplacer `endPtr`.
- Sinon, nous avons besoin d'un **nouveau groupe** → incrément "groupes".
4. Le nombre final de groupes est égal au nombre minimum de groupes.

> C'est la même logique utilisée pour **Seeting Rooms II**, mais le paramètre inclusif change la comparaison entre `>=` et `>`.

Bonne
- **Heure**: `O(n log n)` (le tri domine).
- **Espace**: "O(n)" (deux tableaux auxiliaires).
- **Clarity**: Deux boucles, un seul pointeur, simple.

Mauvais
- **Modèle Heap / Priority-Queue** – toujours `O(n log n)` mais ajoute des frais généraux inutiles.

#### # Ugly
- Balayage excessif avec compteurs et mises à jour en place qui sont difficiles à raisonner.

---

Numéro de code

> Chaque implémentation de langage suit les mêmes étapes algorithmiques.

Python 3

'`python
de taper l'importation Liste

Solution de classe:
def minGroupes(eux-mêmes, intervalles: Liste[Liste[int]]) -> Int:
début = trié(i[0] pour i par intervalles)
fin = trié(i[1] pour i par intervalles)

end_ptr = 0
groupes = 0

pour s en début:
si s > termine[end_ptr] :
end_ptr += 1
Sinon:
groupes += 1

Groupes de retour
«» "

### Java (Java 17+)

"Java
Importer java.util. Les tableaux;

solution de classe {
public int minGroupes(int[][] intervalles) {
int n = intervalles de longueur;
int[] starts = nouveau int[n];
int[] fins = nouvelle int[n];

pour (int i = 0; i < n; i++) {
début[i] = intervalles[i][0];
fin[i] = intervalles[i][1];
}

Arrays.sort(débuts);
Tableau 3.

int endPtr = 0, groupes = 0;
pour (int s : commence) {
si (s > fin[endPtr]) endPtr++;
autres groupes++;
}
les groupes de retour;
}
}
«» "

### C++ (C++17)

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
int minGroupes(std::vector<std::vector<int>>& intervalles) {
int n = intervalles.size();
md::vector<int> starts(n), fin(n);
pour (int i = 0; i < n; ++i) {
début[i] = intervalles[i][0];
fin[i] = intervalles[i][1];
}
à:sort(starts.begin(), starts.end());
std:sort(ends.begin(), find.end());

int endPtr = 0, groupes = 0;
pour (int s : commence) {
si (s > fin[endPtr]) ++endPtr;
autres groupes ++;
}
les groupes de retour;
}
};
«» "

---

Analyse de complexité

Langue Heure Espace
[En milliers de dollars des États-Unis]
Python "O(n log n)" Autres
"O(n log n)" Autres
"O(n log n)" Autres

> L'exécution est dominée par le tri. Le balayage est linéaire ("O(n)").

---

Conseils d'entrevue

1. ** Préciser les paramètres d'inclusion** avant le codage.
2. ** Expliquez le balayage** à l'intervieweur – montrez que vous comptez le nombre maximum d'intervalles simultanés.
3. **Champs d'essai**:
- `[1,5], [5,10]` → 2 groupes.
- Groupe `[1,2], [3,4]` → 1.
4. **Mention** la relation avec les salles de réunion II, car elle démontre votre vaste connaissance.

---

Lire plus

- ** Salles de réunion II** – LeetCode 253
- ** Intervalles de non-overlaping** – LeetCode 435
- **Algorithmes du mariage** – *Cracking the Coding Interview*
- **Algorithme de la ligne de balayage** – *Algorithmes (Cormen, Leiserson, Rivest, Stein)*

---

À emporter

Les intervalles de vie dans le minimum Nombre de groupes** Le problème est une mine d'or pour les intervieweurs afin de tester votre maîtrise du tri avide, de la manipulation des frontières et de l'efficacité algorithmique. La solution de balayage à deux points propre est efficace, facile à mettre en œuvre et linguistique-agnostique. En partageant ce post, vous montrez également la capacité d'écrire du code propre en Java, Python et C++ – exactement ce que les recruteurs recherchent.

Bon codage, et bonne chance avec votre prochaine interview!

---

Note finale

> Si vous avez trouvé cet article utile, partagez-le sur LinkedIn ou Twitter et marquez vos recruteurs avec #codinginterview #leetcode2406 #minGroupes.

---

**Mots clés utilisés:** "Divide Intervals Into Minimum Nombre de Groupes, LeetCode 2406, groupes minimum, algorithme gourmand, ligne de balayage, salles de réunion II, paramètres inclusifs, interview de codage, solution Java, solution Python, solution C++, prép d'entrevue, complexité algorithmique".