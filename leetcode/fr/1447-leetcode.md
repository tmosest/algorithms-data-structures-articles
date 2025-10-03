---
titre: LeetCode 1447. Fractions simplifiées -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1447 – Fractions simplifiées
**Solution d'agnostique en langue de programmation** (Java / Python / C++)
**Complexité temporelle** : \(O(n^2)\)
**Complexité spatiale** : \(O(n^2)\) (taille de sortie la plus mauvaise)

---

1.1 L'idée

Pour chaque dénominateur `d` de **2** à `n "
  pour chaque numérateur `num` de **1** à `d-1`

*Si* `gcd(num, d) == 1` la fraction `num/d` est **irréductible** (simplifiée).
Conservez-le comme une chaîne `"num/d"`.

Le test « gcd » garantit que nous n'ajoutons jamais une fraction réductible comme « 2/4 ».
Aucune structure de données supplémentaire (hash-maps, sets) n'est requise au-delà de la liste de sortie.

---

Code

Code de la langue
- C'est quoi ?
*Java**
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

solution de classe publique {
liste publique<String> pratiques simplifiées(int n) {
Liste du résultat <String> = nouvelle liste de distribution<>();
pour (int denom = 2; denom <= n; denom++) {
pour (int num = 1; num < denom; num++) {
si [gcd(num, denom)] 1) {
résultat.add(num + "/" + nom);
}
}
}
le résultat du retour;
}

// Algorithme euclidien – O(log min(a,b))
Int privé gcd(int a, int b) {
pendant que (b != 0) {
tmp = a % b;
a = b;
b = tmp;
}
retour a;
}
}
«» Autres
*Python**
de taper l'importation Liste

Solution de classe:
et simplifié Fractions(self, n: int) -> Liste[str]:
def gcd(a: int, b: int) -> Int:
tandis que b:
a, b = b, a % b
retour a

res = []
pour le nom dans la plage(2, n + 1):
pour num dans l'intervalle(1, denom):
si gcd(num, nom) == 1 :
res.append(f"{num}/{denom}")
retour res
«» Autres
*C++ *Cpp
#incluez <vecteur>
#incluez <string>
#incluez <numérique> // std::gcd en C++17

solution de classe {
public:
Std::vector<std::string> simplifiéFractions(int n) {
md::vecteur<std::chaîne> rés;
pour (int denom = 2; denom <= n; ++denom) {
pour (int num = 1; num < denom; ++num) {
si (std:gcd(num, denom) == 1) {
res.push_back(std::to_string(num) + "/" + std::to_string(denom));
}
}
}
retour rés;
}
};
«» Autres

---

Pourquoi ça marche ?

Explication
C'est pas vrai.
**Correctness** – L'algorithme euclidien identifie correctement les paires de coprimes. Autres
**Complète** – Chaque fraction réduite avec dénominateur ≤ n est générée. Autres
**Performance** – "O(n^2)" est optimal car il y a environ \(\frac{n(n-1)}{2}\) fractions possibles. Autres
**Simplicité** – Pas d'arithmétique flottante, pas de cartes de hachage. Autres

---

♪ 2. Article du blog
**Titre:** *Fractions simplifiées (Code 1447) – Le bon, le mauvais et le mauvais

2.1 Introduction (Méta-Description du référencement)

> Master LeetCode 1447 - Fractions simplifiées en Java, Python et C++. Découvrez la solution optimale basée sur le GCD, les pièges des tours à point flottant, et comment impressionner les gestionnaires d'embauche avec un code propre et prêt à l'entrevue. Idéal pour les candidats à la structure de données et à l'algorithme.

**Mots clés:** LeetCode 1447, fractions simplifiées, question d'entrevue, algorithme GCD, solution Java, solution Python, solution C++, code d'entrevue d'emploi, pensée algorithmique.

---

2.2 Le problème en bref

> Compte tenu d'un entier **n** (1 ≤ n ≤ 100), retourner toutes les fractions irréductibles comprises entre 0 et 1 (exclusif) dont le dénominateur n'excède pas **n**. L'ordre n'est pas pertinent.

Exemple
`n = 4 → ["1/2", "1/3", "1/4", "2/3", "3/4"] "
(L'avis **2/4** est omis car il simplifie **1/2**.)

---

2.3 La bonne solution – une solution propre et basée sur les GCD

Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Correctness**= Utilise l'algorithme euclidien pour tester `gcd(num, denom) == 1'. Aucune chance de faux positifs. Autres
**Simplicité**= Seulement deux boucles imbriquées; pas de conteneurs supplémentaires ou de conversions en points flottants. Autres
**Performance**= Temps `O(n2)`, qui est optimal compte tenu de la taille de sortie; espace auxiliaire `O(1)` en plus de la liste de résultats. Autres
**Readability**. Autres
**Portabilité**= Fonctionne de façon identique en Java, Python, C++ – parfait pour la préparation d'entrevues dans toutes les langues. Autres

Extrait de code (Java)

"Java
pour (int denom = 2; denom <= n; denom++) {
pour (int num = 1; num < denom; num++) {
si [gcd(num, denom)] 1) {
résultat.add(num + "/" + nom);
}
}
}
«» "

