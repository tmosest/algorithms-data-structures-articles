---
titre: LeetCode 403. Saut à la grenouille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 403 – Saut à la grenouille
- Oui. Le bon, le mauvais et le mauvais – Une plongée profonde avec code en Java, Python & C++

> **Problème** – *Saut de grenouille*
> La rivière est divisée en unités. Une grenouille commence sur la première pierre (position 0) et doit atteindre la dernière pierre.
> Le premier saut doit être exactement **1 unité**. Après un saut d'unités `k`, le prochain saut peut être `k-1`, `k` ou `k+1`.
> **Question** – La grenouille peut-elle atteindre la dernière pierre?

> **Constraints**
> - < 2 ≤ pierres longueur ≤ 2000 > >
> - `0 ≤ pierres[i] < 231'
> - `pierres` augmente strictement et commence à `0`.

---

Pourquoi ce problème est-il une médaille d'or pour les entrevues

1. ** Programmation dynamique + Hashing** – Une combinaison classique qui met en valeur votre capacité à combiner des structures de données avec DP.
2. **Edge‐Case Handling** – Première règle de saut, sauts qui dépasseraient, manipulant les pierres manquantes.
3. **Échanges entre l'espace et le temps** – Vous pouvez discuter de la solution récursive naïve, de la mémoisation et de l'approche efficace DP/HashMap.
4. **Real-World Pertinence** – L'idée de "seul mouvement vers l'avant" et "longueur de saut" apparaît dans la navigation, le développement de jeux et la robotique.

---

## -SEO–Résumé amical

- **Mots-clés**: *LeetCode 403, Frog Jump solution, Java DP, Python récursive mémoization, C++ unordered_map, codage d'entretien, entretien de programmation dynamique, solution optimale, conseils d'entretien d'emploi, pratique d'entretien de codage*
- **Description détaillée**: Master LeetCode 403 – Saut à la grenouille. Découvrez les meilleures solutions Java, Python et C++, explorez DP avec des cartes de hachage et préparez-vous à l'entretien avec un blog détaillé. (en milliers de dollars)

---

L'approche PDD propre et efficace

L'idée est de garder une trace de chaque *possible longueur de saut* qui peut atteindre une pierre particulière.
Si une pierre peut être atteinte avec un saut de `k`, alors la pierre suivante peut être atteinte avec des sauts `k-1`, `k` ou `k+1`.

Texte
[pierre] = ensemble de longueurs de saut qui peuvent atterrir sur cette pierre
«» "

Nous partons à travers les pierres dans l'ordre et pour chaque longueur de saut stockée nous essayons les trois possibilités, les ajoutant à la pierre de destination correspondante si elle existe.

Complexité
- **Heure**: "O(n2)" dans le pire des cas (chaque pierre peut avoir jusqu'à "O(n)" longueurs de saut).
- **Espace**: "O(n2)" pour les ensembles dans le pire des cas, mais pratiquement beaucoup moins en raison de l'ordre croissant des pierres.

---

## Le "Bad" – Retour récursif (Trop lent pour les grandes entrées)

Un DFS simple qui tente les 3 options à chaque étape va rapidement exploser, surtout quand `stones.length` est proche de 2000.
- **Worst-cas exponentiel** ('3^n').
- **Risque de trop-plein** dans les langues sans optimisation de l'appel arrière.

> **Pourquoi c'est mauvais**: Bien que théoriquement simple, il ne respecte pas les limites de temps de LeetCode.

---

## --Les "Ugly" – Tricks HashSet sur-optimisés

Certains codeurs tentent d'enfermer le DP dans une seule ligne ou s'appuient sur des opérateurs ternaires imbriqués, sacrifiant ainsi la lisibilité pour la brièveté.

> **Pourquoi c'est bizarre**:
> - Dur à entretenir.
> - Pronez les bugs parce que vous perdez le flux logique.
> - Difficile à suivre pour les intervieweurs.

---

Code complet – trois langues

Ci-dessous vous trouverez des solutions ** propres, prêtes à la production** dans **Java, Python et C++**.
Tous utilisent la même stratégie DP + HashMap et sont prêts à coller dans l'éditeur LeetCode.

---

C'est pas vrai. Java – DP optimal avec `HashMap<entier, HashSet<entier>> "

"Java
Importation de java.util.*;

solution de classe publique {
pulvérisateur publicCross(int[] pierres) {
int n = longueur des pierres;
// Carte de la position de pierre à ensemble de longueurs de saut accessibles
Carte<entier, ensemble<entier>> accessible = nouveau HashMap<>();
pour (int pos : pierres) {
joignable.put(pos, nouveau HashSet<>());
}
joignable.get(0).add(1); // Le premier saut doit être 1

pour (int pos : pierres) {
pour (int jump : joignable.get(pos)) {
// Essayez k-1, k, k+1
pour (int nextJump = saut - 1; nextJump <= saut + 1; nextJump++) {
si (suivantJump <= 0) continue; // Pas de sauts en arrière
int suivant Pos = pos + nextJump;
si (accessible.contientKey(nextPos)) {
joignable.get(nextPos).add(nextJump);
}
}
}
}
// Si la dernière pierre a une longueur de saut accessible, nous avons réussi
return !reachable.get(stones[n - 1]).isEmpty();
}
}
«» "

**Pourquoi c'est bon**
- Pas de tableau `dp` global → n'utilise que les pierres qui existent.
- `HashSet` évite les duplications automatiquement.
- Séparation claire des préoccupations.

---

Python – Dictionnaire des ensembles

'`python
Solution de classe:
def canCross(self, stones: List[int]) -> bool:
atteignable = {pos: set() pour pos en pierres}
joignable[0].add(1) # Premier saut

pour pos en pierres:
pour sauter à portée de main[pos]:
pour nxt dans (jump - 1, saut, saut + 1):
si nxt <= 0:
poursuivre
nxt_pos = pos + nxt
si nxt_pos est accessible:
accessible[nxt_pos].add(nxt)

retour bool(reachable[stones[-1]])
«» "

*Python"s `dict` + `set` garde la mise en œuvre concise mais lisible. *

---

#### 3=C++ – `unordered_map<int, unordered_set<int> "

'`cpp
solution de classe {
public:
bool canCross(vecteur <int>& pierres) {
unordered_map<int, unordered_set<int>;
pour (int s : pierres) atteindre[s] = {};

atteindre[0].insérer(1); // Premier saut

pour (int s : pierres) {
pour (int jump : portée[s]) {
pour (int nxt = saut - 1; nxt <= saut + 1; ++nxt) {
si (nxt <= 0) continuer;
int nxtPos = s + nxt;
si (atteint.count(nxtPos))
la portée[nxtPos].insérer(nxt);
}
}
}
retour !reach[stones.back()].vide();
}
};
«» "

---

Essais des solutions

Autres Test de Pierres Attentes Java de Python de C++
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
"[0,1,3,5,6,8,12,17]""
"[0,1,2,3,4,8,9,11]"
"[0,1] """ "vrai" """
"[0,2]""""faux"""""""""
[0,1,2,3,4,5,6,6,7,8,9,10]

---

## -O Bonus: Pourquoi cette approche est-elle amicale

1. **Processus de pensée clair** – Commencez par *=Qu'est-ce qui peut atteindre une pierre?==* et construisez la table DP à partir de cela.
2. **Savoirs sur la structure des données** – L'utilisation de cartes et d'ensembles de hachage démontre une compréhension de la recherche moyenne O(1).
3. **Edge Cases** – Gérez les longueurs de saut négatives, les pierres manquantes et la règle du premier saut – les intervieweurs aiment les candidats qui anticipent les cas de coin.
4. **Scalabilité** – Discutez de la façon dont l'algorithme se comporterait si `stones.length` double et pourquoi il s'insère toujours dans les délais habituels.

---

## Comment tirer parti de ce blog pour votre recherche d'emploi

1. **SEO‐Rich Title** – -Master LeetCode 403 – Frog Jump: Java, Python & C++ Solutions pour les interviews
2. **Partager sur LinkedIn / Twitter** – Les recruteurs d'étiquettes et mentionner le tag *dynamic programming*.
3. **Créer une courte vidéo** – Enregistrez une marche de 3 minutes et intégrez les extraits de code.
4. **Ajouter un répertoire d'extraits de code** – Hôtez les trois solutions sur GitHub avec un README qui explique le problème, la complexité et les reprises d'entrevue.
5. **Inviter les commentaires** – Encourager les lecteurs à poser des questions de suivi; une section de commentaires animée signale une communauté engagée.

---

À emporter

- **Le ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
- **Le "Bad"** : Récursion non-mémoisée – exponentielle et trop lente.
- **Le code surminé qui sacrifie la lisibilité pour la brièveté.

En maîtrisant la solution de PDD propre et en comprenant les pièges, vous serez bien préparé pour toute question d'entrevue de style *Frog Jump*. Bon codage ! (en milliers de dollars)