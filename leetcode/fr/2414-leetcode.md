---
titre: LeetCode 2414. Longueur de la plus longue sous-chaîne alphabétique continue -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2414 – Longueur de la plus longue sous-chaîne alphabétique continue
**Difficulté** : Moyen **Tag** : Chaîne, deux-pointeurs

> Une chaîne alphabétique continue est une chaîne composée de lettres consécutives dans l'alphabet. (en milliers de dollars)
> Exemple: `"abc"` est valide, `"acc"` et `"za"` ne le sont pas.

---

Récapitulation des problèmes

Compte tenu d'une chaîne inférieure `s` (1 ≤ ≤ ≤ 105), retourner la longueur de la plus longue sous-chaîne contiguë où chaque paire de caractères adjacente diffère exactement de **1** dans leur valeur ASCII (c'est-à-dire qu'il s'agit de lettres consécutives de l'alphabet).

---

Solutions en 3 langues

> L'idée centrale est un seul balayage linéaire qui maintient une longueur d'exécution du bloc consécutif actuel.
> Quand le caractère suivant est *pas* le successeur du courant, le bloc se termine et nous réinitialisons le compteur.

---

C'est pas vrai. Java

"Java
***
* LeetCode 2414 – Longueur de la plus longue sous-chaîne alphabétique continue
*
Espace O(n)
*/
solution de classe {
publique Sous-chaîne continue(String s) {
// Edge‐case: chaîne vide – pas nécessaire par les contraintes mais sûre.
si (s) null (s) s.isEmpty() retourne 0;

int maxLen = 1; // sous-chaîne la plus longue vue jusqu'à présent
longueur du bloc courant consécutif

pour (int i = 0; i < s.longueur() - 1; i++) {
si (s.charAt(i + 1) - s.charAt(i) == 1) {
curLen++;
si (curLen > maxLen) maxLen = curLen;
} autre {
curLen = 1; // démarrer un nouveau bloc
}
}
retour maxLen;
}
}
«» "

---

# # # # # #

'`python
# LeetCode 2414 – La plus longue sous-chaîne alphabétique continue
# Python 3 – temps O(n), espace O(1)

Solution de classe:
Def le plus longContinuSous-chaîne(s: str) -> Int:
sinon s: # contrôle défensif – les contraintes garantissent len>= 1
retour 0

max_len = cur_len = 1

pour i dans la plage(len(s) - 1):
si ord(s)[i + 1] - ord(s[i]) 1 :
cur_len += 1
si cur_len > max_len:
max_len = cur_len
Sinon:
cur_len = 1

_retourner maxlen
«» "

---

C'est vrai. C++

'`cpp
// LeetCode 2414 – Substring continu alphabétique le plus long
// C++17 – temps O(n), espace O(1)

solution de classe {
public:
int le plus longContinu(chaîne s) {
si (s.vide()) retourne 0; // défensive

l'ent maxLen = 1, curLen = 1;

pour (size_t i = 0; i + 1 < s.size(); ++i) {
Si (s[i + 1] - s[i]] 1) {/ lettres consécutives
++curLen;
si (curLen > maxLen) maxLen = curLen;
} autre {
curLen = 1; // lancer un nouveau bloc
}
}
retour maxLen;
}
};
«» "

---

Article du blog – Le bon, le mauvais, et l'atroce de LeetCode 2414

Introduction

Si vous préparez pour les interviews de codage, vous avez probablement vu le problème **Le plus long Alphabetic Continuous Substring** sur LeetCode (#2414). À première vue, il semble trompeurment simple, mais il offre un grand moment d'enseignement à la fois **la pensée algorithmique** et **le code propre**. Dans cet article, nous disséquerons le problème, explorerons les points forts et les pièges de diverses stratégies de solution, et vous donnerons des idées favorables au SEO qui peuvent vous aider à décrocher votre job de technicien de rêve.

> **Mots clés**: *Longest Alphabetic Continuous Substring*, *LeetCode 2414*, *coding interview*, *Java Python C++*, *Two-pointer technique*, *string manipulation*, *O(n) solution*.

---

Récapitulatif du problème (Le bien)

- **Définition** : sous-chaîne où chaque paire de caractères adjacente est une lettre consécutive de l'alphabet (par exemple, `"abc"` ou `"xyz"`).
- **Objectif** : Retourne la longueur *maximum* d'une telle sous-chaîne.
- **Constraints**: "1 ≤ ≤ 105", toutes lettres minuscules.

Les contraintes nous disent immédiatement qu'il nous faut une solution **O(n)**; tout algorithme qui scanne la chaîne plus d'une fois (p. ex., boucles imbriquées) s'éteindrait à la limite supérieure.

---

### -Le mal – Pièges communs

Pourquoi il échoue Exemple
- C'est quoi ?
**Nested loops / DP**= O(n2) time= Une double boucle qui vérifie chaque sous-chaîne. Fonctionne pour de petites entrées mais TLE pour 105. Autres
**En supposant que "a" suit "z"**" Une interprétation erronée de la continuité "za" est *non* valide, mais certaines implémentations naïves peuvent la traiter comme consécutive. Autres
**Boîtes de bord manquantes**= Chaîne vide / caractère unique== Bien que les contraintes l'interdisent, la programmation défensive permet d'éviter les erreurs d'exécution dans les paramètres d'entrevue. Autres
**Utiliser la mémoire supplémentaire pour les suffixes**= O(n) espace mais inutile==En stockant toutes les sous-chaînes ou une carte de préfixes utilise la mémoire qui=n'est pas nécessaire. Autres
**Manquement de `StringBuilder` en Java**= Calculs d'index erronés= Les erreurs hors-par-un dans `charAt` conduisent à des résultats incorrects. Autres

Être conscient de ces erreurs est la première étape vers l'écriture propre, le code prêt à l'entrevue.

---

### --L'Ugly--Sur-ingénierie de la solution

Certains candidats essaient d'exagérer le problème :

1. ** Expressions régulières**
*Ugly* parce que le régex pour les lettres consécutives est non-trivial (`(?=a)b(?=c)`...).
2. ** Structures de données personnalisées* *
Construire un trie ou un suffixe, c'est trop tuer.
3. **Récursion**
Les sous-chaînes à balayage récursif augmentent inutilement la profondeur de la pile.

Ces approches rendent non seulement la solution plus difficile à lire, mais risquent également de dépasser les limites de temps ou de mémoire.

---

L'approche la plus propre – un seul pass à deux points

**Pourquoi c'est génial**:

- **Heure**: `O(n)` – passe linéaire unique.
- **Espace**: "O(1)" – seulement deux compteurs entiers.
- **Readability**: La logique est simple et facile à expliquer lors d'une entrevue.
- **Extensibilité**: Le même modèle fonctionne pour les problèmes connexes (par exemple, la plus longue augmentation de sous-chaîne, le plus long palindrome).

Code Pseudo

«» "
maxLen = 1
curLen = 1
pour i de 0 à len(s)-2:
si s[i+1] - s[i] 1 :
pour l'année 1
maxLen = maxLen, curLen
Sinon:
curLen = 1
retour maxLen
«» "

La principale perspicacité : **Si deux lettres adjacentes sont consécutives, étendre le bloc actuel; sinon, le remettre à 1**.

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Un seul scan
Autres Contrôle des bords

---

Variations et extensions

Variation Comment s'adapter Pourquoi ça compte
- C'est quoi ?
**Insensible à l'affaire** Autres
**Wrap‐around** (`"xyzabc"` valide)= Ajouter un contrôle pour `s[i] == 'z' && s[i+1] == 'a'.= Affiche la capacité de gérer les conditions de bord. Autres
**La plus longue séquence continue (pas nécessairement contiguë)**= Utilisez DP ou deux pointeurs avec un ensemble. Tests de compréhension de la subséquence par rapport à la subséquence. Autres

Expliquer ces variations peut démontrer la profondeur des connaissances et de la flexibilité.

---

Conseils d'entrevue

1. ** Éclaircir la suite**: Demandez à l'intervieweur si `'z'` suivi de `'a'` compte.
2. **Exposer la complexité à l'avance** : "Nous allons scanner la chaîne une fois, donc c'est O(n). (en milliers de dollars)
3. **Cas de bord de discussion**: Et si la chaîne est un caractère ? Et les entrées vides ? (en milliers de dollars)
4. **Travaux temps/espace**: Cette solution utilise un espace constant; si nous avons besoin de retourner toutes ces sous-chaînes, nous aurions besoin de plus d'espace. (en milliers de dollars)
5. **Afficher la confiance dans le style de codage**: Utilisez des noms de variables significatifs (`currentLen`, `maxLen`) et ajoutez des commentaires.

---

### -SEO-Friendly Conclusion

Le problème *Longe Alphabetic Continuous Substring* (LeetCode 2414) est une question d'entrevue classique qui teste la manipulation des chaînes, les algorithmes linéaires et la manipulation soigneuse des cas de bord. En maîtrisant la solution à deux points en Java, Python ou C++, vous démontrerez :

- **Efficacité algorithmique** (temps O(n), espace O(1))
- **Pratiques de codage propres** (variables claires, vérifications défensives)
- **Versatilité** (adaptation facile aux variations)

Que vous abordiez ce problème pour un défi de codage ou pour préparer une entrevue technique, la clé est de garder la solution simple, lisible et robuste. Bonne chance – et le codage heureux!

---

> ** Prêt à accepter votre prochain entretien? * *
> Plongez dans notre dépôt **free codage challenge** (lien) et pratiquez les problèmes LeetCode avec des explications du monde réel, des questions d'entrevue et des discussions communautaires.

---