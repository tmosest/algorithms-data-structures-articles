---
Titre: LeetCode 1163. Dernière sous-chaîne dans l'ordre lexicographique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1163 – Le dernier sous-chaîne dans l'ordre lexicographique

> **Problème**: Avec une chaîne `s`, retourner la sous-chaîne lexicographiquement la plus importante de `s`.
> **Contraintes**:
> * `1 <= s.longueur <= 4·105 "
> * `s` ne contient que des lettres anglaises minuscules.

La force brute O(n2) classique comparerait toutes les sous-chaînes possibles, ce qui est beaucoup trop lent pour les limites d'entrée.
Ci-dessous vous trouverez un *simple-pass, O(n) time, O(1) space* solution qui fonctionne dans **Java**, **Python** et **C++**.
Après le code, nous plongeons dans une courte discussion de style blog intitulée **=Le Bon, le Mauvais et l'Ugly==** qui explique pourquoi cet algorithme est si puissant – et où il peut vous faire trébucher – tout en étant SEO-friendly pour les recruteurs scannant votre portefeuille.

---

### # -Deux-Pointeurs Greedy (O(n) Heure)

L'idée clé est de maintenir deux postes de départ des candidats (`i` et `j`) et un décalage `k`.
À chaque étape, nous comparons les caractères `s[i+k]` et `s[j+k]`:

Que faire ?
C'est quoi ?
"s[i+k]] == s[j+k]"" L'accroissement `k` – les sous-chaînes correspondent jusqu'à présent. Autres
La sous-chaîne `i` est déjà meilleure. Déplacez `j` après ce rival: `j = j + k + 1`, réinitialisez `k`. Autres
La sous-chaîne à `j` beats `i`. Sauter `i` vers l'avant: `i = max(i + k + 1, j)'. Définir ensuite `j = i + 1` et réinitialiser `k`. Autres

Lorsque `j + k` atteint la fin de la chaîne, `i` indique le meilleur départ.
Retour `s.substring(i)` (Java/C++) ou `s[i:]` (Python).

Autres **Pourquoi le "max" ? * *
> Il saute sur les positions qui ne peuvent jamais battre le meilleur courant et maintient l'algorithme linéaire.

---

Code ## – Java, Python, C++

"Java
// Java 17
solution de classe publique {
public String lastSubstring(String s) {
int n = s.longueur();
i = 0, j = 1, k = 0;

pendant que (j + k < n) {
char a = s.charAt(i + k);
char b = s.charAt(j + k);

si a) b) {
k++; // même préfixe, continuez
} sinon si (a > b) {
j = j + k + 1; // i gagne, saut j
k = 0;
} autres { // a < b
i = Math.max(i + k + 1, j); // j gagne, bouge i
j = i + 1;
k = 0;
}
}
retourner s.substring(i);
}
}
«» "

'`python
# Python 3.10
Solution de classe:
def lastSubstring(self, s: str) -> str:
n = len(s)
i, j, k = 0, 1, 0

alors que j + k < n:
si s[i + k] == s[j + k]:
k += 1
élif s[i + k] > s[j + k]:
j = j + k + 1
k = 0
Autre: # s[i + k] < s[j + k]
i = max(i + k + 1, j)
j = i + 1
k = 0
retour s[i:]
«» "

'`cpp
// C++17
solution de classe {
public:
chaîne lastSubstring(chaîne s) {
int n = s.size(), i = 0, j = 1, k = 0;
pendant que (j + k < n) {
Si (s[i + k] == s[j + k]) {
++k;
} sinon si (s[i + k] > s[j + k]) {
j = j + k + 1;
k = 0;
} autre {
i = max(i + k + 1, j);
j = i + 1;
k = 0;
}
}
retour s.substr(i);
}
};
«» "

---

Les bons, les mauvais et les méchants

> **Objectif** – Rendez l'article utile pour la préparation d'entrevues, la recherche d'emploi et le référencement.

C'est pas vrai. Les bonnes

Aspect Pourquoi ça aide
C'est pas vrai.
**Temps linéaire**=Poigne les caractères `4·105` en millisecondes. Autres
**L'espace continu**= Seulement quelques indices entiers; idéal pour l'interview = aucun espace supplémentaire. Autres
Autres **Greedy + Two-Pointer**= Élégant; une fois que vous voyez le motif, il s'écaille à n'importe quel alphabet. Autres
**No Extra Libraries**" Fonctionne sur Java, Python, C++ – pas de "suffix array" tricks ou dépendances externes. Autres
**Modèle réutilisable**= La même idée apparaît dans =Trouver les problèmes de Subarray les plus importants; vous pouvez réutiliser la logique. Autres

- Oui. Les mauvais

Numéro
C'est pas vrai.
**Hard to Comprehension at First Sight**= L'index jonglant (i, j, k) et `max(i + k + 1, j)' peut être source de confusion. Autres
Une erreur `j = j + k + 1` pour `j = j + k` supprime un saut critique. Autres
**Edge Cases**= Les chaînes de caractères simples (`s = "a"`) reviennent immédiatement, mais oublier d'initialiser `j = 1` peut causer `ArrayIndexOutOfBounds`. Autres
De nombreuses solutions se copient-collent les unes des autres, mais des variations subtiles de la clause «else» peuvent changer la justesse. Autres

C'est vrai. L'Ugly

Comment éviter
C'est quoi ?
**En supposant `s[i+k] < s[j+k]` Déplace toujours `i` vers l'avant**.Il pourrait être préférable de déplacer `i` jusqu'au-delà du préfixe rival: `i = max(i + k + 1, j)`. Autres
**Mixing `substring` et `charAt` en Java**. Utilisez `charAt` pour la comparaison; `substring` pour le résultat final. Autres
**Python=Indice négatif**=Python gère heureusement les indices négatifs, mais vous devriez toujours vérifier `j + k < n` avant d'accéder. Autres
**Ne pas réinitialiser `k`** Autres
**Not Handling Patterns répétitifs**= Pour les chaînes comme `"aaaa"`, `k` peut continuer à incrémenter jusqu'à la fin. La boucle se termine toujours en O(n), mais la logique doit permettre à `k` de croître jusqu'à ce que `j + k` touche la fin. Autres

---

Analyse de complexité

Métrique
- C'est quoi ?
**Heure**="O(n)" – une passe linéaire="O(n)" – même="O(n)" – une seule boucle
**L'espace**="O(1)" – trois entiers="O(1)" – trois entiers="O(1)" – trois entiers
**Temps de fonctionnement de la pire affaire**

---

D'autres approches (pourquoi nous les oublions)

L'approche Temps Espace Remarques
C'est pas vrai.
Comparaison des sous-chaînes Brute-Force Autres
Construisez un Suffix Array. Autres
Manacher-style Sliding Window (en anglais seulement) "O(n)" mais plus de code (en anglais seulement) "O(n)" (en anglais seulement). Autres

---

Liste de contrôle du SEO et du recruteur

Mot-clé Pourquoi ça compte
C'est-à-dire
**Codage à gauche Les recruteurs d'identité de problème cherchent souvent une correspondance exacte. Autres
**Last Substring Ordre Lexicographique**Le nom du problème complet apparaît dans les entretiens d'emploi. Autres
**Two-Pointer Greedy**. Autres
**O(n) Temps, O(1) Espace** Autres
**Traitement de la chaîne**** Affiche que vous pouvez gérer la grande entrée efficacement. Autres
**Entretien d'emploi** / **Codage Challenge** ∙ Signifie que vous êtes prêt à l'entrevue. Autres

> **Astuce:** Ajouter un court lien *GitHub‐Gist* ou un extrait *code‐pen* pour que les gestionnaires embauchent puissent exécuter la solution immédiatement.
> Utilisez la même structure de dépôt entre les langues (par exemple `leetcode/1163/java`, `python`, `cpp`) pour garder votre portefeuille en ordre.

---

Dernier départ

- Oui. La solution avide à deux points est la façon la plus rapide* et la plus spatiale* de résoudre le Leetcode 1163.
- Exécutez-le avec soin : regardez l'arithmétique de l'indice, réinitialisez correctement le "k" et testez avec des cas de coin ("a"`, "aaab"`, "baaa"`).
- Oui. Lorsque vous écrivez la solution dans votre CV, incluez les extraits **Java**, **Python** et **C++** montrés ci-dessus, et peut-être un lien vers cet article pour démontrer une compréhension profonde.

Bon codage – et bonne chance pour votre prochaine interview! C'est ce qu'il a dit