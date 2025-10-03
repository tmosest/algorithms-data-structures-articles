---
titre: LeetCode 2734. Lexicographiquement la plus petite chaîne après l'opération de sous-chaîne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Comment maîtriser LeetCode 2734 – *Lexicographiquement la plus petite chaîne après l'opération de sous-chaîne*

> **Vous voulez décrocher un rôle d'ingénieur en logiciel? * *
> Pratiquez ce tour avide d'un liner, écrivez le code Java/Python/C++ propre, et expliquez-le dans une interview.

---

Récapitulation des problèmes

On vous donne une chaîne de lettres anglaises minuscules.
Vous pouvez effectuer **exactement une opération**:

1. Choisissez toute sous-chaîne contiguë non vide.
2. Remplacer chaque caractère de cette sous-chaîne par sa lettre alphabet *précédente* (`'b' → 'a'`, `'a' → 'z'`).

Retourne la chaîne **lexicographiquement la plus petite** que tu puisses obtenir après une opération.

«» "
Entrée : "cbabc"
Sortie : "baabc" // soustraire de l'indice 0.1
«» "

Contraintes
- "1 ≤ longueur ≤ 3 * 10^5"
- "s" ne contient que des lettres anglaises minuscules

---

Le point de vue clé

Plus un personnage devient petit, plus il domine l'ordre lexicographique. *

Ainsi, pour obtenir la plus petite chaîne mondiale, nous devrions :

1. **Cibler la première série de caractères non «a»** (c'est-à-dire le bloc le plus contigu à gauche qui n'est pas déjà minimal).
2. Diminue chaque personnage de ce bloc par un.
3. Si la chaîne entière est tout `'a'`, la diminution de tout caractère augmenterait * la chaîne.
Dans ce cas particulier, changer le **dernier** `'a'` en `'z'` – c'est le changement le moins dommageable.

Cette stratégie gourmande est optimale et fonctionne en temps linéaire.

---

Aperçu de la solution (Greedy)

Étape Ce que nous faisons Pourquoi ça marche
C'est pas vrai.
Autres Le premier bloc détermine l'amélioration la plus rapide possible. Autres
Autres 2=Continuer à diminuer les caractères jusqu'à ce que nous atteignions un `'a'` ou que la chaîne se termine. Chaque décrément rend le préfixe strictement plus petit; s'arrêter à un `'a'' maintient le reste inchangé. Autres
Si nous ne trouvons jamais de non‐«a»», changez le dernier caractère en «z». Tous les caractères sont déjà minimes ( ''a''). La seule façon de faire une opération qui satisfait exactement une opération est de heurter la dernière `'a'` à `'z'`, ce qui aggrave le moins la chaîne. Autres

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Analyser pour la première fois les non‐« a » **O(n)**
Bloc de décrétion **O(k)** où `k ≤ n' –
Dans l'ensemble **O(n)**

`n` est la longueur de `s`.
L'algorithme gère confortablement jusqu'à "3·10^5".

---

Mise en œuvre du code

Voici des solutions propres et prêtes à la production dans **Java, Python et C++**.
Chaque mise en œuvre suit la même logique gourmande et utilise des modifications *en place* pour une efficacité maximale.

C'est pas vrai. Java

"Java
solution de classe publique {
chaîne publique plus petite chaîne(chaîne s) {
int n = s.longueur();
// Convertir en tableau de caractères mutables
char[] arr = s.toCharArray();

// Vérifiez si la chaîne entière est 'a'
booléen allA = vrai;
pour (charc : arr) {
si (c != 'a') { allA = faux; casse; }
}

si (allA) {
// Changer le dernier caractère en 'z'
[n - 1] = 'z';
retourner la nouvelle chaîne(arr);
}

// Trouver la première sous-chaîne de non-'a' et le décrément
i = 0;
alors que (i < n& arr[i] == 'a') i++; // sautent en tête 'a '
(i < n& arr[i] != 'a') {
arr[i] = (char) (arr[i] - 1); //
i++;
}
retourner la nouvelle chaîne(arr);
}
}
«» "

---

# # # # # #

'`python
Solution de classe:
def le plus petit Chaîne(self, s: str) -> str:
n = len(s)
arr = liste(s)

Tous "a" ?
si tous(c) pour c in arr:
arr[-1] = 'z '
retour ''.join(arr)

i = 0
alors que i < n et arr[i] == «a»:
i += 1 # sauter en tête 'a '
alors que i < n et arr[i] != «a»:
arr[i] = chr(ord(arr[i]) - 1)
i += 1

retour ''.join(arr)
«» "

---

C'est vrai. C++

'`cpp
solution de classe {
public:
chaîne la plus petite Chaîne(s) {
int n = s.size();
bool allA = vrai;
pour (charc : s) {
si (c != 'a') { allA = faux; casse; }
}

si (allA) { // tous 'a' → changer en dernier '
s[n-1] = 'z';
retour s;
}

i = 0;
alors que (i < n& s[i] == 'a') ++i; // sautent en tête 'a '
(i < n& s[i] != 'a') {
s[i] = s[i] - 1; //
++i;
}
retour s;
}
};
«» "

---

Essai rapide

Produit escompté
-- -- -- -- -- -- -- --
"cbabc" "baabc" Autres
"aaa" "az"
"Acbbc" "abaab" Autres
"code de la poste" "kddsbncd" Autres
""aaa" ""aaz"

Exécutez les extraits ci-dessus avec ces exemples pour voir la solution avide en action.

---

## Comment les éviter

Pourquoi ça arrive
- Oui.
Autres **Passer la chaîne entière** (penser que nous devons changer tous les caractères) - Mauvaise interprétation d'une opération exacte - comme -changer tout -- Transformer seulement le premier bloc non--'a'` ; arrêter quand vous touchez un `'a'`. Autres
**Changement d'un `'a'` à `'z'` trop tôt**. Autres
Erreurs hors-par-un dans les maths de caractère** 1 ' au lieu de `c - 1 ' , rappelez-vous que l'opération soustrait l'index alphabétique; utilisez `c = chr(ord(c)-1)' (ou `c-1' en C++). Autres
**O(n2) dans Python**=Construire de nouvelles chaînes dans les boucles== Modifier une liste et joindre une fois à la fin. Autres

---

Pourquoi ce blog aide votre préparation d'entrevue

1. **Explication claire du problème** – Dans les interviews, vous aurez besoin de réaffirmer le problème dans vos propres mots.
2. ** Argument de la grêle** – Démontrez votre capacité à raisonner sur l'optimalité.
3. **Trois implémentations linguistiques** – Montrez la polyvalence à travers Java, Python et C++.
4. **Edge-Case Awareness** – Mettre en avant l'affaire spéciale « All a=»s – une surprise d'entrevue commune.
5. ** Discussion sur le rendement** – Le temps linéaire pour les chars `3·10^5` est une contrainte réelle.

En écrivant cette solution **et en expliquant le raisonnement** dans une interview typique, vous démontrerez :

- **La pensée algorithmique** (greedy, linéaire-time).
- ** Discipline de codage** (changements en place, allocations minimales).
- **Problème de résolution de la clarté** (traitement des cas de bord, preuve de l'optimalité).

---

## Ohio SEO-Friendly Title & Meta‐Description

> **Titre** – Comment résoudre le LeetCode 2734: Lexicographiquement plus petite corde après l'opération de sous-chaîne (Java/Python/C++)
> **Méta‐Description** – Master l'astuce gourmande pour LeetCode 2734 et impressionner les gestionnaires d'embauche. Apprenez les solutions Java, Python et C++ propres, la gestion des cas de bord et les points d'entrevue. (en milliers de dollars)

Utilisez les mots clés suivants dans l'article:
`Lexicographically Smallest String`, `LeetCode 2734`, `string manipulation`, `greedy algorithme`, `coding interview`, `logiciel engineer`, `Java solution`, `Python solution`, `C++ solution`.

---

## -Take final- Loin

- **Greedy** est l'étoile : ciblez le premier bloc non-« a ».
- **Les cas d'Edge sont importants** – les chaînes all‐`'a' ont besoin d'une touche spéciale.
- **La clarté du code** est meilleure que la micro-optimisation dans la plupart des interviews.
- Pratique expliquant le *pourquoi* – ce qui est ce que les intervieweurs sont après.

Si vous pouvez écrire la solution en 30 à 60 secondes et expliquer clairement le raisonnement, vous brillerez dans n'importe quel entretien d'ingénierie logiciel. Bon codage ! (en milliers de dollars)

---