---

## 2.4 L'Énorme – Cartes flottantes

Certaines solutions utilisent une carte des valeurs « flot » pour détecter les duplicatas :

'`cpp
val flottant = statique_cast<float>(j) / i;
si (!mp.count(val)) { /* ajouter fraction */ }
«» "

Problèmes

Sujet Impact
C'est quoi ?
**La perte de précision**. Autres
**Extra Space**= La carte Hash ajoute les frais généraux \(O(n2)\; inutile. Autres
**Complexité** Autres

Dans la pratique, cette approche fonctionne pour `n ≤ 100` mais échoue sur des entrées plus grandes ou des paramètres d'entrevue stricts où l'exactitude compte.

---

## 2.5 La Force brute sans GCD

Des boucles d'approche naïve sur toutes les paires de numérateurs/dénominateurs et *réduit* chaque fraction :

'`python
pour d dans la plage(2, n+1):
pour num dans la plage (1, d):
simplifié = reduce_fraction(num, d) # cher
si simplifié non vu:
voir.add(simplifié)
«» "

Pourquoi c'est moche

Sujet Conséquence
C'est pas vrai.
**Travail répétitif**= Chaque fraction est réduite même si elle est déjà connue. Autres
**Complexité plus élevée**=La réduction peut être `O(log min(a,b)'; répétée pour chaque paire entraîne un ralentissement notable. Autres
**Less Readable**= Fonctions d'aide supplémentaires, structures de données supplémentaires, plus difficiles à vérifier lors d'une entrevue. Autres

---

2.6 Liste de contrôle rapide pour les intervieweurs

Liste de contrôle
-- -- -- -- -- --
Utiliser Euclidean GCD (construits ou personnalisés). Autres
Deux boucles imbriquées; dénominateurs de 2 à "n". Autres
Pas de maths flottants. Autres
Retour `Liste<String>` (Java), `vecteur<string>` (C++), `Liste[str]` (Python). Autres
Conservez le code compact (20 lignes). Autres
Ajouter des commentaires pour plus de clarté. Autres

---

2.7 Réflexions finales

- La solution GCD est la norme **or** pour LeetCode 1447.
- Évitez les astuces flottantes à moins d'être explicitement autorisées.
- Gardez votre code *readable*, *correcte* et *efficace* – les intervieweurs se soucient de *comment* vous résolvez, pas seulement *ce* que vous résolvez.

Bonne chance pour l'entrevue de codage ! C'est ce qu'il a dit.

---

**Références**
- Problème de LeetCode 1447 : <https://leetcode.com/problèmes/simplification-fractions/>
Wikipedia: <https://en.wikipedia.org/wiki/Euclidean_algorithm>

N'hésitez pas à adapter les extraits pour votre propre préparation d'entrevue ou vos contributions en open-source.