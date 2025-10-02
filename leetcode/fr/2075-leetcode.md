---
titre: LeetCode 2075. Décoder le chiffre incliné -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

**LeetCode 2075 – Décoder le chiffre incliné* *

«» "
decodeCiphertext(encodéTexte, lignes)
«» "

Le message original `originalText` a été écrit dans une grille avec des lignes *rows*
et assez de colonnes pour que la colonne la plus droite ne soit jamais vide.
L'ordre de remplissage était *diagonal* – en haut à gauche → en bas à droite.
Après la construction de la grille, la chaîne encodée a été lue **row-wise** et ensuite
les caractères des mêmes diagonales ont été concaténés dans l'ordre
bleu → rouge → jaune ... (l'ordre de visite des cellules lors du remplissage).

Compte tenu de la chaîne codée et du nombre de lignes, récupérer l'original
texte (qui ne se termine jamais avec un espace).

Le défi est d'inverser l'encodage diagonal ** sans construire
matrice entière** – nous n'avons que la chaîne encodée unidimensionnelle.

---

- Oui. 2. Principales perspectives

Si la grille comporte des lignes «R» et des colonnes «C», chaque cellule sur la même diagonale
est espacé par des positions exactement `C + 1` dans la chaîne aplatie.

«» "
ligne 0: 0 1 2 3 ... C-1
ligne 1: C C+1 C+2 ...
ligne 2: 2C 2C+1 ...
«» "

Le premier élément de la première diagonale est à l'index `0`,
la deuxième diagonale commence à l'index `1`, ... la diagonale *j*‐th commence à
indice «j».
Nous pouvons donc:

1. Calculer `C = encodéText.length() / ranges`.
2. Pour chaque indice de départ `j = 0 ... C-1`
traverser la diagonale en ajoutant à plusieurs reprises `C+1` à l'indice actuel.
3. Ajouter chaque personnage visité à la réponse.
4. Enfin, retirez les espaces de fuite qui n'ont été ajoutés que pendant l'encodage.

Cette visite de chaque personnage exactement une fois – **O(n)** temps, **O(1)** espace supplémentaire.

---

- Oui. 3. Solutions de référence

Voici trois implémentations idiomatiques qui suivent exactement la même logique.

Code de la langue Commentaires
- C'est quoi ?
**Java**=Utilisez `StringBuilder` et `stripTrailing()` (Java 11+)
**Python** – enlève les espaces de fuite
**C++**=Utilisez `string` et `erase` pour tailler les espaces=

> **Pourquoi le plus intuitif diagonal ? * *
> Parce qu'il reflète la façon dont la grille a été remplie à l'origine – vous marchez le long d'une diagonale, qui est exactement comment le texte encodé a été construit.

---

3.1 Mise en œuvre de Java 17

"Java
Importation de java.util.*;

solution de classe {
chaîne publique décodeurCiphertext(chaîne codée) Texte, lignes int) {
int n = encodéTexte.longueur();
int cols = n / lignes; // nombre de colonnes
étape int = cols + 1; // sauter à la cellule suivante sur la même diagonale
StringBuilder sb = nouveau StringBuilder();

pour (int start = 0; start < cols; start++) {
pour (int idx = début; idx < n; idx += pas) {
sb.append(encodedText.charAt(idx));
}
}

// EncodéLe texte peut contenir des espaces de traînage – les dépouiller
retour sb.toString().stripTrailing();
}
}
«» "

**Complexité* *

- **Heure:** `O(n)` – chaque caractère est traité une fois.
- **Espace:** `O(n)` pour la chaîne de sortie; espace auxiliaire `O(1)`.

---

3.2 Mise en œuvre de Python 3

'`python
Solution de classe:
décodage Ciphertext(self, encodéTexte: str, lignes: int) -> str:
n = len(texte codé)
nombre de colonnes
étape = cols + 1 # distance jusqu'à la cellule diagonale suivante

res = []
pour commencer dans la plage(cols):
idx = début
alors que idx < n:
res.append(encodéText[idx])
idx += étape

retourner "".join(res.rstrip()
«» "

---

### 3.3 C++17 Mise en œuvre

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne de codeCiphertext(chaîne encodée) Texte, lignes int) {
int n = encodéText.size();
int cols = n / lignes; // nombre de colonnes
Étape int = cols + 1; // Étape diagonale
la chaîne rés;

pour (int start = 0; start < cols; ++start) {
pour (int idx = début; idx < n; idx += pas) {
res += encodéText[idx];
}
}

// Espaces de traçage
pendant que (!res.vide() && res.back() == ') res.pop_back();
retour rés;
}
};
«» "

---

- Oui. 4. Article du blog – Le bon, le mauvais, et l'acharnement de décoder le chiffre incliné

### 4.1 Titre & Meta Description

**Titre:**
> *Décoder le chiffre incliné – le bon, le mauvais et le mauvais (Java, Python, C++)*

**Meta Description:**
> Apprenez comment inverser un chiffrement diagonal en temps O(n).
> Guide étape par étape avec les solutions Java, Python et C++, ainsi que des conseils d'entrevue.

*(Mots-clés de référence: LeetCode 2075, Chiffre de code, Diagonal Traversal, Codage d'entrevue, Java, Python, C++)*

---

4.2 Aperçu

Ce que vous allez apprendre
- Oui.
Autres 1. Aperçu du problème de la grille
Autres 2. Pièges communs
Autres 3. La chaîne encodée en tableau 1-D
Autres 4. La matrice «Bad» – Brute-Force
Autres 5. L'Ugly – Edge Cases
Autres 6. Code Walkthrough de Java, Python, C++ extraits avec commentaire
Autres 7. Questions de style d'entrevue: Comment expliquer la solution et penser aux cas de test:
Autres 8. Takeaway (TL);DR et clés à emporter pour les recruteurs

---

### 4.3 Article complet (extrait)

> **Décoder un chiffre incliné : ce que tout ingénieur logiciel devrait savoir* *
>
> Dans de nombreuses interviews, vous rencontrerez des problèmes qui semblent nécessiter une programmation *grid*, *matrix* ou *dynamique*. Le chiffre incliné est l'un de ces défis faussement simples qui teste en fait votre capacité de penser en termes d'index plutôt que de structures de données.

> **Les bonnes**
> La solution élégante traite la chaîne codée comme un tableau 2-D *flatté*. Le seul truc ?
> **Étapes diagonales égales "cols + 1".**
> Cette vision transforme une reconstruction potentiellement quadratique en un seul balayage linéaire.

> **Les mauvais**
> Un premier instinct est de reconstruire la matrice complète:
> `` "
> char[][] grille = nouveau char[rows][cols];
> // remplir diagonalement, lire les lignes, etc.
> `` "
> C'est la mémoire O(rows * cols) et il faut encore deux passes.

> **Les impies**
> Les cas de bord mordent le codeur naïf:
> * `encodéText` pourrait être vide (`""".
> * Une ligne ('rows == 1`) – la sortie est identique.
> * Les espaces de recherche insérés pendant l'encodage doivent être supprimés, sinon la réponse sera erronée.
> Rappelez-vous `stripTrailing()` (Java) ou `rstrip()` (Python) – ce sont des sauveteurs de vie.

> ** Mise en œuvre de Java* *
> *(inclure le code du 3.1 ci-dessus)*

> ** Mise en œuvre du Python* *
> *(incluez le code de 3.2 ci-dessus)*

> **C++ Mise en œuvre**
> *(inclure le code de 3.3 ci-dessus)*

> **Conseils d'entrevue**
> 1. Clarifier la taille de la grille: `cols = encodéText.length() / rows`.
> 2. Visualisez les premières diagonales; écrivez-les sur papier.
> 3. Interrogez-vous sur la longueur la plus défavorable (106) – cela vous force à penser aux algorithmes O(n).
> 4. Mentionnez le cas de l'espace de fuite; les recruteurs aiment les candidats qui anticipent les pièges.

> **TL;DR**
> *Computer les colonnes, pas par `cols+1`, traverser diagonalement, couper les espaces de traînage. *
> Il est rapide, propre et démontre de solides compétences de manipulation de l'indice.

---

4.4 Pourquoi ce blog aide-t-il votre recherche d'emploi

1. **Démontre la résolution des problèmes** – L'article passe par l'intuition, les pièges et le code propre.
2. **Surmonte la compétence linguistique** – Fournit des solutions Java, Python et C++ côte à côte.
3. **SEO Friendly** – Mots-clés tels que *LeetCode 2075*, *Decode Cipher*, *Interview Coding* rendent le post décelable par les recruteurs à la recherche de défis algorithmes.
4. **Showcases Compétences en communication** – Des explications claires, des commentaires de code et des questions et réponses de type entrevue simulent des conversations d'entrevue réelles.
5. **Ready‐to‐Publish** – Copiez l'article dans votre portfolio ou LinkedIn. L'article attirera les vues et vous positionnera comme un ingénieur réfléchi.

---

- Oui. 5. Pensées finales

Décorer le chiffre incliné est une histoire d'interview parfaite:
un puzzle de grille apparemment complexe qui, une fois que vous voyez le bon modèle, s'effondre à un seul passage linéaire.
Implémentez la solution dans votre langue préférée, testez-la contre les cas de bord, et n'oubliez pas de couper ces espaces de traînage.

Bonne chance – et que les pas diagonaux soient toujours en votre faveur!