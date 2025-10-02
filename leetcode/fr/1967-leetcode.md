---
titre: LeetCode 1967. Nombre de chaînes qui apparaissent comme des sous-chaînes dans Word -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1967 – Nombre de chaînes qui apparaissent comme des chaînes de texte

> [LeetCode](https://leetcode.com/problèmes/number-of-strings-there-as-substrings-in-word/)

> **Objectif** – Compter le nombre de chaînes de "patterns" et de "word" dans les "patterns" comme une sous-chaîne de "word".

> **Pourquoi ça compte** – C'est une question d'interview classique qui teste votre compréhension de la manipulation de chaîne, la méthode `contient`, et comment garder la solution simple mais efficace. Maîtriser cela augmentera vos chances de casser la partie *string* des entretiens techniques.

---

## Description du problème (formelle)

Texte
Entrée : motifs : Chaîne[] (1 ≤ motifs longueur ≤ 100)
mot: chaîne (1 ≤ longueur du mot ≤ 100)
Tous les caractères sont en minuscules lettres anglaises.

Extrant: int – le nombre de motifs qui apparaissent comme une substrante contiguë en mot.
«» "

Échantillon

Modèles
- C'est quoi ?
["a", "abc", "bc", "d"]
"Aaaabbb"
["a", "a", "a"]

---

L'approche – les bons, les mauvais et les méchants

Une bonne approche
C'est pas vrai.
**La force brute "contient"*** *O(n·m*) temps (n motifs, m mots) – parfait pour les contraintes. <br> Simple, lisible, aucune structure de données supplémentaire. Le balayage répété pourrait être coûteux pour les données plus importantes. S/O – trop simple. Autres
**Pré-construire un Suffix Trie/Automaton** <br> Bon pour les "patterns" énormes et les "mots" répétés. Utilisation de la mémoire lourde (~O(m2)). <br> Overkill pour les contraintes LeetCode. Code complexe, sujet aux bogues. Autres
**KMP/Two-Pointer par motif**= Linéaire par motif dans la longueur du motif + mot. <br> Évite le coût du pire cas `contient`.== Toujours *O(n·m*) au total. <br> Frais généraux de mise en œuvre. Sans objet

> **Ligne de bottom:** L'approche de la force brute en utilisant Java="String.contient()`, Python="s `in`, ou C++="s `find()` est le plus pratique* pour ce problème. Il vous donne la bonne réponse, fonctionne en microsecondes pour les limites données, et démontre un style de codage propre – exactement ce que les intervieweurs recherchent.

---

Mise en œuvre du code

Voici des implémentations propres, prêtes à fonctionner dans **Java**, **Python** et **C++**. Chaque solution suit la même logique: itérer sur chaque motif, vérifier s'il s'agit d'une sous-chaîne de `mot`, et incrémenter un compteur.

> **Note** – Le code comprend un petit bloc `main`/`if __name__ == "_main__":` pour les tests rapides. Dans un environnement LeetCode, vous avez seulement besoin de la classe ou fonction `Solution`.

---

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe publique {
***
* Comptez combien de motifs apparaissent comme sous-chaînes en mots.
*
* Les modèles @param Tableau des modèles de candidats.
* @param mot La corde cible.
* @retour Nombre de motifs qui sont des sous-chaînes de mots.
*/
public int numOfStrings(String[] patterns, String word) {
nombre int = 0;
pour (Modèle de fixation : modèles) {
si (word.contient(pattern)) { // O(m) pour chaque motif
count++;
}
}
le nombre de retours;
}

// ---- démo rapide ----
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.numDeString(
nouvelle chaîne[]{"a", "abc", "bc", "d"},
"abc"); // 3

Système.out.println(sol.numDeString(
nouvelle chaîne[]{"a", "b", "c"},
aaaaabbbbb); // 2

Système.out.println(sol.numDeString(
nouvelle chaîne[]{"a", "a", "a"},
"ab"); // 3
}
}
«» "

**Complexités* *

Temps Espace
C'est le cas.
(n ≤ 100, m ≤ 100)

---

- Oui. 2. Python

'`python
de taper l'importation Liste

Solution de classe:
def numOfStrings(self, patterns: List[str], mot: str) -> Int:
"""
Compter les motifs qui apparaissent comme des sous-chaînes en mots.

:param patterns: List[str] – cordes candidates.
:param word: str – chaîne cible.
:retour : int – nombre de motifs correspondants.
"""
nombre = 0
pour pat dans les motifs:
si pat in word: La sous-chaîne de Python
nombre += 1
Nombre de retours

# ---- démo rapide ----
si __nom__ == "__main__" :
sol = Solution()
print(sol.numOfStrings(["a", "abc", "bc", "d"], "abc") # 3
print(sol.numOfStrings(["a", "b", "c"], "aaaabbbbb") # 2
print(sol.numOfStrings(["a", "a", "a"], "ab") # 3
«» "

**Complexités* *

Temps Espace
C'est le cas.
D'une manière générale

---

- Oui. 3. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int numOfStrings(vector<string>& patterns, string word) {
nombre int = 0;
pour (cost string & pat : pat) {
if (word.find(pat) != string::npos) { // O(m) par motif
+ nombre;
}
}
le nombre de retours;
}
};

// ---- démo rapide ----
Int main() {
Solution sol;
vecteur<string> p1 = {"a", "abc", "bc", "d"};
Cout << sol.numOfStrings(p1, "abc") << endl; // 3

vecteur<chaîne> p2 = {"a", "b", "c"};
<< sol.numOfStrings(p2, "aaaaabbbbb") << endl; // 2

vecteur<string> p3 = {"a", "a", "a"};
<< sol.numOfStrings(p3, "ab") << endl; // 3

retour 0;
}
«» "

**Complexités* *

Temps Espace
C'est le cas.
D'une manière générale

---

Plongée profonde – Pourquoi Cela fonctionne

1. **Le contrôle de sous-chaîne** (`contient` / `in` / `find`) est déjà une opération **linéaire**: il scanne `word` jusqu'à ce qu'il trouve `pattern` ou atteigne la fin.
2. Puisque la longueur `mot` ≤ 100, même la pire analyse de chaque motif est banale pour les processeurs modernes.
3. L'algorithme est *stable* – il gère correctement les motifs dupliqués (comme `["a","a","a"]`) parce que chaque événement est compté séparément, correspondant à l'exigence du problème.

---

Les alternatives – Quand aller plus grand

Scénario Recommandation Stratégie Complexité
- C'est quoi ?
**Grand tableau de modèles** (en dizaines de milliers) O(longueur totale du motif + longueur du mot)
Autres **Très long `mot`** (en millions de caractères)= Utilisez un **Suffix Automaton** ou **Suffix Array** pour répondre aux questions d'existence sous-chaîne dans *O(1)* après le prétraitement O(m). O(m) prétraitement, questions O(1)
**Plusieurs requêtes sur le même `mot`**= Préprocessus `word` dans un suffixe trie/automaton une fois, puis vérifier tous les motifs dans *O(1)* chaque.==O(m) préprocessus, O(1) par requête==

> *Mais* pour les contraintes de LeetCode, la solution simple `contient` est la plus concise et passe confortablement.

---

## A emporter pour réussir l'entrevue

- **Lisez d'abord les contraintes.** Une petite taille d'entrée permet souvent une solution simple.
- **Expliquez votre solution en compromis temps/espace.** Les intervieweurs aiment voir que vous pouvez justifier vos choix.
- **Cas de bord de Mention.** Dupliquer les motifs, les chaînes vides (si permis), et la différence entre la sous-chaîne et la sous-séquence.
- ** Gardez le code propre et commenté.** Une solution soignée reflète le professionnalisme.

---

Résumé optimisé du SEO

Vous cherchez à décrocher un rôle d'ingénierie logicielle? Mastering LeetCode #1967 Nombre de cordes qui apparaissent comme des sous-chaînes dans Word est une victoire rapide. Le problème teste les compétences de base en recherche de chaînes et votre capacité à écrire un code clair et efficace. Notre guide offre:

- Implémentations Java, Python et C++
- Le raisonnement pas à pas : pourquoi "contient" suffit
- Analyse de complexité à discuter dans les interviews
- Conseils sur le moment de l'échelle avec essayer ou suffixe automate

Utilisez cet article comme compagnon de préparation d'entrevue et impressionnez les recruteurs avec vos côtelettes de codage et votre pensée stratégique. Bon codage !

---