---
titre: LeetCode 2138. Diviser une chaîne en groupes de taille k -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2138 – *Divisez une chaîne dans des groupes de taille k*
- Oui. C++ Solutions + SEO-Optimized Blog Post

> **Vous voulez passer votre prochaine entrevue de codage? * *
> Apprenez à craquer *Divisez une chaîne dans des groupes de taille k* dans **Java, Python et C++**.
> Ce blog vous permet de parcourir l'algorithme, de montrer des extraits de code propres, d'expliquer les avantages et les inconvénients, et même de vous donner une copie SEO-friendly pour atterrir votre travail de rêve.

---

Déclaration de problème (Code Leet 2138)

> **Divisez une chaîne dans des groupes de taille k**
> **Difficulté:** Facile

On vous donne une chaîne `s`, un entier `k` et un caractère `fill`.
Partition de la chaîne en groupes de longueur `k`:

1. Le premier groupe est les premiers caractères `k` de `s`.
2. Le deuxième groupe est les caractères `k` suivants, et ainsi de suite.
3. Pour le groupe final, s'il reste moins de caractères `k`, cadrez le groupe avec le caractère `fill` jusqu'à ce que sa longueur soit `k`.
4. Après avoir retiré le rembourrage du dernier groupe, la concaténation de tous les groupes doit égaler la chaîne originale `s`.

Retournez la liste de tous les groupes.

> **Exemples**
> ```texte
> s = "abcdefghi", k = 3, remplir = 'x' .
> s = "abcdefghij", k = 3, remplissage = 'x' .
> `` "

> **Constraints**
1 ≤ longueur ≤ 100
1 ≤ k ≤ 100
> - `s` se compose de lettres anglaises minuscules
> - `fill` est une lettre anglaise minuscule

---

Une idée fondamentale

Le problème est un simple exercice de coupe de cordes:

1. **Loop** sur la chaîne par étapes de `k`.
2. **Prenez** une sous-chaîne de longueur "k" (ou la partie restante).
3. **Pad** la dernière sous-chaîne avec `fill` si elle est plus courte que `k`.
4. **Store** chaque groupe dans une liste/une liste.

complexité temporelle: **O(n)**, où `n` est la longueur des `s`.
complexité de l'espace : **O(n)** pour la liste résultante.

---

Les solutions de code

Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**.

C'est pas vrai. Java

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

solution de classe publique {
public Chaîne[] scinderString(String s, int k, char fill) {
int n = s.longueur();
groupe int = (n + k - 1) / k;
Résultat de chaîne[] = nouvelle chaîne[groupes];

pour (int i = 0, idx = 0; i < n; i += k, idx++) {
Int fin = Math.min(i + k, n);
StringBuilder sb = nouveau StringBuilder(s.substring(i, fin));

// Pad seulement si c'est le dernier groupe et c'est court
Si (fin < n + k && fin - i < k) {
pour (int j = sb.longueur(); j < k; j++) {
sb.append(fill);
}
}
résultat[idx] = sb.toString();
}
le résultat du retour;
}
}
«» "

# # # # # #

'`python
de taper l'importation Liste

Solution de classe:
def divisString(self, s: str, k: int, remplissage: str) -> Liste[str]:
res = []
pour i dans la plage(0, len(s), k):
groupe = s[i:i + k]
si len(chunk) < k:
morceaux += remplissage * (k - len(chunk))
res.append(chunk)
retour res
«» "

C'est vrai. C++

'`cpp
#incluez <vecteur>
#incluez <string>

solution de classe {
public:
std::vector<std::string> divizeString(std::string s, int k, char fill) {
md::vecteur<std::chaîne> rés;
pour (size_t i = 0; i < s.size(); i += k) {
std::string chunk = s.substr(i, k);
si (chunk.size() < static_cast<size_t>(k)) {
Annexe k - taille du morceau(), remplissage;
}
res.push_back(chunk);
}
retour rés;
}
};
«» "

Les trois solutions fonctionnent dans le temps linéaire et n'utilisent que quelques variables auxiliaires.

---

Bien, mal et moche

Aspect du bien
- C'est quoi ?
**Complexité algorithmique** Aucune – la solution est déjà optimale. Sans objet
**Readability**= Utilise des noms de variables clairs et une seule boucle. Une logique de rembourrage trop compliquée peut être difficile à lire. Des boucles nichées ou une concaténation excessive de la chaîne peuvent prêter à confusion. Autres
**Pièges spécifiques à la langue** Python : découper des chaînes de caractères – encore bien pour des contraintes données. C++: oublier `#include <string>` conduit à compiler des erreurs. Autres
**Edge Cases**=Poigne les chaînes vides, `k` égale à la longueur de la chaîne et `k` supérieure à la longueur de la chaîne. Aucun. Autres
**Maintenabilité**La solution est concise et peut être étendue (p. ex., retour d'un vecteur de cordes). Aucun. Autres

À emporter

- **Bien** – Le scan linéaire avec rembourrage à la volée est à la fois efficace et élégant.
- **Bad** – Pas vraiment; le seul --bad-- est la complexité inutile.
- **Ugly** – L'utilisation de la concaténation des cordes à l'intérieur des boucles imbriquées ou le fait de ne pas gérer correctement le dernier groupe peut conduire à des bugs subtils.

---

Copie du blog optimisée par le SEO (Prêt à publier)

Description de la méta
> Code maître de leet 2138 – Divisez une chaîne en groupes de taille k. Voir les solutions Java, Python et C++, l'explication de l'algorithme, les cas de bord et les conseils d'entrevue pour obtenir votre prochain emploi.

Mots clés
«» "
LeetCode Diviser une chaîne dans des groupes de taille k
Solution Java LeetCode 2138
Solution Python Diviser la chaîne de caractères k
C++ diviser les groupes de chaînes k
manipulation de chaîne question interview
problème de codage de l'entrevue
question d'entretien avec un algorithme
défi de codage des entretiens d'emploi
«» "

Structure du blog

1. **Titre** – Code Crack 2138: Divisez une chaîne dans des groupes de taille k – Solutions Java, Python & C++
2. **Introduction** – Crochet : Vous voulez décrocher ce rôle d'ingénieur logiciel ? Commencez avec ce problème facile LeetCode. (en milliers de dollars)
3. **Déclaration de problème** – Comme ci-dessus.
4. **Algorithme Marche** – Expliquez l'approche O(n).
5. **Code Snippets** – Java, Python, C++ (comme montré).
6. ** Analyse de complexité** – Temps et espace.
7. **Cas et pièges d'Edge** – bons, mauvais, La mauvaise table.
8. **Conseils d'entrevue** – Comment discuter de ce problème avec les intervieweurs.
9. **Conclusion** – Résumer et encourager la pratique.

---

Mot final

- **Mise en oeuvre** la solution dans votre langue préférée et exécuter les cas de test fournis.
- **Ajouter** vos propres tests d'unité pour couvrir les cas de bord.
- **Pratique** expliquant l'algorithme verbalement – c'est ce que veulent les intervieweurs.
- **Partager** ce post sur LinkedIn et GitHub avec les bonnes balises pour augmenter votre visibilité.

Bon codage, et la meilleure chance d'atterrir ce travail de rêve! C'est ce qu'il a dit