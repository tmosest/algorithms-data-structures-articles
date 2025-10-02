---
titre: LeetCode 2549. Compte Distinct Nombres à bord -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2549. Compte Distinct Nombres à bord – One-liner, One-Solution (Java / Python / C++)

> **LeetCode n°2549** – *Facile* – Nombres distincts à bord

> **Complexité temporelle** – **O(1)**
> **Complexité spatiale** – **O(1)**

---

Récapitulation du problème

Vous commencez par un seul numéro `n` sur un tableau.
Chaque jour vous examinez **chaque** nombre `x` qui est déjà sur le tableau et ajoutez tous les nombres `i` (`1 ≤ i ≤ n`) qui satisfont `x % i == 1'.
Après 1 000 000 000 jours astronomiques, on vous demande : * combien de numéros distincts sont sur le tableau ? *

> **Observation principale** – Après la toute première étape, vous ne pouvez jamais atteindre les numéros `1 ... n`.
> En fait, chaque nombre `k` (`2 ≤ k ≤ n`) sera finalement ajouté, alors que `1` ne peut jamais être ajouté parce que `x % 1 == 0` pour chaque `x`.
> Par conséquent, le tableau contiendra tous les numéros allant de `2` à `n`, c'est-à-dire les numéros `n‐1` (et si `n=1`, seul le nombre `1` reste).

Donc la réponse est

Texte
si n == 1 → 1
Autre → n - 1
«» "

Aucune simulation n'est requise.

---

# # # ##

"Java
solution de classe {
secteur public Totals(int n) {
retour n == 1 ? 1 : n - 1;
}
}
«» "

- Oui. Pourquoi ça marche ?

- "n" 1` → seul le numéro de départ reste.
- Pour tout `n > 1`, chaque entier `2 ... n` devient accessible, donnant `n-1` valeurs distinctes.

---

Python

'`python
Solution de classe:
def distinct Integers(self, n: int) -> Int:
retour 1 si n == 1 autre n - 1
«» "

---

C++

'`cpp
solution de classe {
public:
Int distinct Totals(int n) {
retour (n == 1) ? 1 : n - 1;
}
};
«» "

---

Article sur le blog – Comment faire pour éponger le code 2549 en 3 minutes (Java, Python, C++)

Titre
*Cracking LeetCode 2549 – Compter des numéros distincts à bord : Un liner Java/ Python/C++

Description de la méta
Apprenez la solution O(1) pour le LeetCode 2549. Quick Java, Python et C++ code + aperçus d'entrevue.

---

Introduction

Si vous préparez des interviews d'ingénierie logicielle, LeetCodes *Count Distinct Numbers on Board* (Problème 2549) est une question classique qui teste votre capacité à repérer des modèles.
Ci-dessous vous trouverez une explication concise, pourquoi la simulation naïve échoue, et le parfait un-liner en Java, Python et C++ que vous pouvez copier-coller lors d'une entrevue de codage.

> **Mots clés**: LeetCode 2549, Compte Distinct Nombres sur le forum, interview prep, interview de codage, solution Java, solution Python, solution C++, interview d'algorithme, solution O(1), défi de codage

---

Les bons

Qu'est-ce qui est bien dans ce problème ? Autres
-- -- -- ----------------------------------
**Logique simple**=Elle se réduit à une seule perspicacité mathématique: les nombres 2–n ne sont jamais atteignables. Autres
**Réponse déterministe**. Pas de randomisation, pas de boucles, pas de structures de données – juste un "if". Autres
**Temps et espace « O(1) » rapides – parfaits pour l'entrevue - Autres

---

- Oui. Les mauvais

Pourquoi l'approche naïve est un piège
[En milliers de dollars des États-Unis]
**Simulation gaspillée**= Les gens écrivent souvent des boucles imbriquées pouvant durer jusqu'à 109 jours – ce qui est une complexité temporelle *gigantique* et évidemment impossible. Autres
**Miscompréhension modulo**. Autres
**Erreur de la ligne**= Oublier le cas `n=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=2=1=1=1=1=1=1= "0". Autres

---

- Oui. L'Ugly

Des choses qui peuvent vous faire monter
- C'est pas vrai.
**Off‐by‐one**= Décomptage des nombres accessibles comme `n` au lieu de `n‐1'. Autres
**Loops infinies**=Tentative d'itérer jusqu'à ce qu'aucun nouveau nombre n'apparaisse, mais oubliant que le processus s'arrête après au plus des valeurs uniques `n`. Autres
**En supposant que tous les nombres sont atteignables**= Certains penseront que chaque `i` est ajouté immédiatement, mais la condition modulo filtre beaucoup. Autres

---

### Aperçu étape par étape

1. **Démarrer avec `n`** – le seul nombre présent.
2. **Cherchez `i` où `n % i == 1'.**
Pour `n = 5`, `i = 2` et `4` satisfont à cette exigence.
3. ** Ajouter ces numéros** – le conseil détient maintenant « {2, 4, 5} ».
4. **Le lendemain** – examiner chacun de ces éléments; par exemple `4 % 3 == 1` → ajouter `3`.
5. ** Avisez le modèle** – vous finirez par ajouter *chaque* entier de `2` à `n`.
6. **Le nombre `1` n'est jamais ajouté** parce que `x % 1 == 0`.
7. **Après 1 000 000 000 jours** – vous avez exactement des nombres distincts «n‐1» si «n > 1»; autrement seulement «1».

---

### La ligne unique

"Java
// Java
secteur public Totals(int n) { retour n == 1 ? 1 : n - 1; }
«» "

'`python
# Python
Def distinctIntégres(n: int) -> Int: retour 1 si n == 1 autre n - 1
«» "

'`cpp
// C++
Int distinct Totals(int n) { retour (n == 1) ? 1 : n - 1; }
«» "

---

Dernier départ

*L'astuce est de regarder la condition modulo et la plage fixe `1 ... n`. Une fois que vous réalisez que chaque nombre `k ≥ 2` sera finalement ajouté et `1` jamais, la réponse s'effondre à `n‐1` (ou `1` quand `n == 1`). *

Écrivez ce liner, expliquez le raisonnement en quelques phrases, et vous impressionnerez les intervieweurs avec rapidité et clarté.

---

Liste de contrôle du référencement

- **Titre et Meta** contiennent des mots-clés cibles (`LeetCode 2549`, `Count Distinct Numbers on Board`, `Java solution`, `Python solution`, `C++ solution`).
- **Les Headings** utilisent naturellement les mots clés (`Java solution`, `Python solution`, `C++ solution`).
- **Les points du bulletin** mettent en évidence le bon, le mauvais et laid – maintient les lecteurs engagés.
- **Les extraits de code** sont courts et en trois langues, destinés à un large public.
- **Word compter** ~800 mots – assez pour la profondeur mais assez concis pour se classer pour des recherches de réponses rapides.

---

### TL;DR

Texte
Réponse = (n == 1) ? 1 : n - 1
«» "

Exécutez-le en **Java, Python ou C++** et vous aurez une solution d'interview en quelques secondes. Bon codage